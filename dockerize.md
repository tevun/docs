---
description: Bash like abstraction of local services in docker
---

# Dockerize

When assuming the use of container in our workflow we come to face some challenges. Soon we realize that it is complicated to have a complete environment without installing any tool on the host.

[Tevun's Dockerize](https://github.com/tevun/dockerize) initiative seeks to deliver a comfortable workflow for those who use Docker in their day-to-day lives.

Using it you will abstract all the services you use to develop to run with docker.

## How to configure

{% hint style="danger" %}
Read the steps before you run them to understand what is being done. We will modify your bash environment and we don't want cause problems to you = \)
{% endhint %}

### Getting started

To use dockerize you can clone or download de zip of project from Github.

#### Create a clone

Position your terminal in an easy-to-find folder

```text
$ cd ~
```

Make a local project clone

```text
$ mkdir tevun
$ cd tevun
$ git clone git@github.com:tevun/dockerize.git dockerize-master
```

OR

#### Download

Download the zip of this project

```text
 $ wget -O dockerize.zip https://codeload.github.com/tevun/dockerize/zip/master
```

Then unzip the contents of the zip

```text
$ unzip dockerize.zip -d tevun
```

## Configuration

If you are using the project for the first time you can use our convenient configuration script to add local documents to your terminal environment.

To do this, run the configuration script

```text
$ cd tevun/dockerize-master
$ ./configure.sh
```

### How to use Dockerize

will create a command engine to toggle service commands to run on global images and / or images relative to the project of the folder it is in.

We currently have the following configured services:

* artisan
* composer
* node
* npm
* php
* phpunit
* quasar
* vue
* yarn

In other words, you can simply execute:

```text
$ php -v
```

To perform the service php in your docker host.

### Smart behavior

Dockerize tries to detect which container should be run for each service. When you are in a folder that does not have a container associated with it, your output will be global.

![](.gitbook/assets/image%20%287%29.png)

When the current directory is associated with one container the output will be different.

![](.gitbook/assets/image%20%2814%29.png)

### Detection strategies

* global suffix: Dockerize will first attempt to find a container that has the folder name and suffix associated with the service. You can check the service suffix in the property `T_DOCKERIZE_SERVICE` of file `dockerize/environment/variables.ini.sample`. If your project folder is `foo` and `T_DOCKERIZE_SERVICE` is `app` the name of your service must be `foo-app` to this detection match. 
* service suffix: The second try is check if there is a container with the folder name followed by an hyphen and the name of service. If your project folder is `acme` and you create a service with name `acme-node` you can perform the command `node` and dockerize will use this container.
* file .dockerize: You create a file called .dockerize in your project folder and describe the name of containers of services.

## Customizing

You can customize the main project settings. Go to the environment folder and evaluate the parameters that are defined there.

```text
$ cd ~/.config/tevun/dockerize/environment
```

## Common Problems

* **Address already in use:** 
  * **message**: docker: Error response from daemon: driver failed programming external connectivity on endpoint \* \(\): Error starting userland proxy: listen tcp 0.0.0.0:: bind: address already in use.
  * **solution**: use the guidelines in the Customizing section and configure the ports in the images.ini file according to your port usage.

\*\*\*\*

