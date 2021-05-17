# Move a commit on master to a branch

You committed a change or two to master when you meant to make them on a branch. You want to move them to a branch so that head still matches the remote head.

If you already published (pushed) the changes to the remote (which shouldn't be allowed if you're on `master`) then your best bet is to use `revert`. 

**Be careful. You do not want to arbitrarily change commit history if any of the affected commits are shared with others. It will cause problems for them when they try to merge.**

If you haven't published  the changes yet, then it's simpler. Get the latest commit after the original HEAD that contain your changes

```
git log --oneline
916c802 (HEAD -> master) changes that should have been on a new branch
59f9923 (origin/master, origin/HEAD) Merge pull request #19 in myrepo from some-feature to master
f4c9882 add new pants
```

You want to create a branch based on `origin/HEAD` so:

```shell
git co -b newbranch 59f9923
```

Now you're on the new branch with the changes you made on master. You can push this to `origin` or wherever.

The errant commit is still on master though, so you need to remove that with a `reset`.

```shell
git reset --hard 59f9923
```
