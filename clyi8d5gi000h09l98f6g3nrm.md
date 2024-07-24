---
title: "starship - The customizable prompt for any shell - Share my configuration for better visualization of git and Cloud icon"
seoTitle: "starship - configuration for better visualization of git and cloud"
seoDescription: "starship - Share my configuration for better visualization of git and Cloud icon"
datePublished: Fri Jul 12 2024 05:01:27 GMT+0000 (Coordinated Universal Time)
cuid: clyi8d5gi000h09l98f6g3nrm
slug: starship-the-customizable-prompt-for-any-shell-share-my-configuration-for-better-visualization-of-git-and-cloud-icon
tags: cloud, command-line, starship

---

## Share my configuration for better visualization of git and Cloud icon

[starship - The minimal, blazing-fast, and infinitely customizable prompt for any shell!](https://github.com/starship/starship)

Create configuration file:

```sh
mkdir -p ~/.config && touch ~/.config/starship.toml
code ~/.config/starship.toml
```

`~/.config/starship.toml` file contents:

```toml
# Get editor completions based on the config schema
"$schema" = 'https://starship.rs/config-schema.json'

command_timeout = 2000

[git_branch]
symbol = '🌱 '

[aws]
# disabled = true
format = '[$symbol($profile )(\($region\) )]($style)'
symbol = 'AWS '
style = 'blue'

[gcloud]
# disabled = true
symbol = 'GCP '
```

Sometime you want to hidden cloud icon, please use `disabled = true`.
