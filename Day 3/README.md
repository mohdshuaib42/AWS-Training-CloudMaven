## AWS Lap Excercise 
## 1:Launch a new EC2 instance from a public AMI; attach a fresh gp3 data volume, partition/format/mount it for app data, take a point-in-time snapshot, and provide secure access via both SSH and Session Manager.

Go to EC2 Dashboard → Launch Instance.

Choose a public AMI (e.g., Amazon Linux 2 / Ubuntu).

Select an instance type (e.g., t2.micro for testing).
![alt text](Screenshots/t1.0.png)
Configure key pair for SSH access.

Attach a security group allowing:

SSH (port 22) from your IP.

Session Manager access (requires SSM agent + IAM role).

Launch the instance.

2. Attach gp3 Data Volume
![alt text](Screenshots/t1.1.png)
From EC2 → Volumes, create a new gp3 EBS volume.
![alt text](Screenshots/t1.2.png)

3. Partition, Format & Mount the Volume
Connect to the instance via SSH 
![alt text](Screenshots/t1.3.png)

List block devices:
![alt text](Screenshots/t1.4.png)
lsblk
Partition the volume:

sudo fdisk /dev/xvdf


Create new partition → write changes.

Format with ext4 filesystem:

sudo mkfs -t ext4 /dev/xvdf1


Create a mount directory:

sudo mkdir /appdata


Mount the volume:

sudo mount /dev/xvdf1 /appdata


Verify:

df -h


4. Take Point-in-Time Snapshot

Go to EC2 → Volumes.
![alt text](Screenshots/t1.5.png)
Select the gp3 volume.

Click Actions → Create Snapshot.

Provide description (e.g., App Data Snapshot).
![alt text](Screenshots/t1.6.png)
Snapshot will serve as a backup / restore point.

5. Secure Access Setup

SSH Access:

Use key pair (.pem file) with command:

ssh -i my-key.pem ec2-user@<public-ip>

Screenshots for refrence are from t1.0 to t1.6

## 2: Create a simple golden AMI from a configured instance (web/app baseline), then launcha new instance from that AMI and verify the service comes up without any additional manual steps.

Configured a baseline EC2 instance with all required web/app services.
Verified that the instance is working as expected.
![alt text](Screenshots/t2.0.png)

Created an AMI from the configured instance (Golden AMI).
![alt text](Screenshots/t2.1.png)
![alt text](Screenshots/t2.2.png)
Launched a new EC2 instance using the Golden AMI.
![alt text](Screenshots/t2.3.png)
Verified that the service started automatically without any manual configuration.
![alt text](Screenshots/t2.4.png)
Confirmed that the new instance is fully operational and matches the baseline configuration
Screenshots for refrence are from t2.0 to t2.4

## 3: Migrate application data off the root disk to a separate attached EBS volume, snapshot that data volume, replace the original instance, and restore the data by attaching the volume to the new instance.
![alt text](Screenshots/t3.0.png)
Attached a new EBS volume to the running instance.
![alt text](Screenshots/t3.1.png)

Migrated application data from the root disk to the new EBS volume.

Created a snapshot of the data volume.

Terminated the original instance and launched a new instance.

![alt text](Screenshots/t3.2.png)
Attached the EBS volume to the new instance.
![alt text](Screenshots/t3.3.png)

Verified that all application data was restored and services were functioning correctly
![alt text](Screenshots/t3.4.png)
![alt text](Screenshots/t3.5.png)
![alt text](Screenshots/t3.6.png)
![alt text](Screenshots/t3.7.png)
![alt text](Screenshots/t3.8.png)
![alt text](Screenshots/t3.9.png)
![alt text](Screenshots/t3.10.png)

Screenshots for refrence are from t3.0 to t3.10

## 4: Restore an EBS snapshot to a new volume in a different Availability Zone, validate data integrity there, then copy the same snapshot to another Region, restore it, and verify cross‑region recovery.

Restored an EBS snapshot to a new volume in a different Availability Zone.

Attached the volume to an instance and validated data integrity.
![alt text](Screenshots/t4.1.png)
![alt text](Screenshots/t4.2.png)

Copied the snapshot to another AWS Region.

Restored the copied snapshot in the new Region.
![alt text](Screenshots/t4.0.png)

Verified that the data was fully intact and services were working in the cross-region instance.
Screenshots for refrence are from t4.0 to t4.2

## 5: Modify an EBS volume in place (size and/or type), expand the filesystem online, and confirm capacity and performance changes without downtime.

Selected the target EBS volume and modified its size/type in place.
![alt text](Screenshots/t5.0.png)

Expanded the filesystem on the instance without downtime.
![alt text](Screenshots/t5.1.png)

Verified the updated capacity and confirmed improved performance.
![alt text](Screenshots/t5.2.png)
![alt text](Screenshots/t5.3.png)

Screenshots for refrence are from t5.0 to t5.3

## 6: Create an AMI backup of a running instance, terminate the original, and relaunch a replacement from the AMI to confirm a clean, predictable rebuild.
![alt text](Screenshots/t6.0.png)

Created an AMI backup of the running instance.
![alt text](Screenshots/t6.1.png)
![alt text](Screenshots/t6.3.png)
Terminated the original instance.

Launched a new instance from the AMI.
![alt text](Screenshots/t6.4.png)
Verified that the new instance launched cleanly with all configurations intact, ensuring a predictable rebuild.
Screenshots for refrence are from t6.0 to t6.4

## 8: It's done and half of in previous tasks
Screenshots for refrence are from t7.0
![alt text](Screenshots/t7.0.png)
![alt text](Screenshots/t7.1.png)
![alt text](Screenshots/t7.2.png)
![alt text](Screenshots/t7.3.png)


