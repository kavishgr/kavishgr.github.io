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

### remove duplicate values from a slice

https://www.golangprograms.com/remove-duplicate-values-from-slice.html


## Maps

A map is an unordered list of key-value pairs. It's a dynamic data structure. It can't contain dupicate keys.

### Create an empty map, and a map literal

* Empty map:

**Syntax**: `make(map[KeyType]ValueType)`

```go
m := make(map[string]string)

//OR

var m = make(map[string]string)
```

* Map literal(**last trailing comma is necessary**):

```go
m := map[string]int{
	"First": 100,
	"Second": 80, // comma is necessary
} 
```

### Add new key-value pair

**Syntax**: `m[key] = value`

```go
func main() {

	m := map[string]int{
		"First":  100,
		"Second": 80,
	}
	
	fmt.Println(m)

	m["Third"] = 70

	fmt.Println(m)

}
```
[Go Playground](https://play.golang.org/p/8RRm9AxjkhI)

### Update value

```go
func main() {

	m := map[string]int{
		"First":  100,
		"Second": 80,
	}
	
	m["First"] = 0
	m["Second"] = 0
	
	fmt.Println(m)
}

```
[Go Playground](https://play.golang.org/p/Zh9sL2k07oS)

### Iterating over a map

```go
func main() {

	m := map[string]int{
		"First":  100,
		"Second": 80,
	}

	for key, value := range m {
		fmt.Printf("Key:%v\tValue:%v\n", key, value)
	}
}

```

[Go Playground](https://play.golang.org/p/2jdjZ8tuIry)

### Verify if a key exists or not

A map key can also return a second value, a Boolean. If the key exists, it will return true, or false if the key is not present.

```go
func main() {
	
	listOfName := []string{"John", "Mary", "Jane"}
	for _, name := range listOfName{
		grades(name)
	}
}

func grades(name string) {
	students := map[string]float64{
		"John": 91.7,
		"Jane": 92,
	}
	grade, ok := students[name] // the second value
	if !ok { // if false OR if not true
		fmt.Printf("No grade for %v!!!\n", name)
	} else if grade < 60 {
		fmt.Printf("%v is failing.\n", name)
	} else {
		fmt.Printf("%v is doing well.\n", name)
	}
}

```

[Go Playground](https://play.golang.org/p/C3AL-2-ZToT)

### Delete a key

The built-in `delete()` function will remove the key and its value.

**Syntax**: `delete(map, "KEY")`

```go
func main() {
	
	m := map[string]string{
		"Team A": "Champions",
		"Team B": "Losers",
	}
	
	fmt.Println(m)
	delete(m, "Team B")
	fmt.Println(m)

}
```

[Go Playground](https://play.golang.org/p/Ece3kpTFKIY)

### Maps can't contain duplicate keys

```go
func main() {

	test := map[string]int{
		"one":   1,
		"two":   2,
		"three": 1,
		"one":   20, // duplicate
	}

	fmt.Println(test)
}
```

The above code will produce this error:

```
./prog.go:13:3: duplicate key "one" in map literal 
	previous key at ./prog.go:10:3
```

[Go Playground](https://play.golang.org/p/LbN3tydsGS3)


### Incrementing values

**Syntax**: `map[Key]++`

```go
package main

import (
	"fmt"
)

func main() {
	// list of names
	names := []string{"Willy Denis", "Billy Markovich", "John Carpenter", "Willy Denis", "Billy Markovich", "John Carpenter", "Willy Denis", "Billy Markovich",}
	// initialize a map
	votes := make(map[string]int)
	// range over the slice of names
	for _, name := range names { // leave off the index
		votes[name]++ // use the slice's elements as keys and increment its value by one
		// uncomment the following line to see what's happening
		//fmt.Println(votes)
	}
	fmt.Println("The total number of candidates is", len(votes))
	fmt.Println()
	for key, value := range votes {
		fmt.Printf("%v has %v votes.\n", key, value)
	}
}
```

[Go Playground](https://play.golang.org/p/9yULbWYAAGr)

### Diff maps for duplicate values

https://stackoverflow.com/questions/57236845/checking-if-map-has-duplicate-values-in-go

### Map as a function argument

If a variable is pointing to an already initialized map....

https://medium.com/wesionary-team/pointers-and-passby-value-reference-in-golang-a00c8c59b7f1

https://www.youtube.com/watch?v=SEd9baxsfEA

### Copy a map
https://stackoverflow.com/questions/23057785/how-to-copy-a-map

## Define your own type



## Structs

A struct is a user defined type. It's constructed by grouping multiple values of a single or multiple types together to form a blueprint.

### Define a struct

You declare a struct by using the `struct keyword` as its type. Each field consists of a field name and a field type:

```go
func main() {
	var person struct {
		name     string
		age      int
		employed bool
	}

	person.name = "John"
	person.age = 30
	person.employed = false

	fmt.Println("My name is", person.name)
	fmt.Println("I am", person.age, "years old")
	
	if person.employed {
		fmt.Println("I am currently", person.employed)
	}
```

To create another person, we would have to define a whole new struct (including all its fields)all over again.

[Go Playground](https://play.golang.org/p/TKhulAMvZ6_V)

### Define a struct type

With a user defined struct, you just need to create a struct type once, and then use it as a blueprint to create an instance of that type.

Syntax: `type [StructName] struct{Field FieldType}`

```go
package main

import (
	"fmt"
)

// struct type of a person
type person struct {
	name     string
	age      int
	employed bool
}

func main() {
	// a struct literal
	john := person{
		name:     "John",
		age:      30,
		employed: true, // last comma is mandatory
	}

	fmt.Println(john.name)

	var jane person // create another person
	jane.name = "Jane"
	jane.age = 65
	jane.employed = false

	fmt.Println(jane)
}
```

[Go Playground](https://play.golang.org/p/AKRDRbBVB8s)

### Struct defined type as a function parameter

```go
package main

import (
	"fmt"
)

type person struct {
		name     string
		age      int
		employed bool
	}

func getInfo(p person){ // of type person
	fmt.Println("Name is", p.name)
	fmt.Println("Age is", p.age)
	fmt.Println("Is employed ?", p.employed)
}

func main() {
	
	var john person
	john.name = "John"
	john.age = 30
	john.employed = false
	
	getInfo(john)
}
```

[Go Playground](https://play.golang.org/p/66TnxcE50bn)

### Try

https://www.digitalocean.com/community/tutorials/how-to-use-struct-tags-in-go


### Use a pointer to modify a struct with a function

A pointer is needed to modify a struct. Without a pointer, the function will obtain a copy of the struct, and the original data won't be updated.

```go
package main

import (
	"fmt"
)

type customer struct {
	name  string
	total int
}

func discount(c *customer) { // take a pointer to a struct 
	c.total = c.total / 2
}

func main() {
	var customer1 customer
	customer1.name = "John"
	customer1.total = 50

	discount(&customer1) // pass a pointer
	fmt.Println(customer1.total)
}
```

[Go Playground](https://play.golang.org/p/sLkau2D9LW_E)

https://medium.com/a-journey-with-go/go-should-i-use-a-pointer-instead-of-a-copy-of-my-struct-44b43b104963

### Return a pointer to a struct

```go
package main

import (
	"fmt"
)

var(
	pl = fmt.Println
)

type customer struct {
	name         string
	rate         float64
	subscription bool
}

func newCustomer(name string) *customer { //returns a pointer to a struct
	var c customer
	c.name = name
	c.rate = 2.99
	c.subscription = true
	return &c
}

func discount(c *customer) { // takes a pointer
	c.rate = 1.99
	pl("Discount Applied")
	pl()
}

func customerInfo(c *customer) { //takes a pointer
	pl("Name:", c.name)
	pl("Monthly Rate:", c.rate)
	pl("Active ?", c.subscription)
}

func main() {
	kavish := newCustomer("Kavish") // now the variable kavish is a struct pointer
	customerInfo(kavish)
	pl()
	discount(kavish)
	customerInfo(kavish)	
}
```

[Go Playground](https://play.golang.org/p/zCJIhYeF_Lj)

### Embedding Anonymous Struct Fields

There's 3 structure - Employee, Customer, and Address:

```go
package embeddedstructs

type Employee struct {
	Name       string
	Age        int
	Department string
	Salary     float64
	Address
}

type Customer struct {
	Name string
	Age  int
	Rate float64
	Address
}

type Address struct {
	Street     string
	City       string
	State      string
	PostalCode string
}
```

The `Address` field can be accessed as if it's embedded in both `Employee` and `Customer`:

```go
package main

import (
	"fmt"
	"testing/embeddedstructs" // the file is located in 
)							  // $HOME/go/src/testing/embeddingstructs/embeddingstructs.go

var (
	pl = fmt.Println
) 

func main() {

	customer1 := embeddedstructs.Customer{Name: "Kavish Gour"}
	customer1.Street = "2eme Arrondissement"
	customer1.City = "Paris"
	customer1.State = "France"
	customer1.PostalCode = "75002"

	pl("Customer Info")
	pl("--------------")
	pl("Name:", customer1.Name)
	pl("Street:", customer1.Street)
	pl("City:", customer1.City)
	pl("State:", customer1.State)
	pl("PostalCode:", customer1.PostalCode)
	pl()

	employee := embeddedstructs.Employee{Name: "Jean Delatour"}
	employee.Street = "4eme Arrondissement"
	employee.City = "Paris"
	employee.State = "France"
	employee.PostalCode = "75004"

	pl("Employee Info")
	pl("--------------")
	pl("Name:", employee.Name)
	pl("Street:", employee.Street)
	pl("City:", employee.City)
	pl("State:", employee.State)
	pl("PostalCode:", employee.PostalCode)
}
```

### Methods



https://medium.com/rungo/structures-in-go-76377cc106a2
https://medium.com/rungo/interfaces-in-go-ab1601159b3a
https://medium.com/rungo/anatomy-of-methods-in-go-f552aaa8ac4a

### Encapsulation

https://www.digitalocean.com/community/tutorials/defining-structs-in-go


https://goinbigdata.com/golang-pass-by-pointer-vs-pass-by-value/

## Package Visibility

https://www.digitalocean.com/community/tutorials/understanding-package-visibility-in-go