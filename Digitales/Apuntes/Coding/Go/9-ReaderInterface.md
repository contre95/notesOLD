# Examples of common interfaces

## The io.Reader Interface

The Reader Interface can be found all over Go's documentation, so I guess it is worth mentioning. This interface let us handle a wide diversity of input source with different `types`  associated. The `io.Reader` interface represents an entity from which you can read a stream of bytes.

```go
type Reader interface {
        Read(buf []byte) (n int, err error)
}
```

`Read` reads up to `len(buf)` bytes into `buf` and returns the number of bytes read – it returns an [`io.EOF`](https://golang.org/pkg/io/#pkg-variables) error when the stream ends.

Example of an HTTP request using the `Read()` function from the Reader interface:

```go
// ...
func main() {
	resp, err := http.Get("https://btc.lucascontre.site")
	if err != nil {
		fmt.Println(err)
	}
	bs := make([]byte, 9999)
	resp.Body.Read(bs)
	fmt.Println(string(bs))
}

```

We can see it reads from the body into our byte slice (`[]byte`)

## The io.Writer Interface

```go
type Writer interface {
    Write(p []byte) (n int, err error)
}
```

Writer is the interface that wraps the basic Write method.

Write writes `len(p)` bytes from p to the underlying data stream. It returns the number of bytes written from `p` *(0 <= n <= len(p))* and any error encountered that caused the write to stop early.

## The io.Copy function

The `io.Copy` function is, as well as `io.Writer` and `io.Reader`, part of the io packer

Copy definition:

```go
func Copy(dst Writer, src Reader) (written int64, err error)
```

Copy copies from src to dst until either EOF is reached on src or an error occurs. It returns the number of bytes copied and the first error encountered while copying, if any.

With the `io.Copy` function, our http request would look like this.

```go
import (
		"fmt"
		"io"
    	"os"
)

func main() {
	resp, err := http.Get("https://btc.lucascontre.site")
	if err != nil {
		fmt.Println(err)
	}
    io.Copy(os.Stdout, resp.Body)
    // We know that os.Stdout implement the Writer interface, because it has a Write() function
    // We also know that resp.Body has a Read function because it implements the Read() function
}
```

