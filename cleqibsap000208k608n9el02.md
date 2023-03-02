# Ubuntu - install rust lang 🦀 and try zoxide - a smarter cd command

```bash
# install rust compiler 📖
sudo nala install rustc
# or
sudo apt install rustc

# verify 📖
rustc -V

# install rust package manager 📦
sudo nala install cargo

# verify 📦
cargo -V
```

Install [zoxide - a smarter cd command](https://github.com/ajeetdsouza/zoxide#installation):

```bash
sudo cargo install zoxide --locked

# try it
z
# output is path list
z some-folder-name
# and use "tab" key
```