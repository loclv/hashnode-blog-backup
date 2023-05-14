---
title: "Summary of starting configuration on git 🌱"
datePublished: Sun May 14 2023 03:54:58 GMT+0000 (Coordinated Universal Time)
cuid: clhmvumd0000409jydx53h2hs
slug: summary-of-starting-configuration-on-git
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MNd-Rka1o0Q/upload/2719fc4447c2684974a70d3825fc44ba.jpeg
tags: git

---

## Config user identification

```bash
git config --global user.name "my-name"
git config --global user.email "my@email.com"
```

## Default branch name

```bash
git config --global init.defaultBranch main
```

## Moved block color

```bash
git config --global diff.colorMoved zebra
```

## **Pull with Rebase**

```bash
git config --global pull.rebase true
```

## Shorter minimal git status

```bash
git config --global status.short true
```

## Generate an SSH key

You can read [generating a new SSH key step by step here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

## Confirm all settings

```bash
git config -l
# or
cat ~/.gitconfig
```

## References and detailed explanation

* [https://dev.to/nedsoft/useful-git-config-tips-274i](https://dev.to/nedsoft/useful-git-config-tips-274i)
    
* [https://dev.to/cloudx/how-to-color-the-moved-code-in-git-10ei](https://dev.to/cloudx/how-to-color-the-moved-code-in-git-10ei)
    
* [https://spin.atomicobject.com/2020/05/05/git-configurations-default/](https://spin.atomicobject.com/2020/05/05/git-configurations-default/)
    
* [https://www.freecodecamp.org/news/git-config-how-to-configure-git-settings/](https://www.freecodecamp.org/news/git-config-how-to-configure-git-settings/)