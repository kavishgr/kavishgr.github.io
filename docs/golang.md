# Golang

## Pointers

```golang
package main

import (
	"fmt"
)

var p = fmt.Println()

func main() {
	a := 3
	p(a)       // Step.1 print the value of a
	double(&a) // step.2 give double() the MEMORY ADDRESS of var a
	p(a)       // Step.5 print the new value of a
}

func double(number *int) { // Step.3 double() says ok, that address is holding a value of data type int. Hence an INTEGER.
	*number *= 2 // Step.4 Use the VALUE of that MEMORY ADDRESS and multiply it 2

}

// NOTE:
// & = a pointer(location in memory)
// * = dereferencing a pointer(return the value of that memory address)
// To be able to change/modify a value in memory, we have to get the memory address first.
// To be able to knock on someone's door, we need to know where the house is at.
```

[https://play.golang.org/p/spBmulwDVZf]()

## Slice



