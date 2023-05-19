# Maven Installation
After installing Jenkins, in the same server we are going to install Maven. To run Maven we need Java. But as we already installed Java for Jenkins we can directly install Maven.
## Install Maven - Ubuntu 22.04
### Step 1: Download the Maven Binaries
Go to the URL: https://maven.apache.org/download.cgi Copy the link for the “Binary tar.gz archive” file. Then run the following commands to download and untar it.
```sh
$ cd /opt
$ wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
$ tar -xvf apache-maven-3.6.3-bin.tar.gz
$ mv apache-maven-3.6.3 maven
```
### Step 2: Setting M2_HOME and Path Variables
```sh
$ cd ~
$ vim .profile
```
Add the following lines to the user profile file (.profile).
```sh
M2_HOME='/opt/maven'
PATH="$M2_HOME/bin:$PATH"
export PATH
```
Relaunch the terminal or execute source .profile to apply the changes.
```sh
$ source .profile
```
### Step 3: Verify the Maven installation
You should get a out put similar to following, but versions can be different. 
```sh
$ mvn -version
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /opt/apache-maven-3.6.3
Java version: 13.0.1, vendor: Oracle Corporation, runtime: /opt/jdk-13.0.1
Default locale: en, platform encoding: UTF-8
OS name: "linux", version: "4.15.0-47-generic", arch: "amd64", family: "unix"
$
```
So far we have completed the installation of maven software to support maven plugin on the jenkins console. Let's jump onto Jenkins to complete the remaining steps.
## Setup maven on Jenkins console

   ### Install maven plugin without restart

    Manage Jenkins > Jenkins Plugins > available > Maven Invoker
    Manage Jenkins > Jenkins Plugins > available > Maven Integration

    Configure maven path

    Manage Jenkins > Global Tool Configuration > Maven
