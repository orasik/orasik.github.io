---
title: "Testing the Go way - Day Two"
date: 2020-04-01T22:17:57+01:00
draft: true
categories:
  [go, test, concepts, cli, subtests, coverage, test, example, benchmark]
tags: [go, test, example, benchmark]
description: "Go testing, the Go way without using a testing framework. The lack of assert and the 4 types of functions"
---

In this article, I will explain how you can write a unit test the Go way using the standard unit test library that ships with Go.

### TL;DR

- Test package does not have `asserts`.
- You can use 4 types of functions, `TestXxx`, `BenchmarkXxx`, `Examplexxx` and `TestMain` where:
  - **TestXxx** with argument `t *testing.T` for unit testing functions. Example: **TestConfig(t \*testing.T)**
  - **BenchmarkXxx** with argument `b *testing.B` for benchmarking functions by running them inside a loop to determine the performance. Example: **BenchmarkConfig(b \*testing.B)**.
  - **Examplexxx** with no arguments which is which will be ran and verified based on output provided. Example: **ExampleConfig()**.
  - **TestMain** with `m *testing.M` argument for suppressing all testing functions and run own (details)?? //TODO: add example
- With table testing, you can run the test with multiple values and expected results to simplify and enrich the test.
- Running `go test` will cache the results and if you run it again it will pick results from cache unless you modified or added new tests. (validate)

### Go standard unittest library

Testing Go code using the standard library is different from other languages mainly due to the folder structure (more details [here](/posts/go-test-day-one/)) and the lack of `asserts` in the library.

The way Go does it is to check the value or result and raise an error or fatal if the value is not expected. You still can use logs to display more information if you like.

When testing, the test function **_must_** start with `Test` prefix and have `*testing.T` argument. Example:

```go
func TestNewFeature(t *testing.T) {
    result := MyFunction()

    if result != "valid" {
        t.Error("MyFunction result is not expected")
    }
}
```

If you like to format the error to include expected and actual values, you can use `t.Errorf`:

```go
func TestNewFeature(t *testing.T) {
    result := ToUppercase(" Hello world    ")

    if result != "valid" {
        t.Errorf("MyFunction result is not expected. Expected is %s, actual is %s", "valid", result)
    }
}
```

After the `Test` prefix you can use Capital letters or underscore but you can not use small letter. If you use small letter you'll get a warning in your IDE as below. If you decided to ignore the warning, this will not impact running other tests as `go test` command will just ignore this function.

Code:

```go
func TestnewFeature(t *testing.T) {
    result := ToUppercase(" Hello world    ")

    if result != "valid" {
        t.Errorf("MyFunction result is not expected. Expected is %s, actual is %s", "valid", result)
    }
}
```

Result in VSCode:

![VSCode warning for malformed test name](/images/day2-test-small-letters.png)

### Benchmarking

Benchmarking in Go will determine the performance of your function based on the machine running it. So don't mistake this performance for BigO notation for example. Results will vary from computer to another based on hardware and operating system.

```go
func BenchmarkToUpper(b *testing.B) {
	for i := 0; i < b.N; i++ {
		_ = ToUppercase(" ok hello ")
	}
}
```

This function will run `ToUppercase` for `N` times which will be determined by Go to run enough times to provide reliable results. Running the above on my PC with 8 core CPU running Ubuntu resulted in:

```
goos: linux
goarch: amd64
pkg: github.com/orasik/play
BenchmarkToUpper-8       6865275               146 ns/op
PASS
```

which means the loop ran **6865275** times with average of **146 nano second** per iteration.

//TODO: more about benchmark

### Example

Using `Examples` is a great way to document functions with input and output. Having a comment inside `Example` function with `//Output:`, go test will run it and verify the result with that comment. Let's have an example to make it clearer:

```go
func ExampleToUppercase() {
	ToUppercase("  Hello World  ")
	fmt.Println(ToUppercase("  Hello World  "))
	fmt.Println("Example of using ToUppercase")
	//Output:
	// HELLO WORLD
	// Example of using ToUppercase
}
```

then run the command:

```bash
go test -run Example -v
=== RUN   ExampleToUppercase
--- PASS: ExampleToUppercase (0.00s)
PASS
ok      github.com/orasik/play  0.003s
```

What happend here is `go test` did run the code in `ExampleToUppercase` and checked the output of `fmt.Println` and validated it with comments after **Output**. When the output matched these comments, the test passed. Now try to change the second line of the comment and run the test again, what do you get?

```go
func ExampleToUppercase() {
	ToUppercase("  Hello World  ")
	fmt.Println(ToUppercase("  Hello World  "))
	fmt.Println("Example of using ToUppercase")
	//Output:
	// HELLO WORLD
	// Something Else
}
```

then run the command:

```bash
go test -run Example -v
=== RUN   ExampleToUppercase
--- FAIL: ExampleToUppercase (0.00s)
got:
HELLO WORLD
Example of using ToUppercase
want:
HELLO WORLD
Something Else
FAIL
exit status 1
```

There is another keyword that can be used in `Examples` which is **Unordered output**. This can be used when you know what to expect but don't know the order. Example of this would be printing key->value of a map. Example:

```go
func ExampleMap() {
	values := make(map[string]string)

	values["name1"] = "Name 1"
	values["name2"] = "Name 2"
	values["name3"] = "Name 3"
	values["name4"] = "Name 4"

	for key, value := range values {
		fmt.Printf("%s=>%s\n", key, value)
	}

	// Unordered output:
	// name1=>Name 1
	// name4=>Name 4
	// name2=>Name 2
	// name3=>Name 3
}
```

Output:

```
go test -run ExampleMap -v
=== RUN   ExampleMap
--- PASS: ExampleMap (0.00s)
PASS
ok      github.com/orasik/play  0.003s
```

# To write about:

- Table testing.
- Internal testing (with examples and cases why would we need this).
- Test with VSCode.
- Test Debug with VSCode.
- Test caching.
- Benchmark
- TestMain
