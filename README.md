# CICD-Prototyping
This is a repo for documentation and collaboration in establishing a prototype for future P3 CICD pipelines

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
