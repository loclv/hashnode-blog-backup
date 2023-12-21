---
title: "The minimal version of get started with mongodb 🌱 local development"
seoTitle: "The minimal version of get started with mongodb 🌱 local development"
seoDescription: "The minimal version of get started with mongodb 🌱 local development"
datePublished: Thu Dec 21 2023 11:42:15 GMT+0000 (Coordinated Universal Time)
cuid: clqf4ut5t000z08jyb08ca6x5
slug: the-minimal-version-of-get-started-with-mongodb-local-development
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/QY9LOl9eZ9w/upload/6cf17655ce8cf47a1d494acdf65184bb.jpeg
tags: mongodb

---

## Reference

* [https://www.prisma.io/dataguide/mongodb/connecting-to-mongodb#connecting-to-a-local-database-with-mongo](https://www.prisma.io/dataguide/mongodb/connecting-to-mongodb#connecting-to-a-local-database-with-mongo)
    
* [https://www.mongodb.com/docs/v4.2/reference/program/mongodump/](https://www.mongodb.com/docs/v4.2/reference/program/mongodump/)
    

## Install MongoDB on local machine

In case your OS is MacOS.

```bash
brew tap mongodb/brew
brew install mongodb-community

# check configuration
cat /opt/homebrew/etc/mongod.conf

# check log file
cat /opt/homebrew/var/log/mongodb/mongo.log

# start the MongoDB service
brew services start mongodb-community

# To verify that MongoDB is running
brew services list

# Try MongoDB shell
mongosh
```

Download [compass tool - the GUI for MongoDB](https://www.mongodb.com/try/download/compass).

Or install compass by `brew install --cask mongodb-compass` command.

Connect MongoDB service on `mongodb://`[`localhost:27017`](http://localhost:27017) by that compass tool.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703157643552/079c1477-801b-417c-b743-89bbbe6fd2c4.png align="center")

## Clone data from remote MongoDB connection

```bash
mongodump --uri="mongodb://mongodb0.example.com:27017/db_name?retryWrites=true&w=majority&authSource=admin" [additional options]
```

> [`mongodump`](https://www.mongodb.com/docs/v4.2/reference/program/mongodump/#bin.mongodump) is a utility for creating a binary export of the contents of a database.

```bash
mongorestore --uri="mongodb://localhost:27017/db_name" --db db_name dump/db_name
```

Open the compass tool again and view cloned data!