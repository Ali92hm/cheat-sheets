# Git

## Setup

### Set a name that is identifiable for credit when review version history:
```
git config --global user.name “[firstname lastname]”
```

### Set an email address that will be associated with each history marker:
```
git config --global user.email “[valid-email]”
```

### Set automatic command line coloring for Git for easy reviewing:
```
git config --global color.ui auto
```

## Configuration Files

### Repository specific configuration file [--local]:
```
<repo>/.git/config
```

### User-specific configuration file [--global]:
```
~/.gitconfig
```

### System-wide configuration file [--system]:
```
/etc/gitconfig
```

### Ignore permissions and filemode changes

```
git config core.fileMode false
```

```
git config --global core.fileMode false
```


## Local Changes

### Changes in working directory:
```
git status
```

### Changes to tracked files:
```
git diff
```

### Add all current changes to the next commit:
```
git add .
```

### Add some changes in &lt;file&gt; to the next commit:
```
git add -p <file>
```

### Commit all local changes in tracked files:
```
git commit -a
```

### Commit previously staged changes:
```
git commit
```

### Commit with message:
```
git commit -m 'message here'
```

### Commit skipping the staging area and adding message:
```
git commit -am 'message here'
```

### Commit to some previous date:
```
git commit --date="`date --date='n day ago'`" -am "<Commit Message Here>"
```

### Change last commit

```
git commit --amend
or
git commit --amend -m 'xxxxxxx'
```

### Amend with last commit but use the previous commit log message

```
git commit --amend --no-edit
```

### Change committer date of last commit:
```
GIT_COMMITTER_DATE="date" git commit --amend
```

### Change Author date of last commit:
```
git commit --amend --date="date"
```

### Change wrong name and email

```
git commit --amend --no-edit --author "New Authorname <authoremail@mydomain.com>"
```

An alternative is to correctly configure your author settings in `git config --global author.(name|email)` and then use

```
git commit --amend --reset-author --no-edit
```

### Move uncommitted changes from current branch to some other branch:<br>
```
git stash
git checkout branch2
git stash pop
```

### Restore stashed changes back to current branch:
```
git stash apply
```

### Restore particular stash back to current branch:

```
git stash list
git stash apply stash@{stash_number}
```

### Remove the last set of stashed changes:
```
git stash drop
```


## Commit History

### Show all commits, starting with newest (it'll show the hash, author information, date of commit and title of the commit):
```
git log
```

### Show all the commits(it'll show just the commit hash and the commit message):
```
git log --oneline
```

### Show all commits of a specific user:
```
git log --author="username"
```

### Show changes over time for a specific file:
```
git log -p <file>
```

### Who changed, what and when in &lt;file&gt;:
```
git blame <file>
```


### Show Reference log:
```
git reflog show
```

## Branches & Tags

### List all local branches:
```
git branch
```

### List local/remote branches
```
git branch -a
```

### List all remote branches:
```
git branch -r
```

### Switch HEAD branch:
```
git checkout <branch>
```

### Checkout single file from different branch
```
git checkout <branch> -- <filename>
```

### Create and switch new branch:
```
git checkout -b <branch>
```

### Checkout and create a new branch from existing commit
```
git checkout <commit-hash> -b <new_branch_name>
```

### Create a new branch based on your current HEAD:
```
git branch <new-branch>
```

### Delete a local branch:
```
git branch -d <branch>
```

### Rename current branch to new branch name
```
git branch -m <new_branch_name>
```

### Force delete a local branch:

```
git branch -D <branch>
```

### Mark the current commit with a tag:
```
git tag <tag-name>
```

### Mark the current commit with a tag that includes a message:
```
git tag -a <tag-name>
```


## Update & Publish

### List all current configured remotes:
```
git remote -v
```

### Show information about a remote:
```
git remote show <remote>
```

### Add new remote repository, named &lt;remote&gt;:
```
git remote add <remote> <url>
```

### Download all changes from &lt;remote&gt;, but don't integrate into HEAD:
```
git fetch <remote>
```

### Download changes and directly merge/integrate into HEAD:
```
git remote pull <remote> <url>
```

### Get all changes from HEAD to local repository:
```
git pull origin master
```

### Get all changes from HEAD to local repository without a merge:
```
git pull --rebase <remote> <branch>
```

### Publish local changes on a remote:
```
git push remote <remote> <branch>
```

### Delete a branch on the remote:
```
git push <remote> :<branch> # (since Git v1.5.0)

git push <remote> --delete <branch> # (since Git v1.7.0)
```

### Publish your tags:
```
git push --tags
```

### Overwrite local files when doing a git pull

```
git fetch --all
git reset --hard origin/master
```

## Merge & Rebase

### Merge branch into your current HEAD:
```
git merge <branch>
```

### Rebase your current HEAD onto &lt;branch&gt;:<br>

```
git rebase <branch>
```

### Abort a rebase:
```
git rebase --abort
```

### Continue a rebase after resolving conflicts:
```
git rebase --continue
```

### Use your editor to manually solve conflicts and (after resolving) mark file as resolved:
```
git add <resolved-file>
```

```
git rm <resolved-file>
```

### Squashing commits:
```
git rebase -i <commit-just-before-first>
```

Now replace this,

```
pick <commit_id>
pick <commit_id2>
pick <commit_id3>
```

to this,

```
pick <commit_id>
squash <commit_id2>
squash <commit_id3>
```

## Undo

### Discard all local changes in your working directory:
```
git reset --hard HEAD
```

### Get all the files out of the staging area(i.e. undo the last `git add`):
```
git reset HEAD
```

### Discard local changes in a specific file:
```
git checkout HEAD <file>
```

### Interactive discard
```
git checkout -p
```

### Revert a commit (by producing a new commit with contrary changes):
```
git revert <commit>
```

### Reset your HEAD pointer to a previous commit and discard all changes since then:
```
git reset --hard <commit>
```

### Reset your HEAD pointer to a remote branch current state.
```
git reset --hard <remote/branch> e.g., upstream/master, origin/my-feature
```

### Reset your HEAD pointer to a previous commit and preserve all changes as unstaged changes:
```
git reset <commit>
```

### Reset your HEAD pointer to a previous commit and preserve uncommitted local changes:
```
git reset --keep <commit>
```

### Remove files that were accidentally committed before they were added to .gitignore
```
git rm -r --cached .
git add .
git commit -m "remove xyz file"
```

### Remove a file from the previous commit
```
git checkout HEAD^ myfile
git add myfile
git commit --amend --no-edit
```

In case the file was newly added to the commit and you want to remove it (from Git alone), do:

```
git rm --cached myfile
git commit --amend --no-edit
```

### Delete or remove last commit

```
git reset HEAD^ --hard
git push --force-with-lease [remote] [branch]
```

If you haven't pushed, to reset Git to the state it was in before you made your last commit (while keeping your staged changes):

```
git reset --soft HEAD@{1}
```

### Delete/remove arbitrary commit

The same warning applies as above. Never do this if possible.

```
git rebase --onto SHA1_OF_BAD_COMMIT^ SHA1_OF_BAD_COMMIT
git push --force-with-lease [remote] [branch]
```

### I accidentally did a hard reset, and I want my changes back

Note: This is only valid if your work is backed up, i.e., either committed or stashed.
```
git reflog
git reset --hard SHA1234
```

### Restore a deleted file

First find the commit when the file last existed:

```
git rev-list -n 1 HEAD -- filename
```

Then checkout that file:

```
git checkout deletingcommitid^ -- filename
```

### Delete tag

```
git tag -d <tag_name>
git push <remote> :refs/tags/<tag_name>
```

### Change a file name's capitalization, without changing the contents of the file

```
git mv --force myfile MyFile
```


### Remove a file from Git but keep the file
```
git rm --cached log.txt
```

### Revert a file to a specific revision

Assuming the hash of the commit you want is c5f567:

```
git checkout H -- file1/to/restore file2/to/restore
```

If you want to revert to changes made just 1 commit before c5f567, pass the commit hash as c5f567~1:

```
git checkout c5f567~1 -- file1/to/restore file2/to/restore
```

## Submodules

### Clone all submodules

```
git clone --recursive git://github.com/foo/bar.git
```

If already cloned:

```
git submodule update --init --recursive
```

### Remove a submodule

Creating a submodule is pretty straight-forward, but deleting them less so. The commands you need are:

```
git submodule deinit submodulename
git rm submodulename
git rm --cached submodulename
rm -rf .git/modules/submodulename
```
