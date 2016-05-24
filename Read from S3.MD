Prerequisites: 
- EC2 must have at least read access to s3 bucket 


1. Log into RStudio Server as user 

2. Select 'Tools' and 'Shell' 

3. Show all files currenty in the bucket (replace bucket name  with your bucket)

`aws s3 ls s3://{bucket}`

4. execute in bash

`aws s3 cp s3://{bucket}/{filename} {local.filename}`
