A 3-tier architecture is a well-established software application architecture that organizes applications into three logical and physical computing tiers: the presentation tier, the application tier, and the data tier. In AWS, this architecture is implemented using a variety of managed services to ensure scalability, high availability, and security.
First off, enter the AWS Console & make sure you have specified your region (US East — N. Virginia). Then navigate to VPC, select “create VPC”, & name it. I am naming mine, “Project-VPC”.
Go to your Subnets page, and select “Create subnet”. Locate the correct VPC for each subnet, and begin configuring.
The next four subnets are for my application tier and my database tier. I will name them “app-subnet-1”, “app-subnet-2”, “db-subnet-1”, and lastly “db-subnet-2”.
Now that our subnets are created, we will set up the internet gateway. take a peek at the left hand dropdown menu, and choose “internet gateway”. Select “create internet gateway”, name it, and finalize by clicking “Create internet gateway”. Inside your internet gateway choose “Actions”, “attach to VPC”, then select your VPC, and then choose “Attach internet gateway”.

Next, we will navigate to the Route Tables page. Our subnets should be attached to our main route table by default, but we are going to make sure each tier has it’s own routing table.

The Application subnets and the DBsubnets will have their own private routing tables. When those are created, we will create a public route table for our two Presentation (Web) subnets.
Again, on from the dropdown menu on the left choose “NAT Gateway”, and “Create NAT gateway”. Go ahead and name it (mine is “3-tier-NAT”), choose a public subnet (web-subnet-1), and make sure to select “Allocate Elastic IP”. Then, click “Create NAT gateway”. This will be used to connect our private subnets to the internet.
In the AWS console, locate and select the service “EC2”. Then from the left-hand drop-down menu, choose “Launch Templates” and “Create launch template”. Because this is for our Presentation tier, I am naming mine “web-asg”. Click the box below for “guidance and help with setting up your template with EC2 Auto Scaling”.
You can begin this process right from the launch templates page. Just select one of the templates, I will start with “web-asg”, and under the “Actions” choose “Create Auto Scaling Groups”.
Make sure that it is an Application Load Balancer, that it is internet-facing, and that you have selected the correct VPC and subnets. Scroll down and choose the “internet-facing” option, then make sure your “Listeners and routing”.
Next, we will navigate to the RDS services page. From the left-hand drop-down menu select “Subnet groups” and then “Create subnet group”. I am naming this one, “db-tier-aws”. You can add a description, and then make sure you select your correct VPC and add your database subnets, then click “Create”.

Now that we did that, lets go back to the RDS services page and select “Databases” and “Create database”. We will select the standard option, with a “MySQL” engine type, and a “Free tier” template.
For the first test, lets go to our instances in the EC2 services page. Select one of our web tier EC2’s and open up the public IPv4 address in a new browser tab.
For the second test, let’s connect to that same EC2 through the terminal, and then ssh into the Application Tier from there.
Finally, and for the last test…lets connect to the Database tier from our Application Tier…
And that is how to make an AWS 3-Tier Architecture — now go out for a three course meal!
