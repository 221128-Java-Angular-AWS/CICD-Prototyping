# CICD-Prototyping
This is a repo for documentation and collaboration in establishing a prototype for future P3 CICD pipelines  
Account: EC2-User  
Password: none  
You need the private key file to access.  
ec2-3-133-147-18.us-east-2.compute.amazonaws.com


## Design:
 - T2 Medium EC2, necessary as micro and small frequently crash during build.
 - 2 S3 buckets, one for static site hosting, the other for files like application.properties
 - If we have multiple pipelines in parallel we can merge the EC2 and secret buckets
 - Need an RDS for persistence, should probably decide on a standard flavor. Postgre is widely used in training and allows us to split the db into schemas, one for each project.
 - Need IAM role to grant permission for the EC2 to run aws s3 cp commands.
 - Need two bucket policies for the two buckets.

## Plan:
 - Jenkins runs on EC2, as do APIs. Need to open a block of ports if we will have multiple webservers running.
 - Build with a freestyle project
 - APIs run in docker containers on the same EC2 where jenkins runs
 - we deploy the SPA to the static site bucket
 - during build we copy the properties file from the secret bucket.

## Blockers:
 - In our shared AWS account management has been reticent to consider setting up resources the associates can access directly for hands-on experience. Our own accounts are also very limited in what we can create and modify. Trainers are generally unable to create a fully working pipeline with jenkins due to security and interoperability limitations. Once we can identify the exact needs for a simple pipeline as described above, we can run this past experts to make sure it is stable, secure, and good practice.
 - We should allow associates access to the EC2 server. This might be a bit of a pain, and we might not be able to offer sudo access. We would probably have to partially automate creation of accounts, and would still require a bit of human monitoring. This is probably going to be the biggest pain point.


## Status:
 - Prototype in progress - 221128-Java-Angular-AWS is on P3, devops lead is working with trainer to build the prototype on trainer's account.

## Notes:
 - Need jenkins account to be sudoer on EC2
 - Could use a dynamic DNS, maybe free no-ip? Backend location is likely to change, especially if multiple teams are using it. Restarts generate new public address.
Need



