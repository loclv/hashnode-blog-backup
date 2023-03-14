---
title: "Useful package collection for Windows PowerShell"
datePublished: Tue Mar 14 2023 16:41:57 GMT+0000 (Coordinated Universal Time)
cuid: clf8he0g1000n0ajp5kyb7wf8
slug: useful-package-collection-for-windows-powershell
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/LVnJlyfa7Zk/upload/abe11cb2173994550ddf8f4af6195cb9.jpeg
tags: powershell

---

## 🐚Collection

* [https://github.com/ScoopInstaller/Scoop](https://github.com/ScoopInstaller/Scoop) - A command-line installer for Windows.
    
* [https://github.com/starship/starship](https://github.com/starship/starship) - ☄🌌️ The minimal, blazing-fast, and infinitely customizable prompt for any shell!
    
* [https://github.com/Schniz/fnm](https://github.com/Schniz/fnm) - 🚀 Fast and simple Node.js version manager, built in Rust.
    
* [https://github.com/Peltoche/lsd](https://github.com/Peltoche/lsd) - This project is a rewrite of GNU `ls` with lots of added features like colors, icons, tree-view, more formatting options etc.
    
* [https://github.com/janikvonrotz/awesome-powershell#commandline-productivity](https://github.com/janikvonrotz/awesome-powershell#commandline-productivity) - Commandline Productivity list.
    
* [https://github.com/search?l=powershell&q=stars%3A%3E1&s=stars&type=Repositories](https://github.com/search?l=powershell&q=stars%3A%3E1&s=stars&type=Repositories) - github's query. `stars:>1` and `type=Repositories` params.
    
* [https://draculatheme.com/powershell](https://draculatheme.com/powershell) - Dark theme for PowerShell [and 318+ apps](https://draculatheme.com/).
    

## 🏔️ Config on PowerShell profile

Open PowerShell profile file:

```bash
code  $HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
```

File content:

```bash
Invoke-Expression (&starship init powershell)
fnm env --use-on-cd | Out-String | Invoke-Expression
```