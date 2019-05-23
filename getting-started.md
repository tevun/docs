---
description: After Tevun is installed and configured in your server we can go ahead
---

# Getting started

## Host operations

These operations are performed on the server. They allow you to configure the projects and repositories that will be used by the team.

### Create a new project

```text
tevun create <project> <template>
```

This command will add a new project in projects directory. Where `<project>` is the name of project and `<template>` can be **php** or **html**. We can add other templates too. The main idea is to have skeletons to most common structures used.

```text
tevun create site.com html
```

In this example Tevun will create `site.com` project, initialize a git remote repository, configure `post-receive`, generate a `docker-compose.yml` and show the git remote URL in terminal.

![](.gitbook/assets/image%20%284%29.png)

### **Destroy a project**

```text
tevun destroy <project>
```

The command destroy will stop your docker-compose project and erase the project directory.

{% hint style="danger" %}
The command will not erase the docker volumes, but is important to be careful with this instruction.
{% endhint %}

### Register users

Once the projects have been created we can make a local clone of them, but for that we need an user with access permission. To register users in Tevun use the command below:

```text
tevun register <user>
```

This is a short hand to http basic auth and the file with permissions is in file `/etc/nginx/.users` of _tevun_ container.

![](.gitbook/assets/image%20%2810%29.png)

## Using in a workstation

After having a project created on the server we can use git to publish it and even use the sample project as the basis for working on it.

### Configure in a new project

Clone the host created in your Tevun server:

```text
git clone https://<user>@<host>:<port>/<project>/repo <project>
```

Fetch the setup branch, get setup branch from remote and merge setup branch to your local branch:

```text
git fetch deploy +refs/heads/setup:refs/remotes/deploy/setup && \
git branch --track setup refs/remotes/deploy/setup && \
git merge --no-ff deploy/setup --allow-unrelated-histories
```

### **Configure in an existing project**

If you already has a project can make something like the previous section. We can get the branch setup of project repository to get the files to configure our project to run in Tevun.

Add the remote to your local repository:

```text
git remote add deploy https://<user>@<host>:<port>/<project>/repo
```

Fetch the setup branch, get setup branch from remote and merge setup branch to your local branch:

```text
git fetch deploy +refs/heads/setup:refs/remotes/deploy/setup && \
git branch --track setup refs/remotes/deploy/setup && \
git merge --no-ff deploy/setup --allow-unrelated-histories
```

