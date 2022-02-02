# Git Pull To A Bare Repo

Bare [git](../what/git.md) repos are needed when you want to push to
a repo. If you have a home-lab, there is a good chance that you
have a bunch of bare repos sitting on a node somewhere.

When in a bare repo, you cannot `git pull` into it, because `git pull`
only works on non-bare repos. Instead you have to do `git fetch --all`.
This does fetch any commits from github/upstream, but if you do a
`git log` you will see that the history has not changed. This is because
the `HEAD` pointer has not changed. The changes you fetched, are pointed
to by the `FETCH_HEAD` pointer. To see the new changes in your history
you have to update the `HEAD` to point to `FETCH_HEAD`, via

```
git update-ref HEAD FETCH_HEAD
```

So the full sequence is

```
git fetch --all
git update-ref HEAD FETCH_HEAD
```