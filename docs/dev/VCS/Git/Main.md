### Checkout specific commit in new branch, without messing things up too much
```
git checkout -b test-branch 56a4e5c08
```

### Add files from other branches

Where **versions** is the branch from where the changes need to be imported, and the files are specified after the '--'
```
git checkout versions -- some_folder/other_folder/versions.sql
```

### Push to ssh repo with different user (or github account)
Sources: [this](https://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574) and [this](https://gist.github.com/patsancu/b1504d8dd4bcca8130cb0d66fa2c9539)

#### create-a-new-ssh-key
See [this](../../../Ops/SSH.md#create-a-new-ssh-key)

#### Attach key
Login to your git repo service and paste the contents of your new pub key
#### Add ssh host alias
Edit ~/.ssh/config file to add something like the following
```
#Default GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

### Edit this for a different account!
Host github-COMPANY
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_COMPANY
```

#### Configure repo to work with new host
Replace __github-COMPANY__, __USERNAME__ and __REPONAME__ with your own values
```
git remote add origin git@github-COMPANY:USERNAME/REPO_NAME.git
git config  github.user USERNAME
git push origin master
```

### Change repo from http(s) to git/ssh
Change config url from `https://github.com/USERNAME/REPO_NAME.git` to `git@github.com/USERNAME:REPO_NAME.git`

### Interactively add, skip, or split diff hunks
```
$ git add -p
```

### Show diff of one specific commit
```bash
git show commit-hash-stuff
```

### Squash unpushed commits into one
Scenario: The last two commits are unpushed, and you want to merge them into one.
```git rebase -i HEAD~2```
This will open the default editor
```
pick hash1 Bla bla bla Commit message
pick hash2 Bla bla bla another Commit message
```
Leave the first one as it is and put the second one as squash
```
pick hash1 Bla bla bla Commit message
squash hash2 Bla bla bla another Commit message
```
Again, the editor will open, to let you edit the final commit message.
Sources: [this](https://www.devroom.io/2011/07/05/git-squash-your-latests-commits-into-one/).

### [Stash](https://git-scm.com/docs/git-stash)
**Useful** examples [here](https://git-scm.com/docs/git-stash#_examples)

#### Stash the changes in a dirty working directory away
```
$ git stash
```

#### List modifications stashes
```
$ git stash list
stash@{0}: WIP on alerting: 697194d WIP
```

#### Restore modifications
```
$ git stash apply stash@{0}
```

#### Clear stash list
```
git stash clear
```


### Discard changes
**DANGEROUS**
* Checks out the current index for the current directory.
* Undo unstaged changes in tracked files. It apparently doesn't touch staged changes and leaves untracked files alone.
```
git checkout .
```


### Git revert changes for file
```
git checkout -- filename
```

### Unstage commit
`git reset filepath`

### Undo commits
*Permanently*
* Reset your head to HEAD
`git reset --hard`
* Reset your head to wherever you want to be
`git reset --hard <the sha1 hash>`

*Not permanent*

`git reset HEAD~1`

### See branch status
#### See what branch you're on and if it's synchronized or not
```
git branch -v --color
```
### Check commmits ahead of current branch
```
git cherry -v
```


#### others

```
git log --graph --decorate --pretty=oneline --abbrev-commit --all @{upstream}^..
```

### Export commits as patches
#### Export last n patches
```
$ git format-patch -4
0001-some-commit.patch
0002-some-other-commit.patch
0003-again-committing.patch
0004-first-commit.patch
```
#### Export last n commits as a single patch
Just add the --stdout option
```
$ git format-patch -4 --stdout > `date +"%Y%m%d%H%M"`.patch
```

### View changes made to a file with source
```$ git log -p path/to/file```

### Filter commits by author
```
git log --author john.doe
```

### Making git "forget" about a file that was tracked but is now in .gitignore

_gitignore_ will prevent untracked files from being added (without an add -f) to the set of files tracked by git, however git will continue to track any files that are already being tracked.
To stop tracking a file you need to remove it from the index. This can be achieved with this command.

`$ git rm --cached <file>`

The removal of the file from the head revision will happen on the next commit.
Making git "forget" about a file that was tracked but is now in _.gitignore_

### Git revert changes for file
```
git checkout -- filename
```

### Unstage commit
`git reset filepath`

### Undo commits
*Permanently*

`git reset --hard`

*Not permanent*

`git reset HEAD~1`


### [Rearrange commits](http://stackoverflow.com/a/18308435)

```

I've used another way for a few times. In fact, it is a manual git rebase -i and it is useful when you want to rearrange several commits including squashing or splitting some of them. The main advantage is that you don't have to decide about every commit's destiny at a single moment. You'll also have all Git features available during the process unlike during a rebase. For example, you can display the log of both original and rewritten history at any time, or even do another rebase!

I'll refer to the commits in the following way, so it's readable easily:

C # good commit after a bad one
B # bad commit
A # good commit before a bad one
Your history in the beginning looks like this:

x - A - B - C
|           |
|           master
|
origin/master
We'll recreate it to this way:

x - A - B*- C'
|           |
|           master
|
origin/master
This is the procedure:

git checkout B       # get working-tree to the state of commit B
git reset --soft A   # tell git that we are working before commit B
git checkout -b rewrite-history   # switch to a new branch for our alternative history
Improve your old commit using git add (git add -i, git stash etc.) now. You can even split your old commit into two or more.

git commit           # recreate commit B (result = B*)
git cherry-pick C    # copy C to our new branch (result = C')
Intermediate result:

x - A - B - C
|    \      |
|     \     master
|      \
|       B*- C'
|           |
|           rewrite-history
|
origin/master
Let's finish:

git checkout master
git reset --hard rewrite-history  # make this branch master
That's it, you can push your progress now.
```

### [Rewrite history](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)


### Ignore subsequent changes to a file without deleting it
```
git update-index --skip-worktree path/to/file.cfg
```

### Show last two commits
```
git log -2 --stat
```

### Move committed but unpushed changes to another branch
From [here](https://stackoverflow.com/a/7217912)
```bash
git checkout branch # to checkout the feature branch.
git reset --hard master # to move the branch to be the same commit asmaster right now. By doing this, you lose all commits that are in the branch. Because of your rebase, all those commits should have copies onmaster, so you shouldn't actually lose anything.
git checkout master # to checkout master.
git reset --hard origin/master # to reset master to the state that ison the origin repo. This assumes you didn't have any unpushed changes to master. If you do, replace origin/master with the commit id you wantto reset to.
```

### Rename a local and remote branch

```bash
## 1. Rename your local branch.
## If you are on the branch you want to rename:
$ git branch -m new-name
## If you are on a different branch:
$ git branch -m old-name new-name
## 2. Delete the old-name remote branch and push the new-name local branch.
$ git push origin :old-name new-name
## 3. Reset the upstream branch for the new-name local branch.
## Switch to the branch and then:
$ git push origin -u new-name
```

### Delete remote branch
```bash
$ git push <remote_name> --delete <branch_name>
```
or
```bash
$ git push <remote_name> :<branch_name>
```

### Cherry picking
*extracted from (here)[https://www.previousnext.com.au/blog/intro-cherry-picking-git]*
Supposing there's a branch, `feature/killah-branch` with the following commits
```
d467740 some killer feature
2538f9f some nasty bug fixed
b60f122 le commit pour le commit
```

and want to apply the commit that fixes a nasty bug (id: `2538f9f`) from that branch in another branch, `feature/thenextbigthing`.

Go to the `feature/thenextbigthing` branch
```
$ git checkout `feature/thenextbigthing`
```
then, cherry pick the commit
```
$ git cherry-pick 2538f9f
```
You can cherry pick more than one commit (separate by space the list of commits)

### Push uncreated (remotelly) branch
```
    git push -u origin feature_branch_name
```

### save stash by name

```
    git stash save -u  "good testing"

```
### list stash

```
$ git stash list
stash@{0}: On FEAT/JIRA_FEATURE-530: good testing
```


### apply stash by index

```
git stash apply --index stash@{0}
```

### delete stash by index

```
git stash drop stash@{0}
```

### Rewrite url to use ssh instead of https
```
git config --global url."git@github.com:".insteadOf "https://github.com/"
```

More info [here](https://gist.github.com/patsancu/07b9fc503675392c6b99cefa7584c28a)

### Alias for github
```
git config --global url."git://github.com/".insteadOf gh:
git clone gh:patsancu/wiki.git
```

### Change commit date
Set the date of an arbitrary commit to an arbitrary or current date

* Rebase to before said commit and stop for amendment:
```
git rebase <commit-hash>^ -i
```
* Replace pick with e (edit) on the line with that commit (the first one)
quit the editor (ESC followed by :wq in VIM)
Either:
```
GIT_COMMITTER_DATE="$(date)" git commit --amend --no-edit --date "$(date)"
```
or
```
GIT_COMMITTER_DATE="Mon 20 Aug 2018 20:19:19 BST" git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"
```

Following any of these 2 options, you will want to run:
```
git rebase --continue
```

### Untrack files already added to git repository based on .gitignore
based on [this](https://web.archive.org/web/20191015080715/http://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/)
```
# If you wish to try what it does beforehand, add the -n or --dry-run flag to test things out.
git rm -r --cached .
```
```
git add .
```
```
git commit -m ".gitignore fix"
```
### Untrack a specific file
```
git rm --cached some_file.txt
```

### When pushing to some git server fails
Could happen that there are some server-side push rules. If after changing stuff in the commit, they're still failing, this might be worth a try
Taken from [here](https://stackoverflow.com/a/54108437)

```
# from feature branch
git branch backup                         # create backup branch
git reset --hard HEAD~1                   # remove the problem commit
git cherry-pick <SHA-1 of HEAD of backup> # cherry-pick back the commit
git push origin feature
```

### Update commmit date
In case you want to push the same commit with a different date (maybe to trigger pipeline?)
```
git commit --amend --no-edit --date=\"$(date -R)\"
```
