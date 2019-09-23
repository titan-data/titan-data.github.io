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

## Improved Error Handling

Titan works well in the so-called "happy path". As you start to make mistakes
or deal with unexpected events (such as network failure), the behavior
typically leaves something to be desired. This work includes making clear,
crisp error messages, eliminating the need to consult docker logs to diagnose
problems, automatic push/pull retry, better progress monitoring, and more.

## Docker Configuration Management

Currently, titan sets the docker configuration when a repository is created,
and propagates that information with every commit. But this means that every
clone of that repository must run in exactly the same fashion, down to the
port mapping and exact image version used. If you want to run in a configuration
specific to your machine or with a slightly different version, you're out of
luck. This work would adds the ability to set and manage the docker configuration
of an existing repository, with local overrides and conflict resolution.

## Branches and Tags

While being able to create and checkout commits is great, we know that once
you get past a few commits you start to need a way to help organize and find
your work. Simply searching through commit history doesn't cut it. This work
adds the ability to tag commits locally and remotely, and to leverage tags
to create branches that make it easy to find the latest version of a known
data state.

## Robust Remote Providers

The current remote providers, SSH and S3, are very basic and designed to be
usable without any additional software. As such, they will not scale to any
reasonable number of commits, and are not particularly secure or robust. We
believe that it's possible to create a robust remote provider, but it requires
external software and can't simply operation on existing file services.

## Docker Compose

Docker compose is a common way to describe an application and its dependencies,
including data containers. It's also a way to describe a multi-container
deployment such as those found in distributed systems. This work adds
first-class docker compose support, with the ability to run multi-container
repositories under Titan.

## Auxiliary Data

Data is often accompanied by artifacts such as Jupyter notebooks, SQL scripts,
or test results. In addition to tagging, it would be nice to be able to
commit external data alongside the structured data so you can always get back
to the right artifacts if needed.

## Kubernetes

Docker is an extremely convenient tool for running containers on your laptop,
but Kubernetes is becoming increasingly important in both production and
non-production environments, such as CI/CD infrastructure. This work adds the
ability to create Kubernetes-based Titan repositories.
