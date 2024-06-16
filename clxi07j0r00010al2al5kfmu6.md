---
title: "fnm - get latest 🌱 NodeJS version"
seoTitle: "fnm - get latest NodeJS version"
seoDescription: "fnm - get latest NodeJS version"
datePublished: Sun Jun 16 2024 20:33:25 GMT+0000 (Coordinated Universal Time)
cuid: clxi07j0r00010al2al5kfmu6
slug: fnm-get-latest-nodejs-version
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/vmNr7aM-h8Q/upload/aadafaca483d744996d613231c48e466.jpeg
tags: nodejs, fnm

---

[fnm](https://github.com/Schniz/fnm) is a 🚀 Fast and simple Node.js version manager, built in Rust.

# Get latest 🌱 NodeJS version from [nodejs.org/dist](http://nodejs.org/dist)

```sh
fnm list-remote --latest
# expected version now: v22.3.0

# install it:
fnm use 22.3
# Do you want to install it? answer [y/N]: y
# Using Node v22.3.0

# confirm
node -v
# expected version: v22.3.0

# for more info and config:
fnm list-remote --help
```
