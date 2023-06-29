# Git Plugins

A few small plugins to make life with Git easier.

## Installation

Clone the repository and either add the plugins to your path or link to them.
Git will automatically find any commands on your path with the name `git-*` and add them as subcommands.

```bash
$ git clone https://github.com/darwish/git-plugins
$ cd git-plugins
$(pwd)/git-* /usr/local/bin/

# Usage:
$ git purge
$ git refresh
```

## git-purge

`git-purge` prunes remote refs from the origin, and then finds the corresponding local branches and deletes them.
This comes in handy when your Git workflow involves creating a lot of short-lived feature branches that are deleted on the remote after a merge is completed.

Example workflow:

```bash
# Create a new local feature branch
$ git checkout -b my-feature
Switched to a new branch 'my-feature'

# Make some changes on the local branch
$ touch file

# Commit the changes
$ git add .
$ git commit -m "New file"
[my-feature 69bef9f] New file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file

# Push the changes to a remote feature branch
$ git push --set-upstream origin my-feature
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 340 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To gl:mida/git-plugins
 * [new branch]      my-feature -> my-feature
Branch my-feature set up to track remote branch my-feature from origin.

# There is now a local my-feature branch and a remote origin/my-feature branch
$ git branch -a
  master
* my-feature
  remotes/origin/master
  remotes/origin/my-feature

# On the remote server:
#  - create merge request
#  - branch gets merged
#  - remote branch gets deleted

# Switch away from the local feature branch
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

# Purge branches that have been removed on the remote
$ git purge
Will delete branches:
  my-feature

Delete? (y/n) y
Deleted branch my-feature (was 69bef9f).

# Both the remote and the local branches have been now cleaned up
$ git branch -a
* master
  remotes/origin/master
```

## git-refresh

`git-refresh` checks out the master branch, pulls changes in from the remote, and then runs `git-purge`.
This is a quick way to get rid of any feature branches that were lying around, and get the repository into a state to start working on it again.