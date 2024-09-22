### Serverless Deployment using AWS S3, AWS Lambda, Amazon DynamoDB, Amazon API Gateway and Amazon CloudFront 

Configuring Amazon DynamoDB
- Create a database table name "studentData"
- Create a partition key "studentid"  (partition key here is the primary key which will uniquely identify a student in this case)
- Create table

Configuring AWS Lambda
- Create a function to fetch data 'getStudent' select runtime as Python 3.12
- Change default execution role to "use an exisitng role" choose "lambdaDynamoDB-role"
- Paste the code from "getStudents.py" (Make sure you have selected the right region name in the code as your AWS account region) and then deploy code, create test, give event name. Test code manually it should give empty list [], as expected the table values are empty and nothing to fetch

- Create a function to post data 'insertStudentData' select runtime as Python 3.12, copy the code from "insertStudent.py", deploy code and then create test, give event name and values like and test the code manually it should give output as "status code 200 ok" "student data saved successfully"

```
{   "studentid": "1001",
    "name": "River",
    "class": "A",
    "age": "13"
}

```
Configuring Amazon API Gateway
- To Create a REST API 
- Select API name
- Choose API endpoint type "edge-optimized"
- Create a method 'get' and select integration with Lambda and select Lambda Functions and region accordingly, similarly create another method 'post'
- Create a 'new'stage like "PROD"
- Enable CORS
- Deploy API
- Find and copy invoke URL: paste the URL in API_ENDPOINT of "Script.js"

Configuring Amazon S3 bucket
- Create a bucket
- Enable Static website hosting from "properties" tab, give index document as "index.html"
- Allow Public access and update the bucket policy from "permissions" tab, change here s3 bucket name with yours (In case without using CloudFront, CloudFront will incur charges, CloudFront is suggested for enhanced security, to eliminate public access to your bucket for security concerns)
```
{
  "Id": "Policy1726929142972",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1726929140819",
      "Action": [
        "s3:GetObject"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::serverless-deployment-demo/*", 
      "Principal": "*"
    }
  ]
}
```

- Upload "index.html" and "script.js" files

Configuring CloudFront Distribution for enhanced security
- Origin domain (select the S3 bucket)
- Nmae will be auto-populated
- Origin access - Select Legacy access identities or OAC - Create new OAI or OAC (This will act as a single cloudFront user access)
- Select the update bucket policy
- WAF disabled
- Select Price class 
- Default root object as "index.html"
- Click on create distribution

- Copy the Static website URL and hit it on the browser to view your hosted website !! (without cloudFront)
- Copy the CloudFront Distribution domain name and hit it on the browser once deployed  to view your hosted website (with cloudFront)
  
