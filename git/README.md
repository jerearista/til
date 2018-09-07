# Git Tips & Tricks

## Keep a fork up to date

```
git remote add upstream git@github.com:some_user/some_repo.git
git fetch upstream
git rebase upstream/master
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
