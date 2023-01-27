# CICD-Prototyping
This is a repo for documentation and collaboration in establishing a prototype for future P3 CICD pipelines

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
 - Need to install docker, docker commands must be run as a sudoer
   - sudo yum install docker
 - I think we also need to install git in addition to the git jenkins addon
   - sudo yum install git
   
[Install mvn] https://awswithatiq.com/how-to-install-apache-maven-on-amazon-linux-2/
sudo yum update -y
sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
sudo yum install -y apache-maven

[Install angular and npm] https://www.geeksforgeeks.org/how-to-install-angularjs-on-linux/
sudo apt-get upgrade && sudo apt-get update -y
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
. ~/.nvm/nvm.sh
nvm install 16
node -e "console.log('Running Node.js ' + process.version)"
sudo apt install nodejs
sudo ln -s /usr/bin/nodejs /usr/bin/node
sudo apt install npm -y
sudo npm install -g @angular/cli


[If using v18]
npm use 16.x.x

Steps after launching EC2 with Amazon Linux image:
sudo nano /etc/sudoers
[append "jenkins ALL=(ALL) NOPASSWD: ALL" to the end of the text-file]

sudo yum update
sudo yum install docker
sudo systemctl start docker
sudo docker pull username/img:tagname
sudo docker run -p {}:{} imgname

[If getting compatability err, ex. arm64 incompatability issue]:
sudo docker run --privileged --rm tonistiigi/binfmt --install all
sudo docker run --platform linux/arm64 -p p1:p2 username/img:tagname

[Install npm and maven]

[To install jenkins on EC2 instance]:
sudo yum update -y
sudo wget -O /etc/yum.repos.d/jenkins.repo     https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum upgrade
sudo amazon-linux-extras install java-openjdk11 -y
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

Head to {EC2 IPV4 address}:8080 on browser to sign up for Jenkins.
If unable to connect, add Custom security protocol for port 8080 on instance from any IP address (0.0.0.0/0)

In configuring git settings in Jenkins, add repository name and use */deploy under branch specifier to trigger pipeline whenever a push is made to the deploy branch*

On github, go to your repository: Settings: Webhooks: Add webhook
Get your url:port and append /github-webhook/
