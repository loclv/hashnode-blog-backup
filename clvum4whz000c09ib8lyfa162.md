---
title: "MongoDB 🌱 - Try to backup and restore the database with --gzip option"
seoTitle: " backup and restore the MongoDB database with --gzip option"
seoDescription: " backup and restore the MongoDB database with --gzip option
mongodump
mongorestore"
datePublished: Mon May 06 2024 07:01:04 GMT+0000 (Coordinated Universal Time)
cuid: clvum4whz000c09ib8lyfa162
slug: mongodb-try-to-backup-and-restore-the-database-with-gzip-option
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/xT7OuIFew3Q/upload/6eb8a198b5904fbb731d63011860dbfd.jpeg
tags: mongodb, backup

---

When you backup the database, you should choose collection output with Gzip, not `.bson` or `.json` for efficient storage.

Here is an example using `abc` DB at localhost with output directory is `dump/local_abc_2024_05_05_13_19`:

```bash
mongodump --uri="mongodb://localhost:27017/abc" --db abc -o dump/local_abc_2024_05_05_13_19 --gzip
```

You can use `mongodump --help` for more information:

```txt
Export the content of a running server into .bson files.

Specify a database with -d and a collection with -c to only dump that database or collection.

Connection strings must begin with mongodb:// or mongodb+srv://.

See http://docs.mongodb.com/database-tools/mongodump/ for more information.
...

namespace options:
  -d, --db=<database-name>                                  database to use
  -c, --collection=<collection-name>                        collection to use

uri options:
      --uri=mongodb-uri                                     mongodb uri connection string
...

output options:
  -o, --out=<directory-path>                                output directory, or '-' for stdout (default: 'dump')
      --gzip                                                compress archive or collection output with Gzip

```

Expected output is the following text:

```text
2024-05-05T11:22:33.802+0700    done dumping <database-name>.<collection-name>
```

When running `mongorestore`, you should specify the option `--gzip` to restore from compressed files or data stream created by `mongodump --gzip`.

```sh
mongorestore --uri="mongodb://localhost:27017/abc_2024_05_05_13_19" --db abc_2024_05_05_13_19 dump/abc_2024_05_05_13_19/abc  --gzip
```

## References

- [mongorestore](https://www.mongodb.com/docs/database-tools/mongorestore/)
- [mongodump](https://www.mongodb.com/docs/database-tools/mongodump/)
