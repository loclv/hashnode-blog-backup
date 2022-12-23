# Set PATH for Python PIP on fish shell

If you want to install Python packages and run them as a command on Linux [fish-shell](https://fishshell.com/), it gives an error: `"xxx command not found"`.

> The problem with Linux is that `pip install ...` drops scripts into `~/.local/bin` and this is not on the default Debian/Ubuntu `$PATH`.

To fix it, just add `~/.local/bin` to your `$PATH` but on fish shell:

```bash
# open config file
code ~/.config/fish/config.fish
```

Edit `config.fish` file:

```bash
set -gx PIP_HOME "/home/$USER/.local/bin"
set -gx PATH "$PIP_HOME" $PATH
```

Since `$USER` and `$PATH` is global variable, so we do not need to define them.

Restart a fish shell session and try to run Python packages again!

### Reference

* [https://stackoverflow.com/questions/35898734/pip-installs-packages-successfully-but-executables-not-found-from-command-line](https://stackoverflow.com/questions/35898734/pip-installs-packages-successfully-but-executables-not-found-from-command-line)
    
* [https://github.com/pypa/pip/issues/3813](https://github.com/pypa/pip/issues/3813)