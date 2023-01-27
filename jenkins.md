# Jenkins
Jenkins is installed on EC2 according to the following documentation:
 - https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/
  
Notably, spin up an EC2 and install jenkins with the following commands:

```
sudo yum update –y
```

```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

```
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

```
sudo yum upgrade
```

```
sudo amazon-linux-extras install java-openjdk11 -y
```

```
sudo yum install jenkins -y
```

```
sudo systemctl enable jenkins
```

```
sudo systemctl enable jenkins
```
