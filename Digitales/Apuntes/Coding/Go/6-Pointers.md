##   Pointers in Go

 I'll assume that you already know about pointers and show you how pointers works on Go really quickly. Spoiler: They work pretty much like in C.

Go is a *"pass by value"*  language, so every time we pass a value to a function we are passing a ***copy*** of that value to the function to operate with, no the real value.

Here are two examples dealing with pointers

Without pointers:

```go
package main
import "fmt"

func main() {
    my_greet := "Hola como estás"
    add_name_to_greet(my_greet, "John Doe")
    fmt.Println(my_greet)  // This will print "Hola como estás" without the name
}

func add_name_to_greet(greet string, name string) {
    greet = greet + name
}
```

With pointers:

```go
package main
import "fmt"

func main() {
    my_greet := "Hola como estas "
    add_name_to_greet(&my_greet, "John Doe")  // We pass the memory address where our greet is located (pointer)
    fmt.Println(my_greet)  // This will print "Hola como estás John Doe"}

func add_name_to_greet(greet *string, name string) { // We take this pointer as parameter
     *greet += name  //We take the Value of the pointer and change it
}
```

Another alternative whit pointers:

```go
package main
import "fmt"

func main() {
    my_greet := "Hola como estas " // Acé es donde C  haría el Malloc !
    var pointerGreet *string
    pointerGreet = &my_greet

    add_name_to_greet(pointerGreet, "John Doe") // We pass the memory address where our greet is located (pointer)
    fmt.Println(my_greet)
}

func add_name_to_greet(greet *string, name string) { // We take this pointer as parameter
     *greet += name //We take the Value of the pointer and change it
}
```

This last happens only for **Value Types** in go, which are **int**, **float**, **string**, **bool** and **structs**. But that's not the same for **Reference Types**. So let's see how we deal with pointers in this case.

### Pointers with Reference Types (Slices)

In the case of slices this works just fine since a Slice is a pointer to the head of an array. So copying that pointer will create a pointer that points to the same array.

```go
package main
import "fmt"

func main() {
    mySlice := []string{"Hola","como","estas?"}
    updateSlice(mySlice)
    fmt.Println(mySlice)
}

func updateSlice( slice []string) {
    //slice = append(slice, "John Doe")
     slice[0] = "Hello"
}
```

This also applies for **Maps**, **Channels**, **Pointers** itself and **functions**.

| Value Types | Reference Types |
| ----------- | --------------- |
| int         | slices          |
| floats      | maps            |
| strings     | channels        |
| bool        | pointers        |
| structs     | functions       |

### The `&` and the `*` 

```go
*variableName // Makes refence to the value that the pointer... points.

*type // This is also a type.  A type of "type pointer"

& variableName // Makes reference to memory address.
 
```

So just to recap:

* To turn `address` into `value` : `*address`

* To turn `value` into `address`: `&value`
* To declare some variable as *"pointer to something of `type` type (eg. person)"* : `var contre *person`

### Exercise:

Why this wont work

```go
package main
import "fmt"

func main() {
    var my_greet *string
    *my_greet = "Hola como estas"

    add_name_to_greet(my_greet, "John Doe") // We pass the memory address where our greet is located (pointer)
    fmt.Println(my_greet)
}

func add_name_to_greet(greet *string, name string) { // We take this pointer as parameter
     *greet += name //We take the Value of the pointer and change it
}
```

*Spoiler: I initialize the pointer that point to nil (nowhere) and tried to assigned a value to <nil>*