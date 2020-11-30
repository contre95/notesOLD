# Go programming language

### The "Hello world"

```go
package main
import "fmt"

func main(){
    fmt.Println("Hello world")
}
```

Package = Workspace = Project

Several `files` in go can belong to a same package. All of them must have the `package main` on top of the file.

### Two types of packages 

- Executable -> Generates a file that we can actually run
- Reusable -> A good place to put reusable logic such as "helpers" or libraries or dependencies.


The word `main` is used for executable packages.

```bash
$> go build --> makes our exec file
```

### Imports

Use to get code from other packages, imports go right below the package name.

"fmt" or Format is one of the most known packages and lets us print to stdout among other things. For more info refer to `golan.org/pkg/fmt`

#### Go file organization

1.  package name
2. imports
3. functions

### Functions

We've already seen how a function looks on the "Hello world" example. In the function below we have between brackets the parameters and next to them the type that the function will return. Additionally, we are casting the sum of the  integers we receive by parameter to string in order to return the correct type.

```go
func functionName(a, b, c int) string {
    return string(a + b + c)
}
```

* The `main()` function is called automatically
* Functions must have return types specified.

Function names that starts with lower case are functions that can't be used outside the file/package and functions that start with upper case can be exported and used outside the file/package

### Invariant arguments

Go functions can take invariant arguments. Let's see an example

```go
func my_functions (i int, s string, fn func (u int), t ...string) {
    fmt.Println(i)
    fn(8)
    for a, b := range t {
        fmt.Println("%d - %s", a , b)
    }
}
```

As we can see we can receive **n** strings in the argument *t*.

### Variable declarations

There are several ways of declaring a variable

```go
var card string = "I'm  a wonderful string"
[declaration] [name] [type] = [value]
```

A shorter way where the compiler interprets the type

```go
card := "I'm a  wonderful string"
```



