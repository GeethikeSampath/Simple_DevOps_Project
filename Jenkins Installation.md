# Simple_DevOps_Project
How to create simple CI/CD project with Jenkins,Maven,Docker and Kubernetes.
## Requirements
- Linux and Docker basics
- Github and Dockerhub basics
- Kubernetes basics
## Scenario
In this project we are going to create a simple CI/CD pipeline to deploy a java web application in Kubernetes cluster.This project can be implemented in AWS or Azure or any other cloud platforms. But here i will describe how to implement it using Virtual machines using Virtual box. So we need minimum of 5 VMs to setup the lab.
### Requiremets are as follows;

 5 VMs installed with Ubuntu 22.04 server Operating system.
 - One VM for Jenkin and maven.
 - One VM for Ansible.
 - One  VM for Kubernetes Master.
 - Two VMs as Kubernetes Worker nodes.
### install Jenkins in Ubuntu 22.04
Before we install Jenkins we need install Java.
##### Installing Java

```sh
$ sudo apt update -y
$ sudo apt install default-jre -y
$ sudo apt install default-jdk -y
```
Verify the installation with:
```sh
$ java -version
$ javac -version
```
#### Setting the JAVA_HOME Environment Variable
Many programs written using Java use the JAVA_HOME environment variable to determine the Java installation location.
In this case the installation paths are as follows:
- OpenJDK 11 is located at **/usr/lib/jvm/java-11-openjdk-amd64/bin/java**

Then open **/etc/environment** using vim or your favorite text editor:
```sh
$ sudo vim /etc/environment
```
At the end of this file, add the following line, making sure to replace the highlighted path with your own copied path, but **do not include the bin/ portion** of the path:
```sh
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```
Modifying this file will set the JAVA_HOME path for all users on your system.
Save the file and exit the editor.
Now reload this file to apply the changes to your current session:
```sh
$ source /etc/environment
```
Verify that the environment variable is set:
```sh
$ echo $JAVA_HOME
```
You’ll see the path you just set:
```sh
Output
/usr/lib/jvm/java-11-openjdk-amd64
```
Other users will need to execute the command **source /etc/environment** or **log out and log back** in to apply this setting.
### Jenkins Installation
First, add the repository key to the system:
```sh
$ curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```
Next, let’s append the Debian package repository address to the server’s sources.list:
```sh
$ echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```
After both commands have been entered, we’ll run update so that apt will use the new repository.
```sh
$ sudo apt update
```
Finally, we’ll install Jenkins and its dependencies.
```sh
$ sudo apt install jenkins
```
Now that Jenkins and its dependencies are in place, we’ll start the Jenkins server.
```sh
$ sudo systemctl start jenkins
$ sudo systemctl enable jenkins
```
Since systemctl doesn’t display status output, we’ll use the status command to verify that Jenkins started successfully:
```sh
$ sudo systemctl status jenkins
```
You should get out put as follows;
```sh
Output
● jenkins.service - Jenkins Continuous Integration Server
     Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2022-04-18 16:07:28 UTC; 2min 3s ago
   Main PID: 88180 (java)
      Tasks: 42 (limit: 4665)
     Memory: 1.1G
        CPU: 46.997s
     CGroup: /system.slice/jenkins.service
             └─88180 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080
```
To set up your installation, visit Jenkins on its default port, 8080, using your server domain name or IP address: **http://your_server_ip_or_domain:8080**

You should receive the Unlock Jenkins screen, which displays the location of the initial password:
In the terminal window, use the cat command to display the password:
```sh
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
Copy the 32-character alphanumeric password from the terminal and paste it into the Administrator password field, then click Continue.

The next screen presents the option of installing suggested plugins or selecting specific plugins:

We’ll click the Install suggested plugins option, which will immediately begin the installation process.

When the installation is complete, you’ll be prompted to set up the first administrative user. It’s possible to skip this step and continue as admin using the initial password we used above, but we’ll take a moment to create the user.

After confirming the appropriate information, click **Save and Finish**. You’ll receive a confirmation page confirming that **“Jenkins is Ready!”:**
