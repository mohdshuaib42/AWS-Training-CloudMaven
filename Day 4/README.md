## 1: 
![alt text](Screenshots/t1.0.png)
Here we are creating a Launch template to be used in ASG.

![alt text](Screenshots/t1.1.png)
Setting up network setting.

![alt text](Screenshots/t1.2.png)
Adding user data script for apache webserver and a simple web page.

![alt text](Screenshots/t1.3.png)
We already have two EC2s running and serving a simple web-page. 

![alt text](Screenshots/t1.4.png)
Now Creating an ALB the traffic distribution.

![alt text](Screenshots/t1.5.png)
Here we are creating a target group to the LB route the traffic.

![alt text](Screenshots/t1.6.png)
Here we have 0 Healthy instances because we have not registered our instances.

![alt text](Screenshots/t1.7.png)
This is the LB in Provisioning state.

![alt text](Screenshots/t1.8.png)
![alt text](Screenshots/t1.9.png)
Now our LB is working as expected. 

![alt text](Screenshots/t1.10.png)
Here we have created the AutoScaling Group for scaling up and down based on demand.

![alt text](Screenshots/t1.11.png)
It's the Overview 

## 2:

![alt text](Screenshots/t2.0.png)
Here we created a instance to send load to Load Balancer.

![alt text](Screenshots/t2.2.png)
![alt text](Screenshots/t2.3.png)
Here we are sending huge reqs.. to servers.


![alt text](Screenshots/t2.4.png)
As we can see the Requestcount goes up.

## 3:
![alt text](Screenshots/t3.0.png)
Now I am creating a second target group.

![alt text](Screenshots/t3.1.png)
As we can see the second target group has been created.

![alt text](Screenshots/t3.2.png)
Overview of of 1st TG

![alt text](Screenshots/t3.3.png)
And this is the second target group  having same instances.

## 4:
![alt text](Screenshots/t4.0.png)
View of our ASG having desired capacity 2, min 2, and max 5

![alt text](Screenshots/t4.1.png)
Here we manauly terminated an instance 

![alt text](Screenshots/t4.2.png)
Now we see 1 healthy and 1 unhealthy 

![alt text](Screenshots/t4.3.png)
Now we see here the ASG automatically launching an instance because the minimum and desired capacity is 2, as we deleted one running instance, that is why new instance is being launched by ASG.