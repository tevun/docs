---
description: >-
  to understand how Tevun works it is necessary to understand what pieces it
  joins and how they fit together.
---

# How it works

## Glossary

### Docker

Docker is a computer program that performs operating-system-level virtualization. With `docker` we can run services in the same kernel as containers.

### Docker Compose

Compose is a tool for defining and running multi-container Docker applications. Using `docker-compose` it is possible describe the services in an yaml file and Compose will manage the containers.

### Git

Git is a distributed version-control system for tracking changes in source code during software development. It will be used to handle the base code and make the new changes available.

### Git Hooks

Git hooks are scripts that Git executes before or after events such as: commit, push, and receive. Git hooks are a built-in feature - no need to download anything. Git hooks are run locally. In Tevun we configure the post receive-hook when you create a new project to receive push and deploy the code.

