---
layout: page
title: Getting Started
---

# Installation

Titan runs on any Windows or MacOS system with [Docker
Desktop](https://www.docker.com/products/docker-desktop) installed and
configured to run Linux containers. If you can run `docker run --rm
busybox:latest echo hello`, then you're good to go. If you are using a Linux
system, consult the [Documentation](/docs) to determine if your distribution is
supported.

Once you have docker configured and running, you will need to head to the
[download page](/download) or grab the archive here:
[MacOS]({{ site.data.download.macos }}),
[Windows]({{ site.data.download.windows }}),
[Linux]({{ site.data.download.linux }}). When you extract the archive,
you will have a single `titan` binary that you should place in your path
(such as `/usr/local/bin`). From there, you can run:

```
$ titan install
```

This will download and configure the titan server container that provides the
storage capabilities required for Titan. This requires connectivity to docker
hub - if you are working behind a firewall consult the [Documentation](/docs)
for more information. Part of this also involves installing ZFS on the
Docker VM or Linux host. If you are using an unsupported Linux distribution,
or a bleeding edge Docker Desktop build, you may find that it has to build
a custom distribution and may fail outright. Reach out to the
[community](/community) for assistance.

# Cloning Your First Repo

If you have any AWS credentials, you can access public titan demos hosted on
S3 buckets. If you don't have AWS credentials, skip down to the
(creating a new repository)[#creating-a-new-repository] section. AWS
credentials are configured through the standard means (environment variables
or `.aws` config files). We can launch a postgres database simply by cloning
this demo repository:

```
$ titan clone s3://titan-data-demo/hello-world/postgres hello-world
```

You should now be able to see a repository running:

```
$ titan ls
CONTAINER             STATUS
hello-world           running
```

If the container fails to start, it may be because you already have PosgreSQL
running on port `5432`, in which case you will need to stop the database, `titan
rm hello-world`, and try cloning again. If you have the PosgreSQL tools
installed, you can verify the contents:

```
$ psql postgres://postgres:postgres@localhost/postgres -t -c 'SELECT * FROM messages;'
 Hello, World!
```

If you don't have PostgreSQL tools, you can also run the DynamoDB example:

```
$ titan clone s3://titan-data-demo/hello-world/dynamodb hello-world
$ aws dynamodb scan --endpoint http://localhost:8000 --table-name messages | jq -r '.Items[0].message.S'
Hello, World!
```

# Creating a New Repository

If you want to start your own database, you can do so with `titan run`, which
run any stateful docker image with a `VOLUME` declaration, such as MongoDB. The
arguments after `--` are standard docker arguments, and must include `-d` and
`--name`.

```
$ titan run -- --name mongo -p 27017:27017 -d mongo:latest
```

# Committing and Checking out State

Using the mongo repository we created in the last step, let's add some data:

```
$ mongo --quiet --eval 'db.employees.insert({firstName:"Ada",lastName:"Lovelace"})'
```

And commit that state:

```
$ titan commit -m "First Employee" mongo
Commit b040cfe3-aae5-42b2-a41c-6fe2e2baad1c
```

Now, even if we add more data:

```
$ mongo --quiet --eval 'db.employees.insert({firstName:"Grace",lastName:"Hopper"})'
WriteResult({ "nInserted" : 1 })
$ mongo --quiet --eval 'db.employees.find()'
{ "_id" : ObjectId("5d88d264302cca22a91cfb9a"), "firstName" : "Ada", "lastName" : "Lovelace" }
{ "_id" : ObjectId("5d88d2f897a6f34e91e46f0d"), "firstName" : "Grace", "lastName" : "Hopper" }
```

We can checkout or previous state:

```
$ titan checkout --commit b040cfe3-aae5-42b2-a41c-6fe2e2baad1c mongo
$ mongo --quiet --eval 'db.employees.find()'
{ "_id" : ObjectId("5d88d264302cca22a91cfb9a"), "firstName" : "Ada", "lastName" : "Lovelace" }
```

# Additional Workflows

With just these simple tools, you can start create and manage data state to
match your workflow. Want to keep a blank database with your schema pre-applied?
Want to keep some sample data available for you to do destructive testing?
Have a failing test and want to keep the data state around to debug later? Titan
lets developers work with the data they need, when they need it, all on their
laptop environment.

For more information on pushing and pulling data from remote repositories,
more complex workflows to migrate data from existing containers and filesystems,
and a complete breakdown of command line features, see the
[documentation](/docs).

Titan is still a young community, and there are plenty of rough edges and future
ideas in store. Head over the [future](/future) section to learn more about
what's in store.