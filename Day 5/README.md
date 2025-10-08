## Task 1:

![alt text](Screenshots/t1.0.png)
Here we are creating the S3 Bucket and naming it "testbucket-0142" we always have to make sure that we give a unique name to S3 bucket.

![alt text](Screenshots/t1.1.png)
We Enabled bucket versioning to keep multiple varients of the object.

![alt text](Screenshots/t1.2.png)
As we can see here the bucket has been successfully created.

![alt text](Screenshots/t1.3.png)
Setting up bucket policy for access from anywhere so that anyone can read the objects within the bucket.
```
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"PublicReadGetObject",
      "Effect":"Allow",
      "Principal":"*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::bucket-name/*"]
    }
  ]
}
```


![alt text](Screenshots/t1.4.png)
Here we successfully uploaded a python file to our bucket 

![alt text](Screenshots/t1.5.png)
Testing access from terminal using curl.

![alt text](Screenshots/t1.6.png)
Opening the content in the web browser using the URL.

![alt text](Screenshots/t1.7.png)
In a versioning enabled bucket delete creates a delete marker as the current version, the object will appear removed but in a normal GET but prior versions still exists.
As we see here the delete marker in the type section.

![alt text](Screenshots/t1.8.png)
Now we deleted the delete marker object and now the prior version is the current version.

![alt text](Screenshots/t1.9.png)
After doing this all we have our hello.py file again available. 

## Task 2:
![alt text](Screenshots/t2.0.png)
We created a Elastic file system for concurrent read/write from multiple instances.

![alt text](Screenshots/t2.1.png)
These are the instances we have MyVM1 and MyVM2 are the instances in the private subnets and in two different AZs these two instances will be connected to our EFS.

![alt text](Screenshots/t2.2.png)
Here after installing the EFS utilities in our machine now we have mounted the efs inside /mnt/efs, it is the screenshot of MyVM2.

![alt text](Screenshots/t2.3.png)
After mounting the EFS we created a simple text file containing some content inside it. 

![alt text](Screenshots/t2.4.png)
As we see here It is MyVM1 after installing and mounting the efs here we can see the test.txt is present which was created in different machine so that means concurrent read/write is working perfectly with our EFS.

Note: The EFS and MyVM1, MyVM2 are in the same VPC but VM1 and VM2 are in different private subnets and in two different AZs.

## Task 3:
## Static hosting
Assume we a static website(HTML,CSS,JS) hosted on S3 and we want to make it accessible to users worldwide — efficiently and cost-effectively..

We have two options now:
## Option 1:
We host static content in Amazon S3.

We configure an Application Load Balancer (ALB) in front of it.

ALB forwards HTTP requests to a target group, which might be:
An S3 static website endpoint (via custom target),
## Advantage:
We can integrate with WAF, sheild through ALB for security.
## Disadvantage:
ALB costs per hour + per LCU (Load Balancer Capacity Unit). For pure static hosting, that’s unnecessary overhead.
## ALB is great for dynamic applications — not for static websites.

## Option 2:
S3 + CDN (CloudFront)
Architecture

Host website in S3 bucket (Static Website Hosting enabled).
Use Amazon CloudFront as a CDN (Content Delivery Network) in front of it.
CloudFront caches content at edge locations globally.
## Advantage:
CloudFront caches content close to users → low latency and high throughput.
## Disadvantage:
More configuration (OAC, distributions, caching behavior).
## S3 + CloudFront = best practice for static hosting: fast, secure, and cheaper than S3 + ALB.

## Task 4:
![alt text](Screenshots/t4.0.png)
Uploading a simple text file in S3.

![alt text](Screenshots/t4.1.png)
After some modification we uploaded the same file and as we see here now we have two versions of the file1.txt because we enabled versioning in our bucket that's why we have current and non current version.

![alt text](Screenshots/t4.2.png)
Here we are creating a life cycle rule.

![alt text](Screenshots/t4.3.png)
We set 30 days the objects become noncurrent and it will move to standard IA Storage class. And 60 days for Glacier flexible.
![alt text](Screenshots/t4.4.png)
Transitions.

![alt text](Screenshots/t4.5.png)
We have successfully created the lifecyle rule for our S3 bucket and as we see here the status is Enabled.