# Data Type

Every variable in GO has type.

- Basic Types
- Composite Types

## Basic Type

### Integer

```go
Signed

  - int: Platform Dependent
  - int8: 8bits / 1 byte
  - int16: 16 bits/ 2 byte
  - int32: 32 bits/ 4 byte
  - int64: 64 bits/ 8 byte // for ex. time.Duration
  - // different in size
  - // selecting is dependent on the range needed
```

```go
Unsigned

  - uint
  - uint8
  - uint16
  - uint32
  - uint64
```

### Float

Number with decimal

```go
float32: 32 bits or 4 btyes
float64: 64 bits or 8 bytes
```

### Complex Number

can be initialized in 2 ways

```go
complext(a,b)
// or
a := 5 + 6i
```

### Byte

- alias for **uint8**
- represent ASCII

### Rune

- alias for **int32**
- represent [Unicode](http://www.joelonsoftware.com/articles/Unicode.html)

### String

**read only** slice of bytes in GO

### Boolean

true false

- AND - &&
- OR - ||
- Negation - !

## Composite Types

### Non-Reference Types

#### Array

Arrays in GO are **value**

- when assign an array to another variable, it copies the entire array
- when arrays are passed to function, it makes copy of the array instead of passing address

```go
// specify both size and value
newArray := [n]Type{val1, val2, val3}

// specify both size no value
newArray := [len]Type{}

```

#### Struct

Struct is named collection of fields. (TypeScript Interface)

```go
Type employee Struct {
  name string
  age  int
  dob  time.Time
```

### Reference Type

#### Slice

- dynamically sized
- reference into the elements of an array

Represented by

- address to the underlying array
- length of the slice
- Capacity of the slice

```go
// declaring using make
s := make([]string, 2, 3)

// direct initiazlization
p := []string{"a", "b", "c"}
```

#### Channel

- pipe through which goroutines can send values and receive values
- the operation <- is used to send or receive
- direction of arrow specify the direction of data flow

```go
ch <- val // sending value from val to ch
val := <- cha // receive value from cha and assign to val
```

type of channel

- unbuffered channel

  - no capacity to hold value
  - send on a channel is block unless there is another goroutine to receive
  - receive is block until there is another goroutine on the other side to send

- buffered channel

  - can specify the size of buffer here and for them
  - send on a buffer channel is block if the buffer is full
  - receive is the only block if buffer of the channel is empty

  ```go
  close() // can be used to close channel
  ```

#### Maps

- zero value of a map is nil

```go
// empty map
var employeeSalary make(map[string]int)
employeeSalary := map[string]int{}

// specify value
employeeSalary := map[string]int{
  "John": 1000
  "Sam": 2000
}

// Add to a Map
employeeSalary["New"] = 3000

// Get from a Map
salary := employeeSalary["John"]

// Delete a key from a map
delete(employeeSalary, "John")
```

#### Pointers

- Pointer is a variable that holds a memory address of another variable
- zero value of a pointer is nil

```go
var ex *int // ex is int pointer *

// & used to get the address of a variable
b := &b

fmt.Println(*b) // print value stored at address b
```

#### Function

```go
// func func_name(arg arg_type) return_values_type

func foo(str string) string {
  // do something
}

// also can use this declaration
add := func(x, y int) int {
        return x + y
       }

fmt.Println(add(1, 2))
```

##### Method

```go
func (receiver receiver_type) some_func(arg) return_value {
  // do somethine
}
```

### Interface

- collection of method signatures
- zero value is nil

```go
type interface_name interface {
  // method sig 1
  // method sig 2
}

// example
type shape interface {
    area() int
}

type square struct {
    side int
}

func (s *square) area() int {
    return s.side * s.side
}

func main() {
    var s shape
    s = &square{side: 4}
    fmt.Println(s.area())
}
```
