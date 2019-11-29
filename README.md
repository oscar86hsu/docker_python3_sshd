# docker_python3_sshd
Dockerized SSH service, built on top of [official Python](https://hub.docker.com/_/python/) images. Login using ssh key.

## Image tags

- oscar86hsu/docker_python3_sshd:3.8
- oscar86hsu/docker_python3_sshd:3.7
- oscar86hsu/docker_python3_sshd:3.6
- oscar86hsu/docker_python3_sshd:2.7

## Installed packages

Base:

- [Python3.8](https://github.com/docker-library/python/blob/0b1fb9529c79ea85b8c80ff3dd85a32a935b0346/3.8/buster/Dockerfile)

Package:

- [openssh-server](https://packages.debian.org/zh-tw/jessie/openssh-server)

Default Config:

- `PermitRootLogin yes`
- `PasswordAuthentication yes`
- exposed port 22
- default command: `/usr/sbin/sshd -D`
- root password: `root`

## Getting Started
`docker run -d -p 2222:22 --name python3_sshd oscar86hsu/docker_python3_sshd:latest`<br>
`ssh root@localhost -p2222`

## Security

Using the image with the default password is dangerous. You should change your password after creating the container.<br>
- To change password, use the following command:
`docker exec -ti python3_sshd passwd`

- To not use password and use key instead:<br>
```
docker exec python3_sshd passwd -d root
ssh-keygen -t rsa -f ./id_rsa -N ""
docker cp id_rsa.pub python3_sshd:/root/.ssh/authorized_keys
docker exec python3_sshd chown root:root /root/.ssh/authorized_keys
```

## Useful Links
- [ssh-keygen](https://www.ssh.com/ssh/keygen/)
- [Docker Document](https://docs.docker.com/)


