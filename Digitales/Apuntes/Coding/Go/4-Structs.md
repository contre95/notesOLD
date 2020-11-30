## Not classes, structs.

Go is clearly not an object oriented programing language but taking a POO approach to understand Go worked for me.  

### Struct

A **data structure** in Go that we can think like a collection of properties that somehow are related together. We can think a struct like a plain object.

Defining a struct in Go that represents a person

```go
type person struct { 
  firstName string
  lastName string
  age int
}
```

As you can see we defined a new type `person`. Then we would be able to create diferent **variables of type `person`** like this:

```go
func main() {
    // Option 1
    lucas := person{"Lucas", "Contreras",105})
   // Option 2
    lucas := person{
        firstName:  "Lucas", 
        age: 105, lastName: "Contreras",
      } 
    // Option 3
    var lucas person // This assigns "Zero values" to the properties depending on this type
    lucas.firstName = "Lucas"
    lucas.lastName = "Contreras"
    lucas.age = 105
    }
```

Different ways of printing a struct 

```go
import fmt
fmt.Println(lucas) // Prints  the struct within {}
fmt.Printf("%+v", lucas) // This will print the properties { firstName:Lucas lastName:Contreras age:105 }
```

Nesting sturcts

```go
type contactInfo struct { 
    number int
    email string
}

type person struct {
    name string
    age int
    contact contactInfo
    // we can omit the "contact" but the property will also bename contactInfo (same as the type)
}

contre := person{
    name : "Lucas Contreras",
    age: 100,
    contact contactInfo{
        email: "lucas_email@hey.com",
          number: 123123123123,
    } // returns a reference
    
    contre2 := new(Person) // returns a pointer
}
```

*Note that all of the properties of a struct takes a comma at the end of the line regardless if it is the last properties (unlike JSONs)*