# Debian-based Linux - Try apt alternative - Nala - a packages manager

## Introduction

[Nala](https://gitlab.com/volian/nala) is a neatly structured frontend for [APT Package Manager](https://blog.packagecloud.io/what-is-the-apt-package-manager-why-and-how-to-use-it/).

Basically, it is used to install and manage packages on Debian-based Linux systems. It is an alternative for apt.

## Installation and try it

```bash
# install
sudo apt install nala
# find fastest mirrors
sudo nala fetch
```

The result is more understandable UX:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673176040417/6eb72d36-b0d3-475e-9a8c-479f62310167.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673177756242/de756bda-5000-4256-8f0c-aada66f204ff.png align="center")

```bash
sudo nala update
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673448773301/0dea944e-4427-4e50-ba8a-60a803fe8884.png align="center")

We are going to install [exa](https://github.com/ogham/exa) \- A modern replacement for *ls*, written in Rust language:

```bash
sudo nala install exa
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673451735731/fd456855-43bc-4495-b03c-157401466a85.png align="center")

We check out the new package version to make sure it's installed:

```bash
exa -v
```

The clean-up combo became this:

```bash
sudo apt-get update && sudo apt-get upgrade -y && sudo apt autoremove
# became:
sudo nala update && sudo nala upgrade -y && sudo nala autoremove
```

## References

* [https://www.omgubuntu.co.uk/2023/01/install-nala-on-ubuntu](https://www.omgubuntu.co.uk/2023/01/install-nala-on-ubuntu)
    
* [https://gitlab.com/volian/nala](https://gitlab.com/volian/nala)
    
* [https://www.linuxshelltips.com/nala-frontend-apt-package-manager/](https://www.linuxshelltips.com/nala-frontend-apt-package-manager/)