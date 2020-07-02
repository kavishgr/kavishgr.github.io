# Golang

## Pointers

A Pointer is a variable that stores the memory address of another variable. A variable can contain any type of values, but when a variable has a memory address as its value, it's called a pointer.

To create a pointer, an `&` operator is used to retrieve the memory address of a variable:

```
var x = 101 // an integer as its value
var ptr = &x  // get the memory address of x and stores it in a variable called ptr
```
The `&x` retrieves the memory address of x and stores it in `ptr`. A complete example:

```
package main

import "fmt"

var p = fmt.Println

func main() {
	var x = 101
	var ptr = &x

	p("The memory address of x:", &x)
	p("The memory address of ptr:", &ptr)
	p("The value of ptr:", ptr)
}
```

```
// output
The memory address of x:	 0xc0000b4020
The memory address of ptr:	 0xc0000b6018
The value of ptr:		 	 0xc0000b4020
```

[Go Playground](https://play.golang.org/p/UoAJkaMtucM)

Every variable represents a memory address pointing to a value like so:

``` 
0xc0000b6018  = 101
```

A variable pointing to a memory address of another variable is called a pointer.

### Dereferencing a Pointer

Dereferencing is used to access or manipulate data contained in a memory location pointed to by a pointer variable or simply pointer.

To access or manipulate the data of a pointer or to dereference a pointer, an `*` operator is used in front of the pointer variable:

```
package main

import "fmt"

var p = fmt.Println

func main() {
	var x = "Having fun with pointers" // declare a varible with data of type string
	var ptr = &x // store the memory address of variable, hence a pointer
	p(*ptr) // print the value of the pointer
	*ptr = "Still having fun with pointers" // dereference the pointer with new data
	p(x) // print the new data
}
```

[Go Playground](https://play.golang.org/p/e6v88j4E9cZ)

https://dave.cheney.net/2017/04/26/understand-go-pointers-in-less-than-800-words-or-your-money-back
https://medium.com/@Kabilan1290/journey-of-my-first-bug-bounty-72175d903ce3
https://medium.com/bugbountywriteup/introduction-to-bug-bounty-for-noobs-46654bd6e0e2
https://hackingarise.com/xss-dorking/

https://craighays.com/bug-bounty-hunting-tips-6-simplify/

### A Pointer as an Argument in a Function

To define a function() that takes a memory address as an argument or simply a pointer, **`*T`** is used as the type. In this case, `*int` which stands for a pointer to an int, or a memory address whose value is an int.

You give the function() a memory address by prepending the variable with an `&` operator. Inside the function, an `*` is used to access the value, hence dereferencing a pointer.

```golang
package main

import (
	"fmt"
)

func zero(ptr *int){ 
	
	// *int means: i need a memory address that points to data of type int
	
	// behind the scene, ptr will point to a memory address that looks like this (in hexadecimal): ptr = 0xc00002c008 
	
	// on the next line, the asterisk '*' is used again(now in front of the pointer variable)
	// to dereference the pointer, hence access/manipulate the value stored in that particular 
	// memory address
	// behind the scene => replace the value of 0xc00002c008 with 0
	
	*ptr = 0 // store 0 in the memory address *ptr is refering to
	
	
	// if i write: ptr = 0 
	// the go compiler will return an error saying: cannot use 0 (type int) as type *int in assignment
	// because ptr is like: var ptr *int
	// ptr will only accept or store a memory address as its value
	// 
	// you can't just assign a value in it
	// you have to dereference it first
}


func main() {
	x := 5	
	zero(&x)	// the & operator finds the address of variable x	
	fmt.Println(x)
}
```
[Go Playground](https://play.golang.org/p/DhjG6aC-j-M)

## Assignment Operators


## Loops

The beauty of Go's `For` loop is that it merges many modern style of looping into one [keyword](https://golang.org/ref/spec#Keywords). Loops **always** begin with the `for` keyword.

### 

### Init, Condition, and Post (optional)

```golang
func main() {
	for i := 0; i <=3; i++{
		fmt.Println(i)
	}
```

**Initialize** a statement - `i := 0`
**Condition** that determine if the loop has to continue or stop - `i <= 3`
**Post statement** runs if condition is true - `i++` (including the loop block {})

The variable `i` is only visible in the loop block.

### While loop

To construct a `while loop`, omit the init and post statement:

```golang
package main

import (
	"fmt"
)

func main() {
	i := 0 // declared outside of loop block
	fmt.Println("i is", i)
	for i < 5{ // while true, keep looping
		i++
		fmt.Println("Now i is", i)
	} // end of loop block
	fmt.Println()
	fmt.Println("Final is", i)

}
```

### Infinite loop



### For...range loop

### Continue and Break


## Slice

A slice is a dynamic container that hold elements of the same type. It's build on top of an array.

https://play.golang.org/p/GJrrw1BYo_O

### Slice Literal

A slice literal is used when you already know what values it will contain:

```golang
package main

import (
	"fmt"
)

func main() {

	s := []string{"a", "b", "c", "d"}
	fmt.Println(s)
}
```

### Two ways to create an empty or nil slice

* Initialize an empty slice with a nil value:

```golang
var mySlice []int
```

According to [Golang Wiki](https://github.com/golang/go/wiki/CodeReviewComments#declaring-empty-slices), the former is the preferred way.

* Using the builtin `make` function to create an empty slice (non-nil):

```golang
mySlice := make([]string, 0, 10)
```

The syntax: ```make([]T, length, capacity)```

Full example:

```golang
package main

import (
	"fmt"
)

func main() {
	mySlice := make([]int, 5, 10)
	fmt.Printf("mySlice is of type %T\nIts length is %v\nIts capacity is %v", mySlice, len(mySlice), cap(mySlice))
}
```

Output:

```
mySlice is of type []int
Its length is 5
Its capacity is 10
```

To create a slice with a length or capacity, use `make()`

[Go Playground](https://play.golang.org/p/049NI7H1ROA)

There's another shortcut: 

```golang
slice := []string{}
```

The above slice is empty with a length of zero instead of nil(non-nil slice).

**Note:** In most cases, empty slice and nil slice can be treated the same. In some cases, they should be treated differently, one of them is when doing JSON encoding.
An empty slice will be encoded as an `[]` in JSON while nil slice will be encoded as `null`.

### for...range loop over a slice

The recommended way to iterate over a slice is by using a for...range loop:

```golang
package main

import (
	"fmt"
)

func main() {
	mySlice := []int{1, 2, 3, 4, 5}
	
	for i, v := range mySlice {
		fmt.Printf("Index %v has the value of %v\n", i, v)	
	}	
}
```

[Go Playground](https://play.golang.org/p/t-jsaVKQKYD)

### Slicing a slice

Slicing is used to access an individual or a slice of an array. **Why a slice of an array?** Because slices are built on top of arrays. **If you change an array, the result will reflect in the slice.**

**To use the slice operator, two indexes are required**: where the slice should start, and where the slice should stop, but not including it.

* **Slicing from index 0 to 4**:

```golang
package main

import "fmt"

func main() {
	underlyingArray := [5]string{"g", "o", "l", "a", "n", "g"}
	slice := underlyingArray[0:4]
	fmt.Println(slice)
}
```

Output is:

```
[g o l a]
```

The second index is the index the slice will stop before.

* **Slice from index 1 till the end**

```golang
package main

import (
		"fmt"
		"os"
)

func main() {
	slice := os.Args[1:]
	for _, v := range slice {
		go doSomethingAmazing(v)
	}
}
```

Take a list of arguments from standard input and slice from index 1 till the end. Index 0 or the name of the Go script is discarded.

* **Slice from index 0 till index 4**

If you omit the start index, 0 will be used as default:

```golang
package main

import (
		"fmt"
		"os"
)

func main() {
	underlyingArray := [5]int{1, 2, 3, 4, 5}
	slice := os.Args[:3]
	for i, v := range slice {
		fmt.Printf("Index %v has the value of %v.", i, v)
	}
}
```

Output is:

```
[1 2 3]
```

### Appending to a slice

The [built-in append function](https://golang.org/pkg/builtin/#append), appends element to the end of a slice. It is therefore necessary to store the result of append, often in the variable holding the slice itself.

**The anatomy of the append function**:

```golang
func append(slice []Type, elems ...Type) []Type
```

It takes a slice as the first parameter, and the second parameter can be an unlimited number of elements of the same type or another slice(unfurled with an elipsis). And it returns a slice. That's why it's recommended to store the result in the slice that we're appending values to.

Example:

```golang
package main

import (
	"fmt"
	"bufio"
	"os"
)

func main() {
	var slice []string // initialize a nil slice
	fmt.Println(slice)  // slice is nil
	sc := bufio.NewScanner(os.Stdin) // take parameters from standard input
	for sc.Scan() {					 // loop over lines of input
		slice = append(slice, sc.Text()) // append each line to the slice
	}
	fmt.Println(slice) // results
}
```

Try it:

```bash
echo -e "1\n2\n3\n4" | go run main.go
```

### Passing Slices to a Variadic Function

```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	s := []string{"Go", "is", "my", "favourite", "Programming", "Language"} // creates a slice of string with 6 elements
	result := concatStrings(s...) // unfurl the slice with an elipsis and pass it to the function
	fmt.Println(result) // prints the result
	
}

func concatStrings(sentence ...string) string { 
	var sum string
	for _, v := range sentence {
		sum += v + " " // concatenate all elements
	}
	sum =  strings.TrimSpace(sum) // remove leading and trailing spaces
	return sum + "." // add a dot at the end
}
```

[Go Playground](https://play.golang.org/p/U8SGRB2RO2q)

### The danger of appending to a slice that already has a length and a capacity

```golang
package main

import (
	"fmt"
)

func main() {
	numbers := []int{11, 12, 13}
	mySlice := make([]int, 5, 10)
	
	for _, v := range numbers{
		mySlice = append(mySlice, v)
	}
	fmt.Println(mySlice)
}
```

Output:

```golang
[0 0 0 0 0 11 12 13]
```

One of the ways to make use of an empty slice:

```golang
package main

import (
	"fmt"
)

func main() {
	candidates := []string{"macOS", "OpenBSD", "Linux"}
	// number of votes                                                 
	votes := []string{"macOS", "OpenBSD", "Linux", "macOS", "OpenBSD", "macOS"}
	// make an empty slice with the length of  the total number of candidates 
	counts := make([]int, len(candidates)) 

	for _, vote := range votes {
		matched := false
		for i, candidate := range candidates {
			if candidate == vote {
				counts[i]++
				matched = true
			}
		}
		if matched == false {
			candidates = append(candidates, vote)
			counts = append(counts, 1)
		}
	}
	for i, candidate := range candidates {
		fmt.Printf("%s: %d\n", candidate, counts[i])
	}
}
```

[Go Playground](https://play.golang.org/p/9QncTu0JVhR)

### Update entries in a loop

```golang
num := []int{11, 12, 13}
for _, n := range num {
    n += 1
}
fmt.Println(s)
// Output: [11 12 13]
```

The thing is, all the values is being **copied one by one** to **a local variable n**; the slice remained intact. That's why in certain situation, we have to use pointers.

To update the slice, call the slice itself:

```golang
num := []int{11, 12, 13}
for i := range num { // n: value is not needed
	s[i] =+ 1
}
fmt.Println(s)
// Output: [12 13 14]
```

## Maps



## Structs

https://pragmaticwebsecurity.com/cheatsheets.html

### Pointer in a struct

https://medium.com/a-journey-with-go/go-should-i-use-a-pointer-instead-of-a-copy-of-my-struct-44b43b104963

https://medium.com/a-journey-with-go/archive


https://goinbigdata.com/golang-pass-by-pointer-vs-pass-by-value/