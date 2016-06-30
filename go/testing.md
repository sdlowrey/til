_If your Go project uses Travis for CI, look at the .travis.yml file to see how tests are run._

You are working with an existing Go project created by someone else and you want to run/develop unit tests.

First, just try `go test` and see how that goes.

If the project uses vendoring, try `go test $(go list ./... | grep -v '/vendor/')`.

If the `check.v1` package is required, `go get gopkg.in/check.v1`

Since check.v1 is the bomb, you can select a specific test to run and get verbose output.

```
go test -check.v -check.f ControlSuite
```

The `check.f` option accepts regular expressions.

Use `-check.vv` for more verbosity.
