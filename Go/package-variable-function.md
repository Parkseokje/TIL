# Packages, variables and functions

## Download

In my case, installed `go1.14.darwin-amd64.pkg`

## Test your Installation

```bash
$ go build hello.go
$ ./hello

# hello, world
```

## Go tour

Go tour?

A guide program on how to use go.

```bash
$ go get golang.org/x/tour
```

After above command, you can find `tour` in go/bin/.
Double click to run.

## Tour > Basics > Packages, variables and functions.

### Packages

```go
package main

import (
  "fmt"
  "math/rand"
)

func main() {
  fmt.println(rand.Intn(10))
}
```

- Every Go program is made of packages.
- Programs start running in package `main`
- Imports can also be in multiple import statements.

  ```go
  import "fmt"
  import "math"
  ```

### Exported names

```go
fmt.Println(math.pi) // cannot refer to unexported name math.pi
fmt.Println(math.Pi) // 3.141592653589793
```

When importing a package, you can only accessible to its `Exported names`. Which begins with a capital letter i.e., Pi

### Functions

```go
// Basic
func add(x int, y int) int {
  return x + y
}

// You can omit the type if function parameters has same type
func add(x, y int) { ... }

// Multiple result
// Simply exchange the positions of x and y
func swap(x, y string) (string, string) {
  return y, x
}

func main() {
  a, b := swap("world", "hello")
  fmt.Println(a, b) // "Hello World"
}

// Named return values
func split(sum int) (x, y int) {
  x = sum * 4 / 9
  y = sum - x
  return
}

func main() {
  fmt.Println(split(17)) // 7 10
}
```

### Variables

```go
// A var statement can be at package or function level
var i, j bool
var some_var // don't use underscore in Go names; var some_var should be someVar

func main() {
  var i int
}

// Variables with initializers
var i, j int = 1, 2

// Short variable declarations
// := construct is not available outside a function
k := 3
```

### Basic types

```go
// Variable declaration can be "factored" into blocks like this
var (
  ToBe    bool = false
  MaxInt  uint = 1<<64 - 1
  z       complex128 = cmplx.Sqrt(-5 + 12i)
)
```

### Zero value

Variables declared without an explicit value are given intial value. this is called `zero`value.

```go
var i int
var f float64
var b bool
var s string
fmt.Printf("%v %v %v %q\n", i, f, b, s)
// 0 0 false ""
```

### Type conversions

The expression T(v) converts the value v to the type T.

```go
var x = 3

var y float64 = math.Sqrt(float64(x))
var z float64 = math.Sqrt(x) // cannot use x as typeof float64..
```

### Type inference

The variable's type is inferred from the value on the right hand side.

```go
i := 3 // becomes int
f := 3.14 // becomes float64
g := 0.993 + 0.5i // becomes complexx128
```

### Constants

Constant cannot be declared using `:=` syntax.

```go
const World = "世界"

// Numeric Constants (high-precision values)
const (
  Big = 1 << 100
)
```

## For more insights

https://golang.org/doc/install
