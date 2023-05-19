# Installing Docker on Ubuntu 22.04 server

### Pre-requisites
1. Ubuntu Linux 22.04 Instance

## Installation Steps

1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```sh 
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```
2. Add Docker’s official GPG key:
```sh
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
3. Use the following command to set up the repository:
```sh
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```
   # Install Docker Engine
   1. Update the apt package index:
   ```sh
   sudo apt-get update
   ```
   2. Install Docker Engine, containerd, and Docker Compose.
   ```sh
   sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```
   3. Start and enable docker service
   ```sh
   systemctl start docker
   systemctl enable docker
   ```
   4. Verify that the Docker Engine installation is successful by running the hello-world image.
   ```sh
   sudo docker run hello-world
   ```
   5. Create a user called dockeradmin
   ```sh
   adduser dockeradmin
   passwd dockeradmin
   ```
   6. Add a user to docker group to manage docker 
   ```sh
   usermod -aG docker dockeradmin
   ```
   7. Assign admin privilages with NO password for docker admin
   ```sh
   echo "dockeradmin  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/dockeradmin
   ```
# Basic Docker Commands

1. how to search a docker image in hub.docker.com
```sh
docker search httpd
```
2. Download a docker image from hub.docker.com
```sh
docker image pull <image_name>:<image_version/tag>
```

3. List out docker images from your local system
```sh
docker image ls
```

4. Create/run/start a docker container from image
```sh
docker run -d --name <container_Name> <image_name>:<image_version/tag>

d - run your container in back ground (detached)
```

5. Expose your application to host server
```sh
docker run -d  -p <host_port>:<container_port> --name <container_Name> <image_name>:<Image_version/tag>

docker run -d --name httpd_server -p 8080:80 httpd:2.2
```

6. List out running containers
```sh
docker ps
```

7. List out all docker container (running, stpooed, terminated, etc...)
```sh
docker ps -a
```

8. run a OS based container which interactive mode (nothing but login to container after it is up and running)

```sh
docker run -i -t --name centos_server centos:latest
i - interactive
t - Terminal
```

9. Stop a container 
```sh
docker stop <container_id>
```

10. Start a container which is in stopped or exit state

```sh
docker start <container_id>
```
11. Remove a container

```sh
docker rm <container_id>
```

12. login to a docker container
```sh
docker exec -it <container_Name> /bin/bash
```
