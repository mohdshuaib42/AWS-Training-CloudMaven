## Task 1:
## Created two VPCs
![alt text](<Screenshots/Screenshot (166).png>)


## Created subnets for each VPC 
![alt text](<Screenshots/Screenshot (167).png>)

## Created route Table for public subnets of VPC A and attached the IGW
![alt text](<Screenshots/Screenshot (168).png>)
![alt text](<Screenshots/Screenshot (169).png>)

## Creating peering connection so that VPC A and VPC B can communicate with each other
![alt text](<Screenshots/Screenshot (170).png>) 

## Here we're accepting peering connection request.
![alt text](<Screenshots/Screenshot (171).png>)


## Successfully updated route table for both VPCs i.e. added peering route.
![alt text](<Screenshots/Screenshot (172).png>)


## Here we three instances two in private subnet of each VPC and bastion in VPC-A public subnet.
![alt text](<Screenshots/Screenshot (173).png>)


## Below we connected to private ec2 of VPC-A through bastion.
![alt text](<Screenshots/Screenshot (174).png>)


## Then Connected to private EC2 of VPC-B through private EC2 of VPC-A that means our peering connection is seccessfull established.
![alt text](<Screenshots/Screenshot (175).png>)

## minimal security groups:
![alt text](<Screenshots/Screenshot (177).png>)

## Deliverables
SG-ALB (sg-aaa111) — Inbound: TCP 80 from 0.0.0.0/0

SG-Web (sg-bbb222) — Inbound: TCP 80 from sg-aaa111

SG-Private (sg-ccc333) — Inbound: TCP 80 from 10.0.2.0/24

## Task 2:
## Creating an IAM role for EC2 with CloudWatchLogs write and S3:GetObject read
![alt text](<Screenshots/Screenshot (178).png>)
![alt text](<Screenshots/Screenshot (179).png>)

## Here launching the EC2 and assigning the role which we created earlier 
![alt text](<Screenshots/Screenshot (180).png>)
![alt text](<Screenshots/Screenshot (181).png>)

## Here we have tested the html webpage which is being served by our EC2
![alt text](<Screenshots/Screenshot (182).png>)


## Now we Created the extra 2gb volume and we will attach this to our EC2.
![alt text](<Screenshots/Screenshot (183).png>)
![alt text](<Screenshots/Screenshot (185).png>)


## After attaching the volume we mounted it in /dev/xvdf /data and created a simple text file in it 
![alt text](<Screenshots/Screenshot (184).png>)


## Created an AMI from the EC2 and name it as "base-app-ami"
![alt text](<Screenshots/Screenshot (186).png>)

## ✅ FINAL DELIVERABLES
Deliverable	Example
IAM Role ARN	arn:aws:iam::017820707918:role/EC2-S3-CloudWatch-Role
EC2 Instance ID	i-054a6cd9a8c58ef09
Web output	curl http://localhost → Hello World from EC2 Base Server
AMI ID	ami-04962f096cb50dfa9
EBS Volume ID	vol-0a2ef988648c21a03
Snapshot ID	snap-024fea3419eaedde7


## Task 3:
## Uploaded a simple index.html file in our S3 bucket next we will host this static page
![alt text](<Screenshots/Screenshot (188).png>)

## As we see here we have hosted our static page through AWS S3
NOTE: To serve a static website we must uncheck the public access of out S3 Bucket
![alt text](<Screenshots/Screenshot (189).png>)


## Now creating an ALB in VPC-A public subnet with a listener on port 80.
![alt text](<Screenshots/Screenshot (190).png>)
