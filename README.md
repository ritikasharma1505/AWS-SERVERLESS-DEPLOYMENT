### Serverless Deployment using AWS S3, AWS Lambda, Amazon DynamoDB, Amazon API Gateway and Amazon CloudFront 

Configuring Amazon DynamoDB
- Create a database table name
- Create a partition key
- Create table

Configuring AWS Lambda
- Create a function to fetch data 'getStudent' select runtime as Python 3.12, copy the code from "getStudent.py", deploy code, give event name and values like:
```

```
- Create a function to post data 'insertStudent' select runtime as Python 3.12, copy the code from "insertStudent.py", deploy code

Configuring Amazon API Gateway
- Create a REST API 
- Create two methods 'get' and 'post' respectively and select integration with Lambda and select Functions accordingly
- Create a stage "PROD"
- Enable CORS
- Deploy API
- Find and copy invoke URL: paste the URL in API_ENDPOINT of "Script.js"

Configuring Amazon S3 bucket
- Create a bucket
- Enable Static website hosting
- Allow Public access and update the bucket policy (In case without using CloudFront, CloudFront will incur charges, CloudFront is suggested for enhanced security, to eliminate public access to your bucket for security concerns)
- Upload "index.html" and "script.js" files
- Copy the Static website URL and hit it on the browser to view your website hosted !!
  
