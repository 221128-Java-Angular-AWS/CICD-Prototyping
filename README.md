# CICD-Prototyping
This is a repo for documentation and collaboration in establishing a prototype for future P3 CICD pipelines

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
