Prerequisites: 
- EC2 must have at least read access to s3 bucket 

#Read from S3 
1. Log into RStudio Server as user 

2. Select 'Tools' and 'Shell' 

3. Show all files currenty in the bucket (replace bucket name  with your bucket)

`aws s3 ls s3://{bucket}`

4. execute in bash (--region if required)

`aws s3 --region us-east-1 cp s3://{bucket}/{filename} {local.filename}`

#Write to S3

`aws s3 --region us-east-1 cp {local.filename} s3://{bucket}/{filename}`
