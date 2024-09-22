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

## Anonymous struct?

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

## Embedded Struct

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

## Struct Method

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

## GO For Loop

### Infinite Loop

```go
for INITIAL; ; AFTER {
  // do something forever
}
```

### There is no while loop in Go

Most programming languages have a concept of a while loop. Because Go allows for the omission of sections of a for loop, a while loop is just a for loop that only has a CONDITION.

```go
plantHeight := 1
for plantHeight < 5 {
  fmt.Println("still growing! current height:", plantHeight)
  plantHeight++
}
fmt.Println("plant has grown to ", plantHeight, "inches")
```

### Continue Keyword

The continue keyword stops the current iteration of a loop and continues to the next iteration. continue is a powerful way to use the guard clause pattern within loops.

```go
for i := 0; i < 10; i++ {
  if i % 2 == 0 {
    continue
  }
  fmt.Println(i)
}
// 1
// 3
// 5
// 7
// 9
```

### Break Keyword

The break keyword stops the current iteration of a loop and exits the loop.

```go
for i := 0; i < 10; i++ {
  if i == 5 {
    break
  }
  fmt.Println(i)
}
// 0
// 1
// 2
// 3
// 4
```

## Array

- Arrays are fixed-size groups of variables of the same type.
- The type [n]T is an array of n values of type T
- To declare an array of 10 integers:

```go
var myInts [10]int
primes := [6]int{2, 3, 5, 7, 11, 13}
```

## Slice

- 99 times out of 100 you will use a slice instead of an array when working with ordered lists.
- Arrays are fixed in size. Once you make an array like [10]int you can't add an 11th element.
- A slice is a dynamically-sized, flexible view of the elements of an array.

```go
primes := [6]int{2, 3, 5, 7, 11, 13}
mySlice := primes[1:4]
// mySlice = {3, 5, 7}
```

### Make

Most of the time we don't need to think about the underlying array of a slice. We can create a new slice using the make function:

- Slices created with make will be filled with the zero value of the type.

```go
// func make([]T, len, cap) []T
mySlice := make([]int, 5, 10)

// the capacity argument is usually omitted and defaults to the length
mySlice := make([]int, 5)
```

### Variadic

- Many functions, especially those in the standard library, can take an arbitrary number of final arguments. This is accomplished by using the "..." syntax in the function signature.
- A variadic function receives the variadic arguments as a slice.

```go
func concat(strs ...string) string {
    final := ""
    // strs is just a slice of strings
    for i := 0; i < len(strs); i++ {
        final += strs[i]
    }
    return final
}

func main() {
    final := concat("Hello ", "there ", "friend!")
    fmt.Println(final)
    // Output: Hello there friend!
}
```

### Spread Operator

- The spread operator allows us to pass a slice into a variadic function. The spread operator consists of three dots following the slice in the function call.

```go
// strings is []string
func printStrings(strings ...string) {
  for i := 0; i < len(strings); i++ {
    fmt.Println(strings[i])
  }
}

func main() {
  names := []string{"bob", "sue", "alice"}
  printStrings(names...)
}
```

### Append

- The built-in append function is used to dynamically add elements to a slice:

```go
slice = append(slice, oneThing)
slice = append(slice, firstThing, secondThing)
slice = append(slice, anotherSlice...)

// dont do this!
someSlice = append(otherSlice, element)

// to avoid bugs like this, you should always use the append function
// on the same slice the result is assigned to

// do this instead
mySlice := []int{1, 2, 3}
mySlice = append(mySlice, 4)
```

### Range

```go
fruits := []string{"apple", "banana", "grape"}
for i, fruit := range fruits {
    fmt.Println(i, fruit)
}
// 0 apple
// 1 banana
// 2 grape
```

## GO Map

- Maps are similar to JavaScript objects, Python dictionaries, and Ruby hashes. Maps are a data structure that provides key->value mapping.
- The zero value of a map is nil.
- We can create a map by using a literal or by using the make() function:

```go
ages := make(map[string]int)
ages["John"] = 37
ages["Mary"] = 24
ages["Mary"] = 21 // overwrites 24

ages = map[string]int{
  "John": 37,
  "Mary": 21,
}
```

We can speed up our contact-info lookups by using a map!

- Key-based map lookup: O(1)
- Slice brute-force search: O(n)

### GO Mutation

```go
\\ insert
\\ if not exist, get zero value type
m[key] = elem

\\ get element
elem = m[key]

\\ delete
delete(m, elem)

\\ check if exist
\\ ok is true if existed, otherwise
elem, ok := m[key]
```

## High Order Function

- A function that returns a function or accepts a function as input is called a Higher-Order Function.
- Go supports first-class and higher-order functions. Another way to think of this is that a function is just another type -- just like ints and strings and bools.

```go
func add(x, y int) int {
  return x + y
}

func mul(x, y int) int {
  return x * y
}

// aggregate applies the given math function to the first 3 inputs
func aggregate(a, b, c int, arithmetic func(int, int) int) int {
  return arithmetic(arithmetic(a, b), c)
}

func main() {
  fmt.Println(aggregate(2,3,4, add))
  // prints 9
  fmt.Println(aggregate(2,3,4, mul))
  // prints 24
}
```

## Currying

- Function currying is a concept from functional programming and involves partial application of functions. It allows a function with multiple arguments to be transformed into a sequence of functions, each taking a single argument.

- Although Go does not support full currying, it is possible to simulate this behavior. By designing functions that take other functions as inputs and return new functions, we can achieve a similar effect.

For example:

```go
func main() {
  squareFunc := selfMath(multiply)
  doubleFunc := selfMath(add)

  fmt.Println(squareFunc(5))
  // prints 25

  fmt.Println(doubleFunc(5))
  // prints 10
}

func multiply(x, y int) int {
  return x * y
}

func add(x, y int) int {
  return x + y
}

func selfMath(mathFunc func(int, int) int) func (int) int {
  return func(x int) int {
    return mathFunc(x, x)
  }
}

```

## Defer

- The defer keyword is a fairly unique feature of Go. It allows a function to be executed automatically just before its enclosing function returns.
- The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.
- Deferred functions are typically used to close database connections, file handlers and the like.

For example:

```go
// CopyFile copies a file from srcName to dstName on the local filesystem.
func CopyFile(dstName, srcName string) (written int64, err error) {

  // Open the source file
  src, err := os.Open(srcName)
  if err != nil {
    return
  }
  // Close the source file when the CopyFile function returns
  defer src.Close()

  // Create the destination file
  dst, err := os.Create(dstName)
  if err != nil {
    return
  }
  // Close the destination file when the CopyFile function returns
  defer dst.Close()

  return io.Copy(dst, src)
}
```

- In the above example, the src.Close() function is not called until after the CopyFile function was called but immediately before the CopyFile function returns.
- Defer is a great way to make sure that something happens at the end of a function, even if there are multiple return statements.

## Closures

- A closure is a function that references variables from outside its own function body. The function may access and assign to the referenced variables.
- In this example, the concatter() function returns a function that has reference to an enclosed doc value. Each successive call to harryPotterAggregator mutates that same doc variable.

```go
func concatter() func(string) string {
	doc := ""
	return func(word string) string {
		doc += word + " "
		return doc
	}
}

func main() {
	harryPotterAggregator := concatter()
	harryPotterAggregator("Mr.")
	harryPotterAggregator("and")
	harryPotterAggregator("Mrs.")
	harryPotterAggregator("Dursley")
	harryPotterAggregator("of")
	harryPotterAggregator("number")
	harryPotterAggregator("four,")
	harryPotterAggregator("Privet")

	fmt.Println(harryPotterAggregator("Drive"))
	// Mr. and Mrs. Dursley of number four, Privet Drive
}
```

## Anonymous Function

- Anonymous functions are true to form in that they have no name. We've been using them throughout this chapter, but we haven't really talked about them yet.
- Anonymous functions are useful when defining a function that will only be used once or to create a quick closure.

```go
// doMath accepts a function that converts one int into another
// and a slice of ints. It returns a slice of ints that have been
// converted by the passed in function.
func doMath(f func(int) int, nums []int) []int {
	var results []int
	for _, n := range nums {
		results = append(results, f(n))
	}
	return results
}

func main() {
	nums := []int{1, 2, 3, 4, 5}

    // Here we define an anonymous function that doubles an int
    // and pass it to doMath
	allNumsDoubled := doMath(func(x int) int {
	    return x + x
	}, nums)

	fmt.Println(allNumsDoubled)
    // prints:
    // [2 4 6 8 10]
}
```

## Pointer

- A pointer is a variable that stores the memory address of another variable. This means that a pointer "points to" the location of where the data is stored NOT the actual data itself.
- If a pointer points to nothing (the zero value of the pointer type) then dereferencing it will cause a runtime error (a panic) that crashes the program. Generally speaking, whenever you're dealing with pointers you should check if it's nil before trying to dereference it.
- Pointer receivers are more common than value receivers.

```go
// The * syntax defines a pointer:
var p *int

// The & operator generates a pointer to its operand.
myString := "hello"
myStringPtr := &myString

// pointer receiver
type car struct {
	color string
}

func (c *car) setColor(color string) {
	c.color = color
}

func main() {
	c := car{
		color: "white",
	}
	c.setColor("blue")
	fmt.Println(c.color)
	// prints "blue"
}
```

## Channel

- A send to nil channel is blocked forever
- A receive from nil channel is blocked forever also
- A send to closed channel panics
- A receive from closed channel return the zero value immediately

```go
// create channel
ch := make(chan int)

// assign value to var from channel
ch <- 69

// receive data from channel
v := <-ch
```

### Closing Channel

Channels can be explicitly closed by a sender:

```go
ch := make(chan int)

// do some stuff with the channel

close(ch)

// check if channel is closed
// ok will be false is empty and closed
v, ok := <-ch

```

### Range Channel

- This example will receive values over the channel (blocking at each iteration if nothing new is there) and will exit only when the channel is closed.

```go
for item := range ch {
    // item is the next value received from the channel
}
```

### Select Channel

- Sometimes we have a single goroutine listening to multiple channels and want to process data in the order it comes through each channel.
- A select statement is used to listen to multiple channels at the same time. It is similar to a switch statement but for channels.
- The first channel with a value ready to be received will fire and its body will execute. If multiple channels are ready at the same time one is chosen randomly. The ok variable in the example above refers to whether or not the channel has been closed by the sender yet.
- mostly come with infinite loop

```go
select {
case i, ok := <- chInts:
    fmt.Println(i)
case s, ok := <- chStrings:
    fmt.Println(s)
}
```

## GO Mutexes (Mutual Exclution)

- Mutexes allow us to lock access to data. This ensures that we can control which goroutines can access certain data at which time.
- Go's standard library provides a built-in implementation of a mutex with the sync.Mutex type and its two methods:

  - .Lock*()*
  - .Unlock()

- We can protect a block of code by surrounding it with a call to Lock and Unlock as shown on the protected() method below.
- It's good practice to structure the protected code within a function so that defer can be used to ensure that we never forget to unlock the mutex.

```go
mu := &sync.Mutex{}

func protected(){
    mu.Lock() // other thread cannot access
    defer mu.Unlock()
    // the rest of the function is protected
    // any other calls to `mu.Lock()` will block
    // just add mu.Lock() and defer mu.Unlock() then you should be fine.
}
```

- Maps are not thread-safe. In GO, it's not safe to write and read map at the same time.
- Maps are not safe for concurrent use! If you have multiple goroutines accessing the same map, and at least one of them is writing to the map, you must lock your maps with a mutex.

### RW Mutexes (Read and Write)

- Maps are safe for concurrent read access, just not concurrent read/write or write/write access. A read/write mutex allows all the readers to access the map at the same time, but a writer will still lock out all other readers and writers.
- By using a sync.RWMutex, our program becomes more efficient. We can have as many readLoop() threads as we want, while still ensuring that the writers have exclusive access.

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	m := map[int]int{}

	mu := &sync.RWMutex{}

	go writeLoop(m, mu)
	go readLoop(m, mu)
	go readLoop(m, mu)
	go readLoop(m, mu)
	go readLoop(m, mu)

	// stop program from exiting, must be killed
	block := make(chan struct{})
	<-block
}

func writeLoop(m map[int]int, mu *sync.RWMutex) {
	for {
		for i := 0; i < 100; i++ {
			mu.Lock()
			m[i] = i
			mu.Unlock()
		}
	}
}

func readLoop(m map[int]int, mu *sync.RWMutex) {
	for {
		mu.RLock()
		for k, v := range m {
			fmt.Println(k, "-", v)
		}
		mu.RUnlock()
	}
}
```

## Go Generic

### Type Parameter

- Put simply, generics allow us to use variables to refer to specific types. This is an amazing feature because it allows us to write abstract functions that drastically reduce code duplication.

```go
func splitAnySlice[T any](s []T) ([]T, []T) {
    mid := len(s)/2
    return s[:mid], s[mid:]
}
```

### Generic Type Constraints

```go
type stringer interface {
    String() string
}

func concat[T stringer](vals []T) string {
    result := ""
    for _, val := range vals {
        // this is where the .String() method
        // is used. That's why we need a more specific
        // constraint instead of the any constraint
        result += val.String()
    }
    return result
}
```

### Type List

```go
// Ordered is a type constraint that matches any ordered type.
// An ordered type is one that supports the <, <=, >, and >= operators.
type Ordered interface {
    ~int | ~int8 | ~int16 | ~int32 | ~int64 |
        ~uint | ~uint8 | ~uint16 | ~uint32 | ~uint64 | ~uintptr |
        ~float32 | ~float64 |
        ~string
}
```

### Generic Parameter Constraints

```go
// The store interface represents a store that sells products.
// It takes a type parameter P that represents the type of products the store sells.
type store[P product] interface {
	Sell(P)
}

type product interface {
	Price() float64
	Name() string
}

type book struct {
	title  string
	author string
	price  float64
}

func (b book) Price() float64 {
	return b.price
}

func (b book) Name() string {
	return fmt.Sprintf("%s by %s", b.title, b.author)
}

type toy struct {
	name  string
	price float64
}

func (t toy) Price() float64 {
	return t.price
}

func (t toy) Name() string {
	return t.name
}

// The bookStore struct represents a store that sells books.
type bookStore struct {
	booksSold []book
}

// Sell adds a book to the bookStore's inventory.
func (bs *bookStore) Sell(b book) {
	bs.booksSold = append(bs.booksSold, b)
}

// The toyStore struct represents a store that sells toys.
type toyStore struct {
	toysSold []toy
}

// Sell adds a toy to the toyStore's inventory.
func (ts *toyStore) Sell(t toy) {
	ts.toysSold = append(ts.toysSold, t)
}

// sellProducts takes a store and a slice of products and sells
// each product one by one.
func sellProducts[P product](s store[P], products []P) {
	for _, p := range products {
		s.Sell(p)
	}
}

func main() {
	bs := bookStore{
		booksSold: []book{},
	}

    // By passing in "book" as a type parameter, we can use the sellProducts function to sell books in a bookStore
	sellProducts[book](&bs, []book{
		{
			title:  "The Hobbit",
			author: "J.R.R. Tolkien",
			price:  10.0,
		},
		{
			title:  "The Lord of the Rings",
			author: "J.R.R. Tolkien",
			price:  20.0,
		},
	})
	fmt.Println(bs.booksSold)

    // We can then do the same for toys
	ts := toyStore{
		toysSold: []toy{},
	}
	sellProducts[toy](&ts, []toy{
		{
			name:  "Lego",
			price: 10.0,
		},
		{
			name:  "Barbie",
			price: 20.0,
		},
	})
	fmt.Println(ts.toysSold)
}
```
