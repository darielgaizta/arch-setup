# Setup Docker on Arch

## 1. Install
```
sudo pacman -S docker
```

## 2. Activate daemon
```
sudo systemctl start docker
```

**Q: What is daemon?**

Basically, working with Docker introduces you to two main components: **Docker Client** and **Docker Daemon**. Docker client is just for user interface, whereas daemon is a background process that controls everything. Their relationship is just like a client-server architecture.

## 3. Register your Linux user to Docker
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

Initially, you cannot run Docker commands, such as `docker ps` or `docker info`, because Docker requires you to grant access to the daemon via a Unix group named "docker" (reference: https://docs.docker.com/engine/install/linux-postinstall/). If you are too lazy to create a Unix group, you can just add sudo in every command. Don't forget to re-login after running the command, or maybe you want to try to run the following command to apply the group immediately:
```
newgrp docker
```