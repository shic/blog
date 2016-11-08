---
layout:     post
title:      "Amazon Web Service"
date:       2016-11-07 12:00:00
author:     "Shi"


---



# EC2

## Copy instance

### Copy instance from one account to another

From the destination account: 

1. Find the AWS Account ID from "User name > Security Credentials > Account Identifiers > AWS Account ID".

From your current account: 

1. Right click on the instance and choose "Create Image (AMI)"

2. Check the "AMIs" pane. You need to edit its permissions to be able to use from another AWS account : 

   Right click on the AMI > Modify Image Permissions > Insert AWS Account Number of the destination account.

3. Remember AMI ID

Switch to the destination account's AWS console. 

1. Navigate to "Instances" pane. 
2. Click the "Launch Instance" button -> in the "My AMIs" tab, Check "Shared with me" -> Search AMI by entering the AMI ID.
3. Create the instance STEP BY STEP creating Security Group
4. Create an Elastic IP and bind it to new instance. NETWORK & SECURITY -> Elastic IPs -> Associate Address 

#### Note:

[Guide 1](https://knackforge.com/blog/sivaji/how-move-aws-ec2-instance-one-account-another)

[Official guide: source](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/sharingamis-explicit.html)

[Official guide: destination](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/usingsharedamis-finding.html)