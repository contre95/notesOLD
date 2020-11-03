## Receiver functions in Go

By now we probably know how to declare a function in go from the intro section. Now we'll learn how to declare a receiver functions (spoiler alert: It's a method)

 We would learn that we can add *behavior* to a `struct` with this *Receiver functions* (Spoiler alert: *Methods*)

```go
func (p person) print() {
    fmt.Printf("%+v", p)
}

func (p person) updateName(newFirstName string) {
    p.firstName = newFirstName
}
```

We see that this functions receives a variable *p* of type `person` which is a struct of type `person`. And we can call these functions with the struct the following way

```go
lucas =: person{
    name: "Lucas Contreras",
    age: 100,
}

lucas.print() // {name:Lucas Contreras age:100}
lucas.updateName("Pedro Alfonso") // Name will not change due to pointers.
```



