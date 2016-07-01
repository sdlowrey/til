# Managing Go Dependencies

This world is fraught with peril. Run the wrong command at the wrong time and shit gets really confusing.

## Commands to run.

Use Go 1.6 or later.  If you using 1.5 or earlier, then set the experimental vendoring environment variable.

An accepted plan (where I work now anyway) is to do this when setting or resetting dependencies:

```
godep update ./...
godep save ./...
godep update ./...
```

Do this when you have tested your changes and things are working the way you want.  Be prepared to revert the changes -- `git diff` will give you an overview.

Running `godep save ./...` will update the `vendor/` tree to use the current versions (in your src tree) of all the libs your project depends on.  So be mindful of what repos are checked out, what version they are at, and whether you have modified any of them.  

Check to see what has changed in `Godeps/Godeps.json` after you run any `godep` command.  You can see what has changed and make sure nothing unexpected got pulled in.

If you see a gigantic new dependency in `golang.org\x`. This has something to do with pulling in "transitive dependencies" and (maybe) has something to do with cross-platform builds.  Anyway, you can remove that directory from `vendor/` and from `Godeps.json` manually.  The build should still on Travis or wherever.
