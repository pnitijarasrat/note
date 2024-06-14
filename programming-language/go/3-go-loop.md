# For Loop

## Three Component Loop

```go
// regular loop just like C Java and JavaScript
sum := 0
for i := 1; i < 5; i++ {
  sum += i
}
fmt.Println(sum) // 10 (1+2+3+4)
```

## While Loop

```go
// skip i = 0 and i++, you get while loop
n := 1
for n < 5 {
  n *= 2
}
fmt.Println(n) // 8 (1*2*2*2)
```

## Infinite Loop

```go
sum := 0
for {
  sum++ // repeated forever
}
fmt.Println(sum) // never reached
```

## Exit a Loop

```go
sum := 0
for i := 1; i < 5; i++ {
  if i%2 != 0 { // skip odd numbers
    continue
  }
  sum += i
}
fmt.Println(sum) // 6 (2+4)

// A continue statement begins the next iteration of the innermost for loop at
// its post statement (i++).

// A break statement leaves the innermost for, switch or select statement.
```

## For Each Range Loop

### Basic

```go
strings := []string{"hello", "world"}
for index, value := range strings {
  fmt.Println(index, value)
}

// 0 hello
// 1 world
```

### String Iteration

```go
for i, ch := range "日本語" {
  fmt.Printf("%#U starts at byte position %d\n", ch, i)
}

// U+65E5 '日' starts at byte position 0
// U+672C '本' starts at byte position 3
// U+8A9E '語' starts at byte position 6
```

### Map Iteration: keys and values

```go
m := map[string]int{
  "one":   1,
  "two":   2,
  "three": 3,
}
for k, v := range m {
  fmt.Println(k, v)
}

// two 2
// three 3
// one 1
// the order of each iteration might not be the same
```

### Channel Iteration

```go
ch := make(chan int)
go func() {
  ch <- 1
  ch <- 2
  ch <- 3
  close(ch)
}()
for n := range ch {
  fmt.Println(n)
}

// 1
// 2
// 3

// For a nil channel, the range loop blocks forever.
```
