# Integrate git with Jenkins
Now we look at how to integrate git with Jenkins. First we need to install git.
## install git - Ubuntu 22.04
```sh
$ sudo apt update
$ sudo apt install git -y
```
You can confirm that you have installed Git correctly by running the following command and checking that you receive relevant output.
```sh
git --version
```
## Configure Git pulgin on Jenkins

Git is one of the most popular tools for version control system. you can pull code from git repositories using jenkins if you use github plugin.
Prerequisites

    Jenkins server

Setup Git on jenkins console

    Install git plugin without restart
        Manage Jenkins > Jenkins Plugins > available > github

    Configure git path
        Manage Jenkins > Global Tool Configuration > git
