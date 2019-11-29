# docker_python_sshd
Dockerized Python with SSH service, built on top of [official Python](https://hub.docker.com/_/python/) images.

## Image tags

- oscar86hsu/python_sshd:3.8
- oscar86hsu/python_sshd:3.7
- oscar86hsu/python_sshd:3.6
- oscar86hsu/python_sshd:2.7

## Installed packages

Base:

- [Python3.8](https://www.python.org/downloads/release/python-380/)
- [Python3.7](https://www.python.org/downloads/release/python-375/)
- [Python3.6](https://www.python.org/downloads/release/python-369/)
- [Python2.7](https://www.python.org/downloads/release/python-2717/)

Package:

- [openssh-server](https://packages.debian.org/zh-tw/jessie/openssh-server)

Default Config:

- `PermitRootLogin yes`
- `PasswordAuthentication yes`
- exposed port 22
- default command: `/usr/sbin/sshd -D`
- root password: `root`

## Getting Started
`docker run -d -p 2222:22 --name python_sshd oscar86hsu/python_sshd:latest`<br>
`ssh root@localhost -p2222`

## Security

Using the image with the default password is dangerous. You should change your password after creating the container.<br>
- To change password, use the following command:
`docker exec -ti python_sshd passwd`

- To not use password and use key instead:<br>
```
docker exec python_sshd passwd -d root
ssh-keygen -t rsa -f ./id_rsa -N ""
docker cp id_rsa.pub python_sshd:/root/.ssh/authorized_keys
docker exec python_sshd chown root:root /root/.ssh/authorized_keys
```

## Useful Links
- [ssh-keygen](https://www.ssh.com/ssh/keygen/)
- [Docker Document](https://docs.docker.com/)


