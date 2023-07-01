---
title: "Ruby - Use Rubocop on VS Code"
datePublished: Sat Jul 01 2023 13:40:41 GMT+0000 (Coordinated Universal Time)
cuid: cljk1wqpj000e09mf7x84bvc4
slug: ruby-use-rubocop-on-vs-code
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/F04_1icrUtM/upload/431a8110c7289847588655ab7c55da6a.jpeg
tags: ruby, rubocop

---

Don't want to run Rubocop command on the terminal? Try it on VS Code!

## Prepare to install

If you are using macOS, please follow [this blog post to install Ruby **in a macOS for local development**](https://snyk.io/blog/how-to-install-ruby-in-mac-os/)**.**

Make sure that you can run the `ruby` command on your shell:

```bash
ruby -v
# output is ruby version

gem install rubocop
which rubocop
```

If you are using "zsh" shell and `ruby` from `brew`, make sure that you added the lines below to `~/.zshrc`:

```bash
# ruby
if [ -d "/opt/homebrew/opt/ruby/bin" ]; then
  export PATH=/opt/homebrew/opt/ruby/bin:$PATH
  export PATH=`gem environment gemdir`/bin:$PATH
fi
```

Now, let's install the [Ruby Rubocop extension](https://marketplace.visualstudio.com/items?itemName=misogi.ruby-rubocop) on VS Code.

## Configuration

Open your VS Code configuration by pressing `command + shift + p` and input the `JSON` text.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688217847979/8c7917d6-9585-4a1c-9e5f-c04d9c61dfa8.png align="center")

Then choose the `Open User Settings (JSON)` feature.

Specify the configuration below if you want.

```json
{
  // If not specified searches for 'rubocop' executable
  // available on PATH (default and recommended)
  "ruby.rubocop.executePath": "",

  // You can use specific path
  // "ruby.rubocop.executePath": "/Users/you/.rbenv/shims/"
  // "ruby.rubocop.executePath": "/Users/you/.rvm/gems/ruby-2.3.2/bin/"
  // "ruby.rubocop.executePath": "D:/bin/Ruby22-x64/bin/"

  // If not specified, it assumes a null value by default.
  "ruby.rubocop.configFilePath": "/path/to/config/.rubocop.yml",

  // default true
  "ruby.rubocop.onSave": true
}
```

## How to use it?

To use this extension, press `command + shift + p` and input the `rubocop` text.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688218446127/47905b32-8e6a-4651-b1a4-7c578a1d3dea.png align="center")

We hare 2 options:

* "Lint by rubocop": lint the current ruby file and show warning if Rubocop found problems.
    
* "autocorrect by rubocop": lint the current ruby file and auto fix that problems if Rubocop can.
    

Happy coding!