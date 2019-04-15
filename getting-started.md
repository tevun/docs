---
description: After Tevun is installed and configured in your server we can go ahead
---

# Getting started

## Prepare environment

Before start the usage you can edit the .env file to configure the properties of your server.Open the .env file with your favorite editor and change the properties to suit your needs.  

```
$ nano .env
```

![](.gitbook/assets/image%20%284%29.png)

Make sure you use the appropriate settings

## Create a new project

```text
$ tevun create <project> <template>
```

This command will add a new project in projects directory. Where `<project>` is the name of project and `<template>` can be **php** or **html**. We can add other templates too. The main idea is to have skeletons to most common structures used.

```text
$ tevun create site.com html
```

In this example Tevun will create `site.com` project, initialize a git remote repository, configure `post-receive`, generate a `docker-compose.yml` and show the git remote URL in terminal.

![](.gitbook/assets/image%20%285%29.png)

## Register users

Once the projects have been created we can make a local clone of them, but for that we need an user with access permission. To register users in Tevun use the command below:

```text
$ tevun register <user>
```

This is a short hand to http basic auth and the file with permissions is in file `/etc/nginx/.users` of _tevun_ container.

![](.gitbook/assets/image%20%286%29.png)

## Starting a new project

Clone your repo:

```text
$ git clone https://<user>@<host>:8110/<project>/repo <project>
```

Fetch the setup branch:

```text
$ git fetch deploy +refs/heads/setup:refs/remotes/deploy/setup
```

Get setup branch from remote:

```text
$ git branch --track setup refs/remotes/deploy/setup
```

Merge setup branch to your local branch:

```text
$ git merge --no-ff deploy/setup --allow-unrelated-histories
```

## **Configure in an existing project**

If you already has a project can make something like the previous section. We can get the branch setup of project repository to get the files to configure our project to run in Tevun.

Add the remote to your repo:

```text
$ git remote add deploy https://<user>@<host>:8110/<project>/repo
```

Fetch the setup branch:

```text
$ git fetch deploy +refs/heads/setup:refs/remotes/deploy/setup
```

Get setup branch from remote:

```text
$ git branch --track setup refs/remotes/deploy/setup
```

Merge setup branch to your local branch:

```text
$ git merge --no-ff deploy/setup --allow-unrelated-histories
```

## **Destroy a project**

```text
$ tevun destroy <project>
```

The command destroy will stop your docker-compose project and erase the project directory.

{% hint style="danger" %}
The command will not erase the docker volumes, but is important to be careful with this instruction.
{% endhint %}

