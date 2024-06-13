# Error Handling

## The Error Type

- error is anything that implement Error() method
- Error() return error message as string

```go
if err != nil {
  return errors.New("This is error message")
}
```

### Example

```go
import (
    "errors"
    "fmt"
)

var ErrDivideByZero = errors.New("divide by zero") // declaring expected error

func Divide(a, b int) (int, error) {
    if b == 0 {
        return 0, ErrDivideByZero
    }
    return a / b, nil
}

func main() {
    a, b := 10, 0
    result, err := Divide(a, b)
    if err != nil {
        switch {
        case errors.Is(err, ErrDivideByZero):
            fmt.Println("divide by zero error")
        default:
            fmt.Printf("unexpected division error: %s\n", err)
        }
        return
    }

    fmt.Printf("%d / %d = %d\n", a, b, result)
}
```

- basic idea is return error when declaring function
- if error return err else return nil

## Defer

- something similar to .then().catch()
- also called line by line
- only call in _Last In First Out_

```go
func CopyFile(dstName, srcName string) (written int64, err error) {
    src, err := os.Open(srcName)
    if err != nil {
        return
    }
    defer src.Close() // call src.Close() after return
                      // in case that open file failed, the src is still closed

    dst, err := os.Create(dstName)
    if err != nil {
        return
    }
    defer dst.Close() // same idea as above

    return io.Copy(dst, src)
}
```

```go
func b() {
    for i := 0; i < 4; i++ {
        defer fmt.Print(i)
    }
}

// Last In First Out
// 3210
```

## Panic

- built in function to stop the ordinary flow of control
- deferred functions are called normally

## Recover

- built in function that regains control of a panicking goroutine
- only useful inside deferred functions
- during normal execution, recover returns nil
