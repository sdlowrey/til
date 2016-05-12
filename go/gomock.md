Super useful, super annoying to work with.  Using the sketchy docs provided, I'll run thru a small test based on the examples.

Assume Go is set up and working.  Create a new sandbox dir in the src directory and cd to it.

```
go get github.com/golang/mock/gomock
go get github.com/golang/mock/mockgen
```

Create a Go source file called `interface.go` with some toy interface in it.

Run `mockgen -source interface.go -package main > mock_interface.go`.

The `-package` option should be set to whatever library it should belong to (normally not `main` but OK here).
