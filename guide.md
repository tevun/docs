---
description: Simple tutorial to make your server run Tevun
---

# Getting Started

### Requirements

Verify that your server has the following requirements:  
- Git \(git --version\): git version +2.10.x  
- Docker \(docker -v\): Docker version +18.0x.x-ce, build xxxxxxx  
- Docker Compose \(docker-compose -v\): docker-compose version +1.2x.x, build xxxxxxxxx

### Download and install

Access your server using ssh

```text
$ ssh root@<server>
```

Then create the installation dir, clone repository and create the symlink to use command `tevun` in terminal

```text
# mkdir -p /usr/share/tevun
# git clone https://github.com/tevun/server.git /usr/share/tevun
# ln -s $(pwd)/tevun.sh /usr/bin/tevun
```

Now we can perform `tevun` in terminal.

![Output command &quot;tevun&quot; when we do not pass parameters](.gitbook/assets/image%20%281%29.png)

### Setting up Tevun

Let's configure Tevun on your server. First, let's check the user settings and permissions, and then let's configure Tevun.

#### Users and permissions

{% hint style="info" %}
if you already have an user with the necessary permissions to run your containers or this is not relevant to your scenario you can just disregard this topic.
{% endhint %}

It is important that you avoid using your root user via SSH. It is recommended that you create an user that is limited in order to be able to access your server via SSH. Since we are dealing with docker, we need to have a local user with the same UID that the images will use. Usually this **UID** is the _1000_. To facilitate this operation you can **optionally** use the command below, where `<name>` is the name you want to assign to the new user.

```text
# tevun user <name>
```

{% hint style="warning" %}
This command will also add the new user to the docker group and sudoers group
{% endhint %}



