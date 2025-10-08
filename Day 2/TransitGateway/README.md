# Connected three VPCs using Transit Gateway

## Each with a public subnet and an EC2 instance.
![alt text](<Screenshots/Screenshot (127).png>)

## Configured appropriate security groups to allow ICMP (ping) and HTTP traffic.
![alt text](<Screenshots/ec2 setup for vpc1 (2).png>)

## Created a Transit Gateway (TGW)
![alt text](<Screenshots/Screenshot (121).png>)


## Configured default route table association and propagation.
![alt text](Screenshots/rt-test-vpc-1.png)


## Attached Each VPC to the TGW
![alt text](<Screenshots/Screenshot (123).png>)
## Used Transit Gateway Attachments to link all three VPCs.

Enabled route propagation in TGW route tables.
Updated VPC Route Tables

Added routes pointing to the Transit Gateway ID for other VPC CIDR ranges.

## Verified Connectivity
Connected to EC2 instances using SSH (from one instance).
![alt text](<Screenshots/Screenshot (124).png>)
Used ping and curl commands with private IPs to test connectivity between instances: