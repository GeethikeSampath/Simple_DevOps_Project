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
