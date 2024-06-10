# GO

## TO DO

- [ ] learn more about map
- [ ] learn more about %v %q
- [ ] find something similar to _while_
- [ ] learn more about type
- [ ] Effective GO Topic
- [ ] How to write GO Code Topic

## Declaring Variable

1. var var_name var_type : then assign value
2. var_name := value : this is shortcut for assign type and value at the same time

```go
var foo string
foo = 'foo'

// or

foo := 'foo'
```

## Declaring Function

keyword _func_

```go
func func_name(arg_1 arg_1_type, ...) (return_value_1_type, ...) {
  // do something
}
```

## Slice (javascript array !?)

```go
tests := []string{
  "test_1",
  "test_2",
  ...
}

tests[1] // get "test_2"
```

## Map

```go
var_name := make(map[key_type]value_type)

// this will return something feels like object in javascript
// don't know how to access each yet
```

## For Loop

- use _range_ keyword
- and use _for_ to loop

```go
// range return index, copy of item's value

// the index, and value can be named any
for index, value := range array {
  // do something
}
```

## Handling Error

```go

func Hellos(names []string) (map[string]string, error) {
  messages := make(map[string]string)

  for _, name := range names {
    message, err := Hello(name)
    if err != nil {
      return nil, err
    }
  messages[name] = message
  }

  return messages, nil
}
```

this function return 2 things

1. map
2. error

handling error is simply by

- if there is error then return error
- if there is no error then return error as null (nil)

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
