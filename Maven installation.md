# Maven Installation
After installing Jenkins, in the same server we are going to install Maven. To run Maven we need Java. But as we already installed Java for Jenkins we can directly install Maven.
## Install Maven - Ubuntu 22.04
### Step 1: Download the Maven Binaries
Go to the URL: https://maven.apache.org/download.cgi Copy the link for the “Binary tar.gz archive” file. Then run the following commands to download and untar it.
```sh
$ wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
$ tar -xvf apache-maven-3.6.3-bin.tar.gz
$ mv apache-maven-3.6.3 /opt/
```
