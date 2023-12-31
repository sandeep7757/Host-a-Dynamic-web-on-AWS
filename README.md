﻿# Host-a-Dynamic-web-application-on-AWS
In this project , We will deploy a dynamic website on AWS by uploading the code into a s3 bucket in a zip file.
# Prerequisites:
 AWS account
# Task to do:
1. create a S3 bucket
2. Upload the application code (zip file) 
3. create a IAM role
4. create a Instance
# step 1: create a s3 Bucket
You will need to create an S3 bucket to upload a application code (in a zip file).

To do this, login into your AWS management console and search for S3 and select it to display the S3 dashboard.
1. click on Create bucket and now give a bucket name as shown below 
![image](https://github.com/sandeep7757/Host-a-Dynamic-web-on-AWS/assets/84711922/ebf698f8-8d25-433b-9c46-f05a1b4cb85b)
![image](https://github.com/sandeep7757/Host-a-Dynamic-web-on-AWS/assets/84711922/1b92906b-78ca-4159-9888-53f4dea5c6b1)
![image](https://github.com/sandeep7757/Host-a-Dynamic-web-on-AWS/assets/84711922/da668ff9-77ec-4f13-b014-47e8e7f7e4ef)
2. click on create bucket, it will create you a bucket
3. now click on the bucket you created and upload the zip file to this bucket.
# step 2: create a IAM role
Now, EC2 want to pull code from S3. So you want to create IAM Role to give EC2 permission to access S3.
To do this, from the Services drop-down, select IAM from the Security, Identity& Compliance section. From the IAM dashboard, click on Roles. Then Click on Create role.
![image](https://github.com/sandeep7757/Host-a-Dynamic-web-on-AWS/assets/84711922/98e274ce-0966-4588-af89-f5f8086d5a56)
Choose EC2 and click Next: Permissions.
![image](https://github.com/sandeep7757/Host-a-Dynamic-web-on-AWS/assets/84711922/a07f8b5d-cd54-454c-a760-74b3bd1b7e31)

Search for S3 and check AmazonS3FullAccess. Then click Next: Tags.
![image](https://github.com/sandeep7757/Host-a-Dynamic-web-on-AWS/assets/84711922/c826628c-9470-4e7d-8e0c-44e0f1a35d68)

Click on Next: Review.

Give the role name and description. Then click on Create role.

Now, the role has been created successfully.
# step 3: create a instance
we need to create a EC2 instance to install apache and copy the s3 bucket content to it.
1.Select Amazon linux 2,security group and vpc default make sure to allow port 80, attached the IAM role created.

Connect to the instance:

then . 
commands:
To ensure that all of your software packages are up to date, perform a quick software update on your instance.

# sudo yum update -y

Install the lamp-mariadb10.2-php7.2 and php7.2 Amazon Linux Extras repositories to get the latest versions of the LAMP MariaDB and PHP packages for Amazon Linux 2.

# sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2

Now, you can install the Apache web server, MariaDB, and PHP software packages.

# sudo yum install -y httpd mariadb-server 

Start the Apache web server.
# sudo systemctl start httpd 
Use the systemctl command to configure the Apache web server to start at each system boot.
# sudo systemctl enable httpd
You can verify that httpd is on by running
# sudo systemctl is-enabled httpd 
Now, you want to copy content of website from S3 to directory /var/www/html in EC2 . Make sure you copy your S3 bucket name.
# sudo aws s3 cp s3://dynamicwebapp-77557 /var/www/html/ --recursive
To verify that content is copied to /var/www/html .
# cd  /var/www/html 
# ls
#unzip the file
# sudo unzip <filename>.zip 
#moving the content of files to /var/www/html path
# sudo mv <filename>/* .
#removing the unwanted files 
# sudo rm -rf <filename>.zip <filename> #removing the unwanted files 

Now copy the public ipv4 DNS or the public ip of the EC2 instance , application is hosted.

![image](https://github.com/sandeep7757/Host-a-Dynamic-web-on-AWS/assets/84711922/43206b6f-01f8-4c30-9ca9-8e31e77cf0b9)

Thank you 
