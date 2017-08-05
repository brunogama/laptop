Laptop
======

Laptop is a fork from the awesome script made by the good people of thoughtbot. It's purpose is to set up an macOS laptop for Mobile Development.

It can be run multiple times on the same machine safely.
It installs, upgrades, or skips packages
based on what is already installed on the machine.

Why to use this fork?
---------------------

Most of the things installed by the original Laptop script are to prepare the machine for Web Development. It will install things like Heroku toolbelt, Postgres, MySQL which in my opinion should not be installed in the machine but in a self contained environment using something like Docker.

Requirements
------------

* macOS Sierra (10.12)

Older versions may work. But if they don't, feel free to write a PR.

Install
-------

Download the script:

```sh
curl --remote-name https://raw.githubusercontent.com/brunogama/laptop/master/mac
```

Review the script (avoid running scripts you haven't read!):

```sh
less mac
```

Execute the downloaded script:

```sh
sh mac 2>&1 | tee ~/laptop.log
```

Optionally, review the log:

```sh
less ~/laptop.log
```

Debugging
---------

Your last Laptop run will be saved to `~/laptop.log`.
Read through it to see if you can debug the issue yourself.
If not, copy the lines where the script failed into a
[new GitHub Issue](https://github.com/brunogama/laptop/issues/new) for us.
Or, attach the whole log file as an attachment.

What it sets up
---------------

macOS tools:

* [Homebrew] for managing operating system libraries.

[Homebrew]: http://brew.sh/

Unix tools:

* [Git] for version control
* [OpenSSL] for Transport Layer Security (TLS)
* [The Silver Searcher] for finding things in files
* [Tmux] for saving project state and switching between projects
* [Zsh] as your shell

[Git]: https://git-scm.com/
[OpenSSL]: https://www.openssl.org/
[The Silver Searcher]: https://github.com/ggreer/the_silver_searcher
[Tmux]: http://tmux.github.io/
[Zsh]: http://www.zsh.org/


GitHub tools:

* [Hub] for interacting with the GitHub API

[Hub]: http://hub.github.com/

Programming languages, package managers, and configuration:

* [Java] for writing Android code
* [Bundler] for managing Ruby libraries
* [Rbenv] for managing versions of Ruby
* [Ruby Build] for installing Rubies
* [Ruby] stable for writing general-purpose code
* [Pyenv] For managing versions of Python
* [Pyenv-virtualbox] virtualenvs and conda environments for Python on UNIX-like systems
* [Python] install the latest stable Python 3

[Java]: https://java.com/
[Bundler]: http://bundler.io/
[Node.js]: http://nodejs.org/
[NPM]: https://www.npmjs.org/
[Rbenv]: https://github.com/sstephenson/rbenv
[Ruby Build]: https://github.com/sstephenson/ruby-build
[Ruby]: https://www.ruby-lang.org/en/
[Pyenv]: https://github.com/pyenv/pyenv
[Pyenv-virtualbox]: https://github.com/pyenv/pyenv-virtualenv
[Python]: https://www.python.org/

Mobile development utilities

* [Liftoff] CLI for creating and configuring new Xcode projects
* [mogenerator] Core Data code generation

[Liftoff]: https://github.com/liftoffcli/liftoff
[mogenerator]: https://github.com/rentzsch/mogenerator

Aplications

* [Google Chrome] because it is like Java, because everything uses Google Chrome
* [Android Studio] "Android Studio provides the fastest tools for building apps on every type of Android device" (sic)
* [Sip] simply the color picker created
* [Developer Colorpicker] another useful color picker
* [Github Desktop] a Github client
* [VirtualBox] is a general-purpose full virtualizer for x86 hardware
* [Genymotion] a much better Android simulator which runs on virtualbox environment
* [Realm Browser] utility to open and modify realm database files

[Google Chrome]: https://www.google.com.br/chrome/browser/desktop/index.html
[Android Studio]: https://developer.android.com/studio/
[Sip]: http://sipapp.io/
[Developer Colorpicker]: https://download.panic.com/picker/
[Github Desktop]: https://desktop.github.com/
[VirtualBox]: https://www.virtualbox.org/
[Genymotion]: https://www.genymotion.com
[Realm Browser]: https://github.com/realm/realm-browser-osx

iOS Development Utilities

* [Cocoapods] a dependency manager for Swift and Objective-C Cocoa projects
* [Fastlane] the easiest way to automate building and releasing your iOS and Android apps

[Cocoapods]: https://cocoapods.org/
[Fastlane]: https://fastlane.tools/

It should take ~15 minutes to install (depends on your machine).

Customize in `~/.laptop.local`
------------------------------

Your `~/.laptop.local` is run at the end of the Laptop script.
Put your customizations there.
For example:

```sh
#!/bin/sh

brew bundle --file=- <<EOF
brew "Caskroom/cask/dockertoolbox"
brew "go"
brew "ngrok"
brew "watch"
EOF

default_docker_machine() {
  docker-machine ls | grep -Fq "default"
}

if ! default_docker_machine; then
  docker-machine create --driver virtualbox default
fi

default_docker_machine_running() {
  default_docker_machine | grep -Fq "Running"
}

if ! default_docker_machine_running; then
  docker-machine start default
fi

fancy_echo "Cleaning up old Homebrew formulae ..."
brew cleanup
brew cask cleanup

if [ -r "$HOME/.rcrc" ]; then
  fancy_echo "Updating dotfiles ..."
  rcup
fi
```

Write your customizations such that they can be run safely more than once.
See the `mac` script for examples.

Laptop functions such as `fancy_echo` and
`gem_install_or_update`
can be used in your `~/.laptop.local`.

See the [wiki](https://github.com/thoughtbot/laptop/wiki)
for more customization examples.

Contributing
------------

Edit the `mac` file.
Document in the `README.md` file.
Follow shell style guidelines by using [ShellCheck] and [Syntastic].

```sh
brew install shellcheck
```

[ShellCheck]: http://www.shellcheck.net/about.html
[Syntastic]: https://github.com/scrooloose/syntastic



Credits
-------

The Bruno Gama laptop script is based on and inspired by
[thoughtbot's laptop](https://github.com/thoughtbot/laptop) script.

LICENSE
-------------

thoughtbot's original work remains covered under an [MIT License](https://github.com/thoughtbot/laptop/blob/c997c4fb5a986b22d6c53214d8f219600a4561ee/LICENSE).

Bruno Gama work on this project is licensed under MIT License (LICENSE.md).