# Git Tips & Tricks

## Keep a fork up to date

```
git remote add upstream git@github.com:some_user/some_repo.git
git checkout master
git fetch upstream
git rebase upstream/master
git push
```

## Dev flow on a fork

```
git checkout -b feature-x
#some work and some commits happen
#some time passes
git fetch upstream
git rebase upstream/master
git push origin feature-x
```

## Rebasing a fork branch on upstream

```
git pull --rebase upstream master
```

This is similar but slightly differnt from

```
git fetch upstream
git rebase upstream master
```

## Work directly on an upstream branch

```
git checkout -b upstream upstream/master
```

## Force a fork's branch in sync with upstream

```
git remote add upstream git@github.com:some_user/some_repo.git
git fetch upstream
git checkout master
git reset --hard upstream/master  
git push origin master --force
```

## Checking out and working with Pull Requests

https://github.com/TeamPorcupine/ProjectPorcupine/wiki/How-to-Test-a-Pull-Request

```
git config --global --add alias.pr '!f() { git fetch -fu ${2:-upstream} refs/pull/$1/head:pr/$1 && git checkout pr/$1; }; f'

git config --global --add alias.pr-clean '!git checkout master ; git for-each-ref refs/heads/pr/* --format="%(refname)" | while read ref ; do branch=${ref#refs/heads/} ; git branch -D $branch ; done'
```

https://help.github.com/articles/checking-out-pull-requests-locally/  
https://gist.github.com/piscisaureus/3342247
