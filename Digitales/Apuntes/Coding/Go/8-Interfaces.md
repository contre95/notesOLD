## Interfaces 101

### Interfaces theory

*Interfaces* are named collections of method signatures. If we have two or more Structs that have the have the same method, we can use an interface so we don't need to specify the type of our Structs every time we need to work with them. We just use the interface in that case.  

A code snippets from [goyexample.com/interfaces](goyexample.com/interfaces) leaves this very clear. 

*I added some notes as comments in the code*

Here we declare our interface and other Structs that will make use of our interfaces.

```go
// Boilerplate code..

// This is our interface, there are many shapes that will have area and perimeter (rectangle, circle, triangle, ...)
type geometry interface {
    area() float64
    perim() float64
}

type rect struct {
    width, height float64
}

type circle struct {
    radius float64
}
```

Not that in the example above we distinguish two classes of types, an **interface type** "geometry" which can not be instantiated by itself and two **concrete types** "rect" and "circle" than can be instantiated. Other concrete types are the one predefines in go like "maps", "structs", "int" , etc.

Here's an important part, and this might be a bit counter-intuitive if you come from POO languages. The way we have of implementing an interface is by implementing ALL the methods in the interface.

So our program now has a new type called `geometry`. So from now on, every single type in our program with a (receiver) function called *"area()"* that returns a `float64` and a (receiver) function called *"perim()"* that returns a `float64` are now an honorary member of type `geometry`.

```go
// IMPORTANT !
// We implement an interface by just implementing ALLL the methods in the interface. Here we implement geometry on rect
func (r rect) area() float64 {
    return r.width * r.height
}
func (r rect) perim() float64 {
    return 2*r.width + 2*r.height
}

func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perim() float64 {
    return 2 * math.Pi * c.radius
}
```

Making use of our interface.

```go

func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}

func main() {
    r := rect{width: 3, height: 4}
    c := circle{radius: 5}
    measure(r)
    measure(c)
}
```

As we can see, without interfaces we would have to make a ***measure()*** function for each type (rect and circle).

### More "complex" Interfaces

Here's an example of an interface that specifies multiples return and parameter types

```go
type vehicle interface {
    driveCoordinate(int, int) (int,int,string,error)
}
```

#### Interface inside interfaces

*Example: https://golang.org/pkg/io/#ReadCloser*

```go
type Reader interface {
    Read(p []byte) (n int, err error)
}

type Closer interface {
    Close() error
}

type ReadCloser interface {
    Reader
    Closer
}
```

In order to satisfy the `ReadCloser` interface you will need to also satisfy both `Reader` and `Closer` interfaces.

### Some notes on interfaces

* Interfaces are not generic types
* Interfaces are implicit 
  * We don't "inherit" or link any interface with other types, Go handles that for us
* Interfaces are a **contract** to help us manage types and only types
* Step #1 of understanding interfaces i understanding **how to read them.**