Prerequisites are that Go is installed, GOPATH is set up, and you have some project in GitHub (or one of the supported repo types) that you want to work on.

For the sake of example, we'll say the GitHub account is `thedude` and the project is `bowling`.

To fetch the project code and all of its dependencies:

```
cd $GOPATH
go get github.com/thedude/bowling/...
```

Verify that $GOPATH/src has dependencies.

Now you can build and install this way

```
go install github.com/thedude/bowling
```

Or this way

```
cd github.com/thedude/bowling
go install ./...
```

Executables will land in `$GOPATH/bin` and libraries will be in `$GOPATH/pkg`.

If there is a specific sub-directory in the project that contains the source for an executable, you can build/install that directly. Say the command `roll` is built from the `roll` subdir. Just run `go install github.com/thedude/bowling\roll`.
