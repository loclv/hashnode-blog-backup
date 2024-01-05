---
title: "Show git tags from most recent created and filter by tag name 🎏"
seoTitle: "Show git tags from most recent created and filter by tag name"
seoDescription: "Show git tags from most recent created and filter by tag name, also view commit message of tag."
datePublished: Fri Jan 05 2024 03:02:13 GMT+0000 (Coordinated Universal Time)
cuid: clr01vtsv000009l7e24m8sbi
slug: show-git-tags-from-most-recent-created-and-filter-by-tag-name
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/W8Qqn1PmQH0/upload/7e2435bce8f6d87d68f8c1dd97b5d06e.jpeg
tags: git

---

## Why we need this?

- In case we want to know which tag is newest.
- We want to know tag description by commit message.

## Git command options

```bash
git log --no-walk --tags --pretty="%h %d %s" --decorate=full | grep "tag-name"
```

Output's template:

```txt
<shortened version of commit hash>  (tag: <tag name>, tag: <another tag>, ...) <commit message>
# for example
# abc123456  (tag: refs/tags/xxx.v1) fix: bug when something has changed
```

## References

- <https://stackoverflow.com/questions/4211604/show-all-tags-in-git-log>
