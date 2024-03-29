# An Article/Guide on how To Install Jenkins on an EC2 Instance

https://medium.com/@TheCloudLord/an-article-guide-on-how-to-install-jenkins-on-an-ec2-instance-53965a9fc33f
![image](https://user-images.githubusercontent.com/60587384/145048143-c8137134-611d-4536-bf42-5a5aabd48afa.png)

Jenkins is known as an  open-source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.

## What You will Need:

* An AWS Account
* Security group with port 8080 opened
* Java SDK 11
* Jenkins installer
* PUttY App (This will be used to connect to our Instance)
* An Internet connection
* And my Guide (lol)

## Setting up an EC2 Instance

* Login to your AWS account
* Search for EC2 in the search pane
* Go to “Instances”
* At the top right corner, click on ‘Launch Instance”
* Leave configurations as default till you get to the Tag section, you can type in Name: Jenkins_Server
* Next is the security group, remember this server should be accessible over the internet and port 8080 should also be accessible. By default, port 22 is included in our security group which allows access over the internet, but to allow access to port 8080,

```Click on “Add rule” -> Set Protocol to TCP -> Set Port to 8080```

* Then Review and Launch Instance
* You can Download existing or Create a new key pair if you don’t have one already. This will be used to SSH (i.e Connect) into our Instance.

# To Connect (SSH) into our Instance

* Download and Install PuTTY App here : https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

* First You copy your Instance’s Public IP Address paste it in the Hostname Input
* Click on “Auth” and then import your download Keypair to complete the authentication process to connect to the Instance.

![image](https://user-images.githubusercontent.com/60587384/145049275-92144fa0-f064-469f-bbed-6f102db66c4b.png)

* To go into root user, enter the command below

su ec2-user

![image](https://user-images.githubusercontent.com/60587384/145049379-26298142-4d70-4ae1-a205-dfe9ea79da96.png)

# Install Jenkins

You can install Jenkins using rpm or by setting up the repository. We will set up our repo so we can update it later.

Get the latest version of Jenkins Here: https://pkg.jenkins.io/redhat-stable/

But before installing Jenkins, we have to install our Java SDK

```amazon-linux-extras install epel ```

and then install JDK using

```amazon-linux-extras install java-openjdk11```

![image](https://user-images.githubusercontent.com/60587384/145051017-2e218309-b5d5-44ad-8eb5-c117a74d39e3.png)

Or Install using the step below

```sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
yum install epel-release # repository that provides 'daemonize'
yum install java-11-openjdk-devel
yum install jenkins
```

# Accessing Jenkins:

You can access your Jenkins by typing your EC2 ip address and the Jenkins port in your browser.

```https://YOUR-IP-ADDRESS:8080```

# Configure Jenkins:

* Default username is admin
* Get the default password from :

```/var/lib/Jenkins/secret/InitialAdminPassword```

* You can skip the PlugIn installation for now (It can be done later)
* To change the admin password to something you would remember,

```Click Admin-> Configure -> Password```

* To configure the Java path, you can do this,

```Manage Jenkins -> Global tool configuration -> SDK```

* Then lastly, Create another User

# Now to the most interesting Part!!!!

I know you can’t wait to build your first project, trust me I was as excited as you are!

To build a sample project,

* Create “New Item”
* Give it a Name e.g My First Ever Jenkins Project!!
* Click on “Freestyle Project”
* Click “Ok”
* Now, click on the “Build Section” at the top bar, type in

```echo “Welcome to my DevOps Journey!!!”```
