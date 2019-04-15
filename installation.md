---
description: Simple tutorial to make your server run with Tevun
---

# Installation

## 1. Requirements

Verify that your server has the following requirements:

* Git \(git --version\): git version +2.10.x  
* Docker \(docker -v\): Docker version +18.0x.x-ce, build xxxxxxx  
* Docker Compose \(docker-compose -v\): docker-compose version +1.2x.x, build xxxxxxxxx

## 2. Download and install

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

![Output command &quot;tevun&quot; when we do not pass parameters](.gitbook/assets/image%20%2812%29.png)

## 3. Setting up Tevun

Let's configure Tevun on your server. First, let's check the user settings and permissions, and then let's configure Tevun.

## 3.1. Users and permissions

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

## 3.2. Access policy via SSH

You can use a single Tevun command to configure a less privileged user to access SSH and disable root access by using the command below.

{% hint style="danger" %}
Just use it if you know what it's doing!
{% endhint %}

```text
# tevun ssh <name>
```

## 3.3. Tevun setup

To perform the setup use the following command in the terminal, replacing &lt;user&gt; with the name of the user that will be used to manipulate the containers.

```text
# tevun setup <user>
```

![](.gitbook/assets/image%20%284%29.png)

After perform this command you can access the your server in port 8110 to see if it works.

![](.gitbook/assets/image%20%282%29.png)

## 3.4. What happens in my server?

Setup command will create 3 containers:

* [nginx-proxy](https://github.com/jwilder/nginx-proxy): a nginx instance to make the reverse proxy and allow we up various containers to the same port
* [nginx-letsencrypt](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion): a listener to docker socket that run LetsEncrypt bot to VIRTUAL\_HOST property of containers environment
* [tevun](https://github.com/tevun/server/blob/master/.docker/tevun/Dockerfile): nginx server configured to run CGI and communicate with docker of host

> If you are here and is all right you can start creating projects your server!
>
> In case you got issues in this process keep in touch. You can open issues in our [repo](https://github.com/tevun/server) or call in [telegram](https://t.me/tevun) = \)

