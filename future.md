---
layout: page
title: Titan Future
---

# Titan Future

Titan is a young community, and as such there are plenty of rough edges and
potential ideas. We're excited to build our future together as a community.
Here you'll find some of the larger themes that loom large in our future, but
it's just a start. Come join the [community](/community) to help on these
ideas or contribute new ones!

## Robust Remote Providers

The current remote providers, SSH and S3, are very basic and designed to be
usable without any additional software. As such, they will not scale to any
reasonable number of commits, and are not particularly secure or robust. We
believe that it's possible to create a robust remote provider, but it requires
external software and can't simply operation on existing file services.

## Multi Container Repositories

Docker compose is a common way to describe an application and its dependencies,
including data containers. It's also a way to describe a multi-container
deployment such as those found in distributed systems. Similarly, Kubernetes
supports a variety of ways to describe pods and deployments consisting of
multiple containers. This work adds first-class support for multiple containers,
for both docker-compose and Kubernetes.

## Auxiliary Data

Data is often accompanied by artifacts such as Jupyter notebooks, SQL scripts,
or test results. In addition to tagging, it would be nice to be able to
commit external data alongside the structured data so you can always get back
to the right artifacts if needed.
