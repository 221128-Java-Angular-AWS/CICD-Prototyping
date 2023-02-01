## new server
following the basics from here:  
https://ravivalecha30.medium.com/continuous-integration-and-deployment-of-angular-application-using-jenkins-on-aws-ec2-19de3e3c7f3b  

installing node via nvm instead, according to:  
https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html  
  
skipped installing pm2. May need to come back to this?

  
  
### install java jdk
sudo yum install java-17-amazon-corretto-devel  

### install jenkins
https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/  

### set the java home variable 
May need to export this variable as well as PATH during the build, or maybe there are ENV options in jenkins config  
https://bhargavamin.com/how-to-do/setting-up-java-environment-variable-on-ec2/  
  
location:
/usr/lib/jvm/java-17-amazon-corretto.x86_64/bin  
set java home in jenkins config  
  
### Install git
sudo yum install git  
set git location in jenkins config  

### Install maven - installs v3.5.2
https://docs.aws.amazon.com/neptune/latest/userguide/iam-auth-connect-prerq.html  
 - sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
 - sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
 - sudo yum install -y apache-maven

### Install docker - create boot service - fix groups so no sudo necessary  
https://www.cyberciti.biz/faq/how-to-install-docker-on-amazon-linux-2/  
sudo yum install docker  
sudo usermod -a -G docker jenkins  
newgrp docker  
sudo systemctl enable docker.service  
sudo systemctl start docker.service  
  
  
### installing node
https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html  
sudo yum install -y gcc-c++ make - is this necessary?  
may need to perform these steps during build?
 - curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
 - . ~/.nvm/nvm.sh
 - nvm install 16

checking locations:
`which node`: /home/ec2-user/.nvm/versions/node/v16.19.0/bin/node  
  
`which npm`: /home/ec2-user/.nvm/versions/node/v16.19.0/bin/npm  
symlink to: /home/ec2-user/.nvm/versions/node/v16.19.0/lib/node_modules/npm/bin/npm-cli.js  
  
node version: `node -e "console.log('Running Node.js ' + process.version)"  `
 - Running Node.js v16.19.0
  
install node plugin in jenkins - Manage Jenkins > Jenkins Plugins > available > NodeJs Plugin  
Configure Node JS installations - Manage Jenkins > Global Tool Configuration > NodeJs Installations  
Guide at this point instructs us to install automatically, but didn;t we already install it? I went with install auto and selected the same node version 16.19.0


