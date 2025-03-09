AWS Beginner Project 1
Problem Statement: Deploy a Static Website on AWS using S3, CloudFront and CI/CD with GitHub Actions 

Project Overview: In the above project you will deploy a static website using Amazon S3, you will configure cloud front for content delivery and setup CI/CD using GITHUB Actions.  

Pre-requisites
1.	Amazon Free Tier Account. 
2.	Knowledge on how to create IAM users and add permissions.

Section 1 - Step by Step Guide
1.	Login into AWS Management Console 
2.	Navigate to Storage – S3 
3.	Click on create a bucket 
         
4.	Check the AWS region where you are creating the bucket. 
5.	Select General Purpose. 
6.	Provide a unique bucket name. 
7.	Uncheck Block All public access
8.	Confirm the changes 
9.	Click on create bucket  
10.	The bucket has been created successfully.
 
11.	Click on the bucket name and navigate to the Properties. 
12.	Enable Static Website hosting.
13.	 In the hosting type select – Host a Static Website
14.	In the index document enter index.html and error document enter error.html
15.	Click on save changes

 
16.	I will create a sample html and error file and will upload into the S3 bucket. 
17.	Click on add files and select the html files. Click on Upload
          
18.	Let us test out if the index.html page is getting displayed using the bucket website endpoint. 
19.	Copy the endpoint URL and paste it in the browser. Use http://<URL>
 
20.	The message displayed will be Access Denied and need to add permission to the bucket policy. 
21.	Navigate to Bucket Permissions > Bucket Policy and Click on EDIT 
22.	 I will explain the code which is written in JSON format. The users need access to view the index.html content
                 
23.	Line 2 represents the latest version and should always be used. It specifies the policy language version
24.	The statement represents the list of permission rules and there is only one rule in the array
25.	The SID is optional, and I have named it PublicReadGetObject which means the rule allows public read access
26.	Effect can be allow or deny and here it means the action to read the file is permitted
27.	The principal is Who can access the bucket and the ‘*’ means anyone on the internet can access the objects in this bucket
28.	You can replace with an IAM role or AWS account id if you want to limit access or services
29.	The resource indicates who is affected and here it is the bucket name and /* means ‘it refers all the objects inside the bucket’
30.	Click on save changes
31.	Refresh the end point URL and the index.html page will be displayed. 
                
32.	Instead of index.html type in.html and it will redirect to the error page
               


Section 2 – Configure Cloud Front for Content Delivery 

33.	In the AWS management console, locate CloudFront Services
34.	Click on Create Distribution
               
35.	In the Set Origin Name, Select the Name of your S3 Bucket from the drop down
36.	Leave all the default settings as-is
37.	In the Web Application Firewall Select Do not Enable Security Permissions
38.	Click on Create Distribution. It will take 5 minutes to get completed. Copy the distribution name and paste in the browser address bar. 
               
39.	We will get an error message Access Denied while using the cloudfront URL. 
40.	How do we de-bug the error message. 
41.	While creating the distribution, add the index.html in the default root object under the general tab of the cloud front distribution 
 

42.	While creating the distribution, add the static website hosting property URL instead of selecting the default origin name. 

43.	Copy the entire URL  
 

44.	Paste it the Origin name 
 


 


Section 3 – Automate Deployments using GITHUB Actions 
45.	You will need a GITHIB Account 
46.	You will need to create a repo
47.	You will need the AWS Key ID and Secret Key
48.	Add the AWS KEY ID and Secret Key as mentioned below
49.	After creating a repo , navigate to settings 
50.	Locate Secrets and Variables – Click on it
51.	Select Actions
52.	Select Secrets Tab 
 

53.	Click on New Repository Secret
54.	Provide a name and add the secret id
 
55.	Click again in the New Repository Secret
56.	Provide a name and add the secret key
               
57.	Click on Add Secret 
58.	The secrets are added
             
59.	Now we will create a workflow in GITHUB and whenever a new change is pushed to the main branch and synchronized all files from the GITHUB report to the s3 bucket. 

60.	So, what does the workflow do is that when you push updates to the main branch of the main branch the workflow will clone the latest code, and it will authenticate using the AWS credentials and uploads the files to the S3 bucket automatically without manual intervention. 

Section 4 – Writing YAM code 
 
61.	Create a repo with public access and provide a description of why you are creating the repo. 
62.	Click on Actions and click on ‘Simple Workflow’
                
63.	Click on configure 
64.	Rename it to deploy,yml and past the code 
65.	Do not forget to update the bucket name 
           

66.	Click on commit changes
67.	The deploy code is available. 
68.	If you get an error, check credentials is correct while creating the secret key. 
69.	Also check permissions for the IAM user if you get an error. 
70.	There are no index or error files in my GitHub and the files got deleted in S3 bucket automatically. 
             
71.	Navigate to S3 and the files are not available. 
              
