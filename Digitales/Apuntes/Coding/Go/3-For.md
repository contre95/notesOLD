## For loops

The most basic for loop with a single condition

```go
 i := 1
    for i <= 3 {
        fmt.Println(i)
        i = i + 1
    }
```

A classic initial/condition/after `for` loop.

```go
for j := 7; j <= 9; j++ {
        fmt.Println(j)
    }
```

A `for` without a condition will loop repeatedly until you `break` out of the loop or `return` from the enclosing function, basically a `while loop`

```go
for {
        fmt.Println("loop")
        break
    }
```

You can also `continue` to the next iteration of the loop

```go
for n := 0; n <= 5; n++ {
        if n%2 == 0 {
            continue
        }
        fmt.Println(n)
    }
```

For loops in slices. (Basically a for each with indexes :) 

```go
for index,value := range sliceName {
    fmt.Println("Index: ". index, "Value: ", value)
}
```
