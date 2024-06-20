# GO

## Compiled vs Interpreted

- go runtime - automated memory management - a code, in every executable binary, that will cleanup the unused memory

  Computers need machine code, they don't understand English or even Go. We need to convert our high-level (Go) code into machine language, which is really just a set of instructions that some specific hardware can understand. In your case, your CPU.

  The Go compiler's job is to take Go code and produce machine code. On Windows, that would be a .exe file. On Mac or Linux, it would be any executable file. The code you write in your browser here on Boot.dev is being compiled for you on Boot.dev's servers, then the machine code is executed in your browser as Web Assembly.

- package main lets the Go compiler know that we want this code to compile and run as a standalone program, as opposed to being a library that's imported by other programs.
- func main() defines the main function. main is the name of the function that acts as the entry point for a Go program.

You can run a compiled program without the original source code. You don't even need a compiler. For example, when your browser executes the code you write in this course, it doesn't use the original code, just the compiled executable.

- main.go -> go build -> program.exe where it can be run anywhere

This is different than interpreted languages like Python and JavaScript. With Python and JavaScript, the code is interpreted at _runtime_ by a separate program known as the "interpreter". Distributing code for users to run can be a pain because they need to have an interpreter installed, and they need access to the source code.

- node is javascript runtime
- python is python runtime

## GO is strongly typed

One of the biggest benefits of strong typing is that errors can be caught at "compile time". In other words, bugs are more easily caught ahead of time because they are detected when the code is compiled before it even runs.

- you can use + to concate string because its strongly typed

## GO is lightweighted

Go programs are fairly lightweight. Each program includes a small amount of "extra" code that's included in the executable binary. This extra code is called the _Go Runtime_. One of the purposes of the Go runtime is to clean up unused memory at runtime.

## GO number type

The size (8, 16, 32, 64, 128, etc) represents how many bits in memory will be used to store the variable. The "default" int and uint types refer to their respective 32 or 64-bit sizes depending on the environment of the user.

```go
int int8  int16  int32  int64 // whole numbers

uint uint8 uint16 uint32 uint64 uintptr // positive whole numbers

float32 float64 // decimal numbers

complex64 complex128 // imaginary numbers (rare)
```

## GO const

Constants must be known at compile time. They are usually declared with a static value

However, constants can be computed as long as the computation can happen at compile time.

```go
// this is valid
const firstName = "Lane"
const lastName = "Wagner"
const fullName = firstName + " " + lastName

// this break
const now = time.Now() // it needs to be compiling in order to assign value
```

## GO Formatting String

Go follows the printf tradition from the C language. In my opinion, string formatting/interpolation in Go is less elegant than Python's f-strings, unfortunately.

```go
    fmt.Printf("String") // Prints a formatted string to standard out.
    fmt.Sprintf("String") // Returns the formatted string
```

### Representation

- %v = value
- %s = string
- %d = integer
- %.xf = float with x decimal places

## GO if else statement

```go
if INITIAL_STATEMENT; CONDITION {
  // do something
}

length := getLength(email)
if length < 1 {
    fmt.Println("Email is invalid")
}
// we can do
// shorter and we don't have to declare length
if length := getLength(email); length < 1 {
    fmt.Println("Email is invalid")
}
```

## GO struct

### When should you use an anonymous struct?

In general, prefer named structs. Named structs make it easier to read and understand your code, and they have the nice side-effect of being reusable. I sometimes use anonymous structs when I know I won't ever need to use a struct again. For example, sometimes I'll use one to create the shape of some JSON data in HTTP handlers.

If a struct is only meant to be used once, then it makes sense to declare it in such a way that developers down the road won’t be tempted to accidentally use it again.

```go
type car struct {
  make string
  model string
  doors int
  mileage int
  // wheel is a field containing an anonymous struct
  wheel struct {
    radius int
    material string
  }
}
```

### Embedded Struct

```go
type car struct {
  make string
  model string
}

type truck struct {
  // "car" is embedded, so the definition of a
  // "truck" now also additionally contains all
  // of the fields of the car struct
  car
  bedSize int
}
```

### Struct Method

A receiver is just a special kind of function parameter. Receivers are important because they will, as you'll learn in the exercises to come, allow us to define interfaces that our structs (and other types) can implement.

```go
type rect struct {
  width int
  height int
}

// area has a receiver of (r rect)
func (r rect) area() int {
  return r.width * r.height
}

var r = rect{
  width: 5,
  height: 10,
}

fmt.Println(r.area())
// prints 50
```

## GO Interface

Interfaces are just collections of method signatures. A type "implements" an interface if it has methods that match the interface's method signatures.

In the following example, a "shape" must be able to return its area and perimeter. Both rect and circle fulfill the interface.

> interfaces are collections of method signatures. A type "implements" an interface if it has all of the methods of the given interface defined on it.

> there is no keyword indicated that this type implements this interface in GO unlike JAVA

```go
type shape interface {
  area() float64
  perimeter() float64
}

type rect struct {
    width, height float64
}
func (r rect) area() float64 {
    return r.width * r.height
}
func (r rect) perimeter() float64 {
    return 2*r.width + 2*r.height
}

type circle struct {
    radius float64
}
func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perimeter() float64 {
    return 2 * math.Pi * c.radius
}
```

### GO Type Assertion

Type assertions in Go

When working with interfaces in Go, every once-in-awhile you'll need access to the underlying type of an interface value. You can cast an interface to its underlying type using a type assertion.

In the example below:

- we want to check if s is a circle in order to cast it into its underlying concrete type
- we know s is an instance of the shape interface, but we do not know if it's also a circle
- c is a new circle struct cast from s
- ok is true if s is indeed a circle, or false if s is NOT a circle

```go
type shape interface {
	area() float64
}

type circle struct {
	radius float64
}

c, ok := s.(circle)
if !ok {
	// log an error if s isn't a circle
	log.Fatal("s is not a circle")
}

radius := c.radius
```

A type switch makes it easy to do several type assertions in a series.

A type switch is similar to a regular switch statement, but the cases specify types instead of values.

```go
func printNumericValue(num interface{}) {
  switch v := num.(type) {
  case int:
    fmt.Printf("%T\n", v)
  case string:
    fmt.Printf("%T\n", v)
  default:
    fmt.Printf("%T\n", v)
  }
}

func main() {
  printNumericValue(1)
  // prints "int"

  printNumericValue("1")
  // prints "string"

  printNumericValue(struct{}{})
  // prints "struct {}"
}
```

### Clean Interface

Writing clean interfaces is hard. Frankly, anytime you’re dealing with abstractions in code, the simple can become complex very quickly if you’re not careful. Let’s go over some rules of thumb for keeping interfaces clean.

1. Keep Interfaces Small

```go
type File interface {
    io.Closer
    io.Reader
    io.Seeker
    Readdir(count int) ([]os.FileInfo, error)
    Stat() (os.FileInfo, error)
}
```

2. Interfaces Should Have No Knowledge of Satisfying Types

```go
// don't do this
type car interface {
  Color() string
  Speed() int
  IsFiretruck() bool
}

// do this
type firetruck interface {
  car
  HoseLength() int
}
```

3. Interfaces Are Not Classes

> [Best Interface Practice](https://blog.boot.dev/golang/golang-interfaces/?_gl=1*1s3zsib*_gcl_au*MTQwMzMxODE1NS4xNzE4ODUyMzky*_ga*MTM2NzExOTUzOC4xNzE4ODUyMzk1*_ga_M7P2PBGN8N*MTcxODg2MTkwNS4yLjEuMTcxODg3MzQxNi42MC4wLjA.)

- Interfaces are not classes, they are slimmer.
- Interfaces don’t have constructors or deconstructors that require that data is created or destroyed.
- Interfaces aren’t hierarchical by nature, though there is syntactic sugar to create interfaces that happen to be supersets of other interfaces.
- Interfaces define function signatures, but not underlying behavior. Making an interface often won’t DRY up your code in regards to struct methods. For example, if five types satisfy the fmt.Stringer interface, they all need their own version of the String() function.
