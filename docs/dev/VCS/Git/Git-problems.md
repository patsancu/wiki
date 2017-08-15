### not something we can merge

```
git checkout branch-name
git checkout master
git merge branch-name
```

### git is pushing with an unexpected user/email
According to the github [docs](https://help.github.com/articles/setting-your-commit-email-address-in-git/), GitHub uses the email address set in your local Git configuration to associate commits pushed from the command line with your GitHub account.
* Check values from
```bash
git config -l
```
* Check
```bash
git config --global -l
```
* Check
Check host from
```bash
vim ~/.ssh/config
```
and compare it with the one in the repo push/fetch url at
```bash
.git/config
```
