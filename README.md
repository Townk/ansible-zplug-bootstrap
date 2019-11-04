# ZPlug Bootstrap
Installs and configure ZPlug into the host machine. ZPlug can be installed
locally or on the system if your host is a MacOSX machine, or locally on any
other Unix box.

## Requirements
- Open internet connection on the host in order to install ZPlug.

## Role Variables
| Variable                      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                   | Default value      |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `zplug_plugins`               | List of plugin objects to keep installed. Each plugin is a dictionary with keys that are the same as the [tags](https://github.com/zplug/zplug#3-tags-for-zplug) for ZPlug, plus the key `name` with the plugin name as value.                                                                                                                                                                                                                | `[]`               |
| `zplug_preffer_local_install` | Flag indicating if the user preffers to install ZPlug inside the `$HOME` folder, or if ZPlug Bootstrap should try to install it on the system with the default package manager. Currently, ZPlug Bootstrap only uses Homebrew for system installs, which means tht Linux and other Unix systems will have ZPlug installed on the user space.                                                                                                  | `no`               |
| `zplug_home_dir`              | Where ZPlug should be installed. If the value is the string `"XDG_PACKAGE_HOME"`, this role will try to resolve the `XDG_PACKAGE_HOME` environment variable in the host to use it as the installation directory. If the variable is not defined, it uses `$HOME/.zplug` as a fallback.                                                                                                                                                        | `XDG_PACKAGE_HOME` |
| `zplug_cache_dir`             | Where ZPlug cache should be stored. If the value is the string `"XDG_CACHE_HOME"`, this role will try to resolve the `XDG_CACHE_HOME` environment variable in the host to use it as the cache directory. If the variable is not defined, it uses `$HOME/.zplug/cache` as a fallback.                                                                                                                                                          | `XDG_CACHE_HOME`   |
| `zplug_repos_dir`             | Where ZPlug download repositories should be stored. If the value is the string `"XDG_DATA_HOME"`, this role will try to resolve the `XDG_DATA_HOME` environment variable in the host to use it as the repositories directory. If the variable is not defined, it uses `$HOME/.zplug/repos` as a fallback.                                                                                                                                     | `XDG_DATA_HOME`    |
| `zplug_packages_location`     | Where ZPlug package list file should be stored. If the value is the string `"XDG_DATA_HOME"`, this role will try to resolve the `XDG_DATA_HOME` environment variable in the host to use it as the base directory for the packages list file (`$XDG_DATA_HOME/zplug/packages.zsh`). If the variable is not defined, it uses `$HOME/.zplug/packages.zsh` as a fallback.                                                                         | `XDG_DATA_HOME`    |
| `zplug_plugin_location`       | Where the ZSH plugin that loads ZPlug should be stored. The ZSH plugin should be sourced from your `.zshrc`. If the value is the string `"XDG_DATA_HOME"`, this role will try to resolve the `XDG_DATA_HOME` environment variable in the host to use it as the base directory for the ZSH plugin file (`$XDG_DATA_HOME/zplug/zplug-bootstrap.zsh`). If the variable is not defined, it uses `$HOME/.zplug/zplug-bootstrap.zsh` as a fallback. | `XDG_DATA_HOME`    |

## Dependencies
None.

## Example Playbook
Uses the same install configuration as the ZPlug entries in a `.zshrc` file:

```yaml
    - hosts: servers
      tasks:
        - name: Install ZPlug
          include_role:
            name: townk.zplug_bootstrap
          vars:
            zplug_plugins:
                - name: softmoth/zsh-vim-mode
                - name: plugins/colored-man-pages
                  defer: 2
                  from: oh-my-zsh
                  as: plugin
                - name: zsh-users/zsh-autosuggestions
                  defer: 2
```     

## License
MIT License

Copyright (c) 2019 Thiago Alves

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## About the author
My real name is Thiago Alves and I'm an old-school software engineer trying to
keep up with the cool kids' toys of these days.