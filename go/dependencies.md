# Managing Go Dependencies

This world is fraught with peril. Run the wrong command at the wrong time and shit gets really confusing.

Use Go 1.6 or later.  If you using 1.5 or earlier, then set the experimental vendoring environment variable.

## Updating a Single Dependency

From the help text:

```
Update changes the named dependency packages to use the
revision of each currently installed in GOPATH. New code will
be copied into the Godeps workspace or vendor folder and the
new revision will be written to the manifest.
```

That's why it's probably not best to do a blanket update by specifying `./...` in an update. If a dependent project is in a state other than what it was when saved, you might not want it updated.

If you want to update just the `coolstuff/project` dependency:

`godep update github.com/coolstuff/project/...`

## Nested Vendor Directories

After doing any kind of update, run `godep save ./...`.

You will probably see a ton of `godep: rewrite:` lines but that's OK. Run 'git status' to verify that nested `vendor` directories were removed.

## Changed Repo Names

If a dependent repo has its name changed, here's how to deal with projects that depend on it.

First, the renamed project should be checked out to a tagged commit that indicates the latest release.

In the dependent project:

1. create a feature branch
2. in the code, change the name of the imported project wherever necessary
3. `go install ./...` _this will probably fail_
4. remove old-name project references from the manifest file `Godeps/Godeps.json`
5. `go install ./...` _failures here may point to type mismatches in the type path due to vendored code in other projects_
6. `godep save ./...` _this will reanalyze deps and save to `vendor`_
7. again, `go install ./...` _to verify_

## CAUTION: Older Notes

An accepted plan (where I work now anyway) is to do this when setting or resetting dependencies:

_Update: `godep update ./...` is discouraged unless you're sure all your dependent projects checked out to a state you want._

```
godep update ./...
godep save ./...
godep update ./...
```

Do this when you have tested your changes and things are working the way you want.  Be prepared to revert the changes -- `git diff` will give you an overview.

Running `godep save ./...` will update the `vendor/` tree to use the current versions (in your src tree) of all the libs your project depends on.  So be mindful of what repos are checked out, what version they are at, and whether you have modified any of them.  Remember to checkout a _tag_ of a dependent repo, if possible.  Godep seems to understand that better than, say, being at the head of a branch like `develop`. Dunno why.

Check to see what has changed in `Godeps/Godeps.json` after you run any `godep` command.  You can see what has changed and make sure nothing unexpected got pulled in.

If you see a gigantic new dependency in `golang.org\x`. This has something to do with pulling in "transitive dependencies" and (maybe) has something to do with cross-platform builds.  Anyway, you can remove that directory from `vendor/` and from `Godeps.json` manually.  The build should still on Travis or wherever.
