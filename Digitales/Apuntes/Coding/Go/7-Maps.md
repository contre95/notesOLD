## Maps

Maps in Go similar to Hashes in Ruby, Objects in JavaScript and Dictionaries in
Python is a Key-Value datatype. Even though they are similar to sturcts, they
differ in some things. 

Both Keys and Values are statically types. Keys and Values can be of different
types between them but all Keys on a Map should be of the same Type, same for
Values.

Declare an empty **Maps**.

```go
colors := map[string]string{
    "red": "#ff0000",
    "white": "#fffffff",
    "black": "#000000",
}
```

*Note that all of the values should have a comma at the end of the value.*

```go
// Another option #1
var color map[string]string
// Another option #2
color := make(map[string]string)
```

Add items to a map and the call it

```go
// Set a alue for a key
colors["white"] = "#ffffff"
// Retrieve a value given a key
colors["white"]
```

Delete a value inside a map

```go
delete(colors, "white")
```

Iterating over Maps

```go
func main(){
    for key,value := range colors {
        fmt.Println("This is my ", key," and this is my value ", value )
    }
}
```

### Difference  between Maps and Structs

| Maps                                                | Structs                                                       |
| --------------------------------------------------- | ------------------------------------------------------------- |
| All Keys must be the same type                      | Struct's "Keys" (Fields) does not have a type                 |
| All Values must be of the same type                 | Values can be of different types                              |
| Use to represent a collection of related properties | Use to represent a "thing" with a lot of different properties |
| Don't need to know all the keys at compile time     | You need to know all the different fields at compile time     |
| Keys are indexed, we can iterate over them          | "Keys" (Fields) are not indexed, we can't iterate a Struct    |
| Referent Type                                       | Value Type                                                    |
