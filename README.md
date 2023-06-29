# Git Plugins

A few small plugins to make life with Git easier.

## Installation

Clone the repository and either add the plugins to your path or link to them.
Git will automatically find any commands on your path with the name `git-*` and add them as subcommands.

```bash
$ git clone https://github.com/darwish/git-plugins
$ cd git-plugins
$ sudo ln -s $(pwd)/git-* /usr/local/bin/

# Usage:
$ git purge
$ git refresh
```

## git-purge

`git-purge` prunes remote refs from the origin, and then finds the corresponding local branches and deletes them.

## git-refresh

`git-refresh` checks out the master branch, pulls changes in from the remote, and then runs `git-purge`.
