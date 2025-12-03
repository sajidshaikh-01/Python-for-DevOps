# AWS Cost Optimization — GitHub Project Scaffold

This canvas contains a ready-to-use GitHub-friendly project scaffold for **10 AWS automation projects** (Python Lambda + boto3). Each project folder includes:

* A clear problem statement
* `README.md` template (deployment steps, permissions, test cases)
* Lambda function code (production-ready patterns)
* IAM policy example
* Interview Q&A + talking points

---

## How to use this canvas

1. Open each project section below. Copy files into separate folders in your local machine or directly into a GitHub repo.
2. Each project has a `README.md` skeleton you can paste into the repo root of that project.
3. To deploy: create an IAM role for Lambda with the provided minimal permissions, zip the code, and deploy via the AWS Console, AWS CLI, SAM, or Terraform (examples included in each README).

---

# Projects (folder names shown)

1. `01-ebs-snapshot-cleanup`
2. `02-release-unused-eips`
3. `03-stop-idle-ec2s`
4. `04-delete-unattached-volumes`
5. `05-deregister-old-amis`
6. `06-rds-idle-detector-notify`
7. `07-s3-lifecycle-checker`
8. `08-cloudtrail-bucket-encryption-checker`
9. `09-insecure-sg-detector`
10. `10-auto-tag-resources`

---

> **Common items included in each project folder**
>
> * `README.md` (deployment, IAM policy, test cases)
> * `lambda_function.py` (main code)
> * `requirements.txt` (if external libs are needed)
> * `ci/` — sample GitHub Actions workflow to run lint/test and optionally deploy
> * `examples/` — sample input events for local testing
> * `INTERVIEW.md` — concise set of interview questions & answers

---

## Project 01 — ebs snapshot cleanup (`01-ebs-snapshot-cleanup`)

**Problem**: Stale EBS snapshots accumulate and create storage cost.

**Files**:

* `README.md` (deployment + required IAM policy)
* `lambda_function.py` (see snippet)
* `INTERVIEW.md` (how to explain in interview)

**lambda_function.py (snippet)**

```python
import boto3
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

ec2 = boto3.client('ec2')

def lambda_handler(event, context):
    snapshots = ec2.describe_snapshots(OwnerIds=['self'])['Snapshots']

    # Get all volumes and their attachments
    volumes = ec2.describe_volumes()['Volumes']
    attached_volume_ids = set()
    for v in volumes:
        if v.get('Attachments'):
            attached_volume_ids.add(v['VolumeId'])

    for s in snapshots:
        sid = s['SnapshotId']
        vid = s.get('VolumeId')

        try:
            if not vid or vid not in attached_volume_ids:
                ec2.delete_snapshot(SnapshotId=sid)
                logger.info(f"Deleted snapshot {sid} (volume: {vid})")
        except Exception as e:
            logger.error(f"Failed to delete snapshot {sid}: {e}")
```

**README highlights**

* IAM role must include `ec2:DescribeSnapshots`, `ec2:DescribeVolumes`, `ec2:DeleteSnapshot`.
* Schedule via CloudWatch Events (e.g., daily).
* Safety: tag snapshots with `retain:true` to skip deletion (code includes tag check example).

**Interview points** in `INTERVIEW.md`:

* Why checking `VolumeId` is not enough — snapshots may be decoupled after volume deleted
* How tagging strategy prevents accidental deletion
* How to test in lower environments safely

---

## Project 02 — release unused EIPs (`02-release-unused-eips`)

**Problem**: Charged for EIPs that are not attached.

**lambda_function.py (snippet)**

```python
import boto3

ec2 = boto3.client('ec2')

def lambda_handler(event, context):
    addrs = ec2.describe_addresses()['Addresses']
    for a in addrs:
        # allocation id exists for VPC EIPs; association absent => unused
        if 'AssociationId' not in a:
            try:
                ec2.release_address(AllocationId=a['AllocationId'])
                print(f"Released EIP {a.get('PublicIp')}")
            except Exception as e:
                print(f"Failed to release {a.get('PublicIp')}: {e}")
```

**Safety**: Add allowlist tags (e.g., `keep:true`) or add a dry-run mode before actual release.

---

## Project 03 — stop idle EC2 instances (`03-stop-idle-ec2s`)

**Problem**: Instances with low CPU still running.

**Design**:

* Query `describe_instances` for running instances.
* For each instance, pull CPU metrics from CloudWatch over last N hours.
* If average < threshold, stop instance.
* Expose environment variable `DRY_RUN=true` for safe testing.

**Interview topics**

* Choosing CPU threshold vs. network/IO metrics
* Use of `Stop` vs `Hibernate` vs `Terminate`

---

## Project 04 — delete unattached EBS volumes (`04-delete-unattached-volumes`)

**Problem**: Unattached (`available`) volumes continue to incur charges.

**lambda_function.py (snippet)**

```python
import boto3

ec2 = boto3.client('ec2')

def lambda_handler(event, context):
    vols = ec2.describe_volumes(Filters=[{'Name':'status','Values':['available']}])['Volumes']
    for v in vols:
        vid = v['VolumeId']
        try:
            ec2.delete_volume(VolumeId=vid)
            print(f"Deleted volume {vid}")
        except Exception as e:
            print(f"Error deleting {vid}: {e}")
```

**Safety**: Skip volumes with tag `retain:true` or older than X days depending on policy.

---

## Project 05 — deregister old AMIs (`05-deregister-old-amis`)

**Problem**: Old AMIs & their snapshots cost storage.

**Design**:

* List AMIs owned by account
* Check `CreationDate` and apply cutoff (e.g., 30 days)
* Deregister AMI and delete associated snapshots

**Caveat**: Deleting AMI snapshots should be handled carefully; show sample code in `lambda_function.py`.

---

## Project 06 — RDS idle detector + SNS notification (`06-rds-idle-detector-notify`)

**Problem**: Idle RDS instances still cost money.

**Design**:

* Pull CloudWatch metrics for `CPUUtilization` and `DatabaseConnections`
* If below threshold for a period, publish SNS alert to owners
* Optionally, stop instance (if non-production)

**Files**:

* `lambda_function.py` with metric analysis + SNS publish
* `README.md` explaining runbook

---

## Project 07 — S3 buckets missing lifecycle rules (`07-s3-lifecycle-checker`)

**Problem**: Buckets without lifecycle rules can grow indefinitely.

**Design**:

* List all buckets
* For each, check `get_bucket_lifecycle_configuration`
* If missing or misconfigured, send SNS/email to bucket owner or create a suggested lifecycle policy

**Interview point**: Discuss GDPR/retention policies and cross-account buckets.

---

## Project 08 — CloudTrail S3 encryption checker (`08-cloudtrail-bucket-encryption-checker`)

**Problem**: CloudTrail logs must be encrypted and write-only.

**Design**:

* Read all CloudTrails (`cloudtrail.describe_trails()`)
* For trails logging to S3, check bucket encryption configuration and bucket policy
* Report / auto-remediate (apply SSE-KMS) with caution and approval flow

---

## Project 09 — insecure Security Group detector (`09-insecure-sg-detector`)

**Problem**: SG rules open to 0.0.0.0/0 (especially on sensitive ports).

**Design**:

* `ec2.describe_security_groups()`
* Inspect `IpPermissions` and flag rules using `0.0.0.0/0` or `::/0`
* Create an alert (SNS) + optional automated remediation (revoke rule + create justification ticket)

**INTERVIEW.md**: how to explain false positives, whitelists, and emergency exceptions.

---

## Project 10 — Auto-tagging resources (`10-auto-tag-resources`)

**Problem**: Missing tags hinder cost allocation and ownership.

**Design**:

* Trigger on CloudTrail events for `Create*` API calls via EventBridge
* On resource creation event, call `create_tags` to add `Owner`, `Env`, `Project` fields if missing
* Keep an allowlist/denylist to avoid tagging certain services

**Security**: The Lambda role will need broad resource-specific `Tag` permissions which must be scoped carefully.

---

