---
title: "Go Test - Day One"
date: 2020-03-30T06:03:28+01:00
categories: [go, test, concepts, cli, subtests, coverage, skipping]
tags: [go, test]
description: "Go test, how to, cli options, coverage and essential information about testing in Go lang"
draft: true
---

In this post, I wil start with essential information about Go test for those who are new to Go or can be just a refresher about Go testing.

To start, there are a hard requirements for writing Go tests:

- Test file name `should` have `_test` suffix. For example: `config_test.go`.
- Test file `should` be in the same folder (package) of the function to be tested.
- Test function `should` start with `Test` prefix as `TextXxx` where first letter of `Xxx` can not be a small letter, for example: `func TestValidConfig(t *testing.T)` or `func Test_Missing_Values(t \*testing.T).
- Test function `should` have the `t *testing.T` argument. (Explain why).
- Test file package `can` be the same as function package if you're testing internal functions but `preferred` to be `package_test`. If you're testing `config` package then the package in test file should be `config_test` unless there is a private function in test where you can not call from external package then you can use `config` package inside the test file.

## Some concepts regarding testing in Go.

### Go test cli options

1. To run the test for the current package (folder) you can use `.`

```bash
go test .
```

2. If you want to display verbose information about tests, you can use the `-v` flag:

```bash
go test . -v
```

3. To run the test for just a function, you can use regex in test command:

```bash
go test -run ToUpper
```

This will run the tests for `ToUppercase` function only. Now if you want to run just a sub tests matching a string you can use:

```bash
go test -run Upper/Leading
```

This will run just subtests for `ToUppercase` function. The output of the previous command for the test mentioned above will be:

```
=== RUN   TestToUpper
=== RUN   TestToUpper/Leading_Space_string
=== RUN   TestToUpper/Leading_Space_string#01
--- PASS: TestToUpper (0.00s)
    --- PASS: TestToUpper/Leading_Space_string (0.00s)
    --- PASS: TestToUpper/Leading_Space_string#01 (0.00s)
PASS
ok      github.com/orasik/play  0.003s
```

### Skipping

To skip a test, you can use `t.Skip()` with a flag condition like env variable or `Short` flag:

Example of using env variable:

```bash
export SKIP_TESTS=true && go test .
```

Go code:

```go
func TestNewFeature(t *testing.T) {
  if os.Getenv("SKIP_TESTS") != "" {
    t.Skip("Skipping testing")
  }
}

```

or with `Short` flag:

```bash
go test ./... -test.short
```

Go code:

```go
func TestTimeConsuming(t *testing.T) {
    if testing.Short() {
        t.Skip("skipping test in short mode.")
    }
    ...
}
```

### Subtests

Sometimes writing many testing functions can lead to lots of duplicates in mock data or verbose output so you might want to write a function and have subtests inside. For example, if you want to test a function that takes a string and return it upper case, you want to check if the function can take white space in the begining or end of string so rather than writing 3 functions to check:

- Leading white space.
- Trailing white space.
- Both

You can write one function to test white spaces and have a sub test for each case.

Example:

```go
func ToUppercase(s string) string {
	return strings.ToUpper(strings.Trim(s, " "))
}


func TestToUpper(t *testing.T) {
	t.Run("Leading Space string", func(t *testing.T) {
		if ToUppercase(" hello") != "HELLO" {
			t.Error("ToUpper failed with leading whitespace")
		}
	},
	)

	t.Run("Trailing Space string", func(t *testing.T) {
		if ToUppercase("hello ") != "HELLO" {
			t.Error("ToUpper failed with trailing whitespace")
		}
	},
	)

	t.Run("Leading Space string", func(t *testing.T) {
		if ToUppercase(" hello  ") != "HELLO" {
			t.Error("ToUpper failed leading and trailing whitespace")
		}
	},
	)
}

```

and output when you run `go test . -v` will be:

```
=== RUN   TestToUpper
=== RUN   TestToUpper/Leading_Space_string
=== RUN   TestToUpper/Trailing_Space_string
=== RUN   TestToUpper/Leading_Space_string#01
--- PASS: TestToUpper (0.00s)
    --- PASS: TestToUpper/Leading_Space_string (0.00s)
    --- PASS: TestToUpper/Trailing_Space_string (0.00s)
    --- PASS: TestToUpper/Leading_Space_string#01 (0.00s)
PASS
ok      github.com/orasik/play  0.001s
```

### Logging during tests

To display logs of running tests you can use `t.Log` or `t.Logf` methods. Examples:

```go
func TestNewFeature(t *testing.T) {
  t.Log("Staring the NewFeature test")
  ...
  t.Logf("Finished runn %d tests", 5)
}
```

### Generating test coverage

To create a coverage profile that you can view later, you can specify coverage file using `go test` command:

```bash
go test . -v -coverprofile=app.out
```

Now to view that coverage in html format, you can use `go tool`:

```bash
go tool cover -html=cp.out
```

Or to view the coverage percentage of each function you can use:

```bash
go tool cover -func app.out
```

### Resources

[Go Test package](https://golang.org/pkg/testing/)

[Go Unit Tests: Tips from the Trenches](https://www.red-gate.com/simple-talk/dotnet/software-testing/go-unit-tests-tips-from-the-trenches/)
