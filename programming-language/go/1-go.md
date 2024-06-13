# GO

## Declaring Variable

1. var var_name var_type : then assign value
2. var_name := value : this is shortcut for assign type and value at the same time
3. if declaring without value it will assign default value of each type

- string = ""
- int = 0
- bool = false

```go
var foo string = 'foo' // can be used anywhere

// or

foo := 'foo' // this can be used inside function only
```

## Declaring Function

keyword _func_

```go
func func_name(arg_1 arg_1_type, ...) (return_value_1_type, ...) {
  // do something
}
```

## The _main_ package

- It's like App component in React that it's the place where every component (package) is called.
- It's the main app when run _go build_.

```go
package main

import (...)

func main () {
  // the entire app runs here
}

// example

package main

import (
  "fmt"
  "log"

  "example.com/greetings"
)

func main() {
  log.SetPrefix("greetings: ")
  log.SetFlags(0)

  names := []string{"Tar", "John", "Diana"}

  messages, err := greetings.Hellos(names)
  if err != nil {
    log.Fatal(err)
  }

  fmt.Println(messages)
}

```
