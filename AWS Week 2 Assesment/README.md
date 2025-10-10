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


## Created a Target Group 
![alt text](<Screenshots/Screenshot (191).png>)


## Here we are creating the ASG 
![alt text](<Screenshots/Screenshot (192).png>)

## As we can see the page using the ALB DNS and also showing the s3 logo
![alt text](<Screenshots/Screenshot (194).png>)
## Deliverables
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::test-portfolio-bucket42/*"
        }
    ]
}
```
Item	Example / What to Include
S3 Bucket Name	test-portfolio-bucket42 
ALB DNS Name	http://public-app-alb-1022207104.eu-north-1.elb.amazonaws.com/
Target Group ARN	arn:aws:elasticloadbalancing:eu-north-1:017820707918:targetgroup/tg-public-app/3671b3e184f39a92
ASG Name	asg-public-app
Desired Capacity 1	

## Task 4
## Here we are creating a DB instance which is a private app db
![alt text](<Screenshots/Screenshot (195).png>)

## We have ran a user data script when we were launching our ec2 from the base app image from task 2 in that script we installed httpd and gave the commad to connect to our private app db if it would show the html page and as we can see here we tested it using curl.
![alt text](<Screenshots/Screenshot (196).png>)

## And also mounted the efs 
![alt text](<Screenshots/Screenshot (197).png>)
![alt text](<Screenshots/Screenshot (198).png>)

## 🧾 Deliverables Summary
Item	Example / What to Include
RDS Endpoint	private-app-db.cp4688a0wfxo.eu-north-1.rds.amazonaws.com
RDS Instance Identifier	private-app-db
EFS ID	fs-0190295f1de91d477
Evidence of Mount yes df -h shows /mnt/efs
Private App EC2 Private IP	10-1-1-42
Proof of Access	curl 10-1-1-42
Private App RDS & EFS mounted!

SG Rules	
SG-RDS: MySQL 3306 from SG-PrivateApp
SG-EFS: NFS 2049 from SG-PrivateApp
SG-PrivateApp: HTTP 80 from VPC-A private CIDR / SG-Web


## Task 5:
## First we are creating the VPC 
![alt text](<Screenshots/Screenshot (203).png>)

## Downloading AWS Client VPN FOR DESKTOP 
![alt text](<Screenshots/Screenshot (204).png>)

## Genrating keys and certificates for both client and server
![alt text](<Screenshots/Screenshot (206).png>)
![alt text](<Screenshots/Screenshot (207).png>)
![alt text](<Screenshots/Screenshot (208).png>)

## Importing certificates in ACM for server
![alt text](<Screenshots/Screenshot (209).png>)

## Importing certificates in ACM for client
![alt text](<Screenshots/Screenshot (211).png>)

## As we see here both for server and the client certs have been issued
![alt text](<Screenshots/Screenshot (212).png>)

# Creating Client VPN Endpoint
![alt text](<Screenshots/Screenshot (215).png>)

## Associating with our target network which is our VPC which we created in the first step
![alt text](<Screenshots/Screenshot (217).png>)

# now adding authorization rules
![alt text](<Screenshots/Screenshot (218).png>)

## installing aws vpn client so that we could connect to our vpn after downloading the client configuration file the add vpn configuration file and display name then we will connect
![alt text](<Screenshots/Screenshot (219).png>)

## As we can after importing the oppn config file we have successfully connected 
![alt text](<Screenshots/Screenshot (220).png>)

## Checking the connection details 
![alt text](<Screenshots/Screenshot (221).png>)

## In our CMD WE SEE HERE WE ARE CONNECTED TO AWS CLIENT VPN 
![alt text](<Screenshots/Screenshot (222).png>)


## Thank you Manish sir for these two great AWS Weeks 
