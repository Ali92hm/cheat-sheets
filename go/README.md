# Go cheat sheet

## Setup

### $GOPATH
Go uses the `$GOPATH` directory to manage files, packages, and dependencies. 

Make sure to set `$GOPATH` in `.profile`

```
export GOPATH=${HOME}/go
```

## Useful commands
### Pulling dependencies
```
go get github.com/<package-path>
```

### Building project
```
go build
```

### Build and run
```
go run
```

### Cleaning the working directory
```
go clean
```

### Compile and install packages
```
go install
```
This command compiles all packages and generates files, then moves them to $GOPATH/pkg or $GOPATH/bin.

### Lint the source code
```
go fmt
```

### Run tests
```
go test // runs all files named *_test.go
```

### Documentation 
```
godoc -http=:8080
```

Runs the documentation on local server

## Style Guide

Go comes with an official style guide. Use `go fmt` to format files. There is Sublime package called [GoSublime](https://github.com/DisposaBoy/GoSublime) that helps with linting, code completion, etc.




## Syntax
### Variable declaration
```GO
var variableName type
var variableName1, variableName2, variableName3 type // multiple variable declaration
var variableName type = value // variable declaration and initialization
var vname1, vname2, vname3 type = v1, v2, v3 // multiple variable declaration and initialization
vname1, vname2, vname3 := v1, v2, v3 // short assignment (type is inferred from rhs) 
```

### Blank `_`
`_` (blank) is a special variable name. Any value that is given to it will be ignored
```GO
_, b := 34, 35 // 34 is ignored
```

### Constants
```GO
const constantName = value
const constName type = value
```

### Types
#### Boolean
```GO
var isActive bool
```

#### Numerical
##### Int
* `int8`
* `int16`
* `int32`(alias `rune`)
* `int64`

`int` uses 32-bit in 32-bit operating systems, and 64-bit in 64-bit operating systems.
 
##### uint
* `uint8` (alias `byte`) 
* `uint16`
* `uint32`
* `uint64`

`uint` uses 32-bit in 32-bit operating systems, and 64-bit in 64-bit operating systems.

##### Float
* `float32`
* `float64`

##### Complex
* `complex64`: a 32-bit real and 32-bit imaginary part
* `complex128`: a 64-bit real and 64-bit imaginary part

```GO
var c complex64 = 5+5i
```

#### String
```GO
var emptyString string = ""
```

#### Array
```GO
var arr [n]type
a := [3]int{1, 2, 3} // array literals
a := [...]int{1, 2, 3} // go will replace ... with 3
```

#### Slice
Slices in go act like dynamic arrays. `slice` is not really a dynamic array. It's a reference type. `slice` points to an underlying array whose declaration is similar to array, but doesn't need length.

```GO
// define an array
var array = [10]byte{'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}
// define two slices
var aSlice, bSlice []byte

// some convenient operations
aSlice = array[:3] // equals to aSlice = array[0:3] aSlice has elements a,b,c
aSlice = array[5:] // equals to aSlice = array[5:10] aSlice has elements f,g,h,i,j
aSlice = array[:]  // equals to aSlice = array[0:10] aSlice has all elements

// slice from slice
aSlice = array[3:7]  // aSlice has elements d,e,f,g，len=4，cap=7
bSlice = aSlice[1:3] // bSlice contains aSlice[1], aSlice[2], so it has elements e,f
bSlice = aSlice[:3]  // bSlice contains aSlice[0], aSlice[1], aSlice[2], so it has d,e,f
bSlice = aSlice[0:5] // slice could be expanded in range of cap, now bSlice contains d,e,f,g,h
bSlice = aSlice[:]   // bSlice has same elements as aSlice does, which are d,e,f,g
```

* `len(slice)` gets the length of slice.
* `cap(slice)` gets the maximum length of slice
* `append(slice, item1, item2, ...)` appends one or more elements to slice, and returns slice .
* `copy(dest, src)` copies elements from one slice to the other, and returns the number of elements that were copied.

#### Map
Dictionaries (hashmaps) in go are called `map`.

```GO
var numbers map[string] int
rating := map[string]float32 {"C":5, "Go":4.5, "Python":4.5, "C++":2 } // map literals
numbers := make(map[string]int) // dynamically allocated
numbers["one"] = 1  // assign value by key
delete(numbers, "one") // delete value associated with a key
v, ok := numbers["one"] // ok is false since key doesn't exists 
```

#### Error types
```GO
err := errors.New("emit macho dwarf: elf header corrupted")
if err != nil {
    fmt.Print(err)
}
```

#### Custom types
Go doesn't have classes. Structs are used for custom data types

```GO
type Point struct {
  X int
  Y int
}

v := Vertex{1, 2} // instantiation 
```

### Flow
#### `if` statement

* Simple `if/else` statement

```GO
if x == 0 {
	return 0
} else if x < 0 {
	return -x
} else {
   return x
}
```

* You can put one statement before the condition. Variable `a` is not defined outside `if` statement
    	
```GO
	
	if a := b + c; a < 42 {
		return a
	} else {
		return a - 42
	}
    
    fmt.Println(a) // Compile error
```

#### Loops

* `for` loop

```GO
for expression1; conditional; expression2 {
    //...
}

for i := 1; i < 10; i++ {
    //...
}
```

* There is no `while` loop, but:

```GO
for i < 10  {
    //...
}

// while true
for {
    //...
}
```

* Iteration over `array`, `slice`, `map` and `string`

```GO
for i, v := rage array {
    // ...
}

for i := range pow {
    pow[i] = i * 2
}

for _, value := range pow {
    fmt.Printf("%d\n", value)
}

// map
for k,v := range map {
    fmt.Println("map's key:",k)
    fmt.Println("map's val:",v)
}
```

#### `switch`

```GO
switch sExpr {
case expr1:
    // some instructions
case expr2, expr3, expr4:
    // some other instructions
case expr5:
    // some other instructions
default:
    // other code
}
```

* There is no need for `break` but if you want to continue checking for conditions you can use the `fallthrough` keyword.

### Functions

```GO
func funcName(input1 type1, input2 type2) (output1 type1, output2 type2) {
    // function body
    // multi-value return
    return value1, value2
}
```

Examples:

```GO
func add(x int, y int) int {
    return x + y
}

func swap(x, y string) (string, string) {
    return y, x
}

func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return
}
```

#### Variadic functions
Go supports functions with a variable number of arguments.

```GO
func myfunc(arg ...int) {
    for _, n := range arg {
	   fmt.Printf("And the number is: %d\n", n)
    }
}
```

#### Pass by value and reference (pointers)
This is exactly how it works in C++

```GO
// pass by value
func add1(a int) int {
	a = a + 1 // we change value of a, but the original value is untouched
	return a
}

func add1(a *int) int {
	*a = *a + 1 // we changed value of a, and the original value is updated
	return *a
}
```

#### defer
You can have many `defer` statements in one function; they will execute in reverse order when the program executes to the end of functions.

```GO
func ReadWrite() bool {
	file.Open("file")
	defer file.Close()
	if failureX {
		return false
	}
	if failureY {
		return false
	}
	return true
}
```

#### Panic and Recover
`panic` and `recover` are Go's version of `try` and `catch` blocks.


```GO
func doSomething() {
	defer func() {
		if x := recover(); x != nil {
			fmt.Println("Recovering from", x)
		}
	}()

	panic("Oops")
}
```

#### `main` and `init`




### Allocation
`make` does memory allocation for built-in models, such as `map`, `slice`, and `channel`, while `new` is for types memory allocation.

`new(T)` allocates zero-value to type `T`'s memory, returns its memory address, which is the value of type `*T`. By Go's definition, it returns a pointer which points to type `T`'s zero-value. `new` returns pointers.

The built-in function `make(T, args)` has different purposes than `new(T)`. `make` can be used for `slice`, `map`, and `channel`, and returns a type `T` with an initial value. The reason for doing this is because the underlying data of these three types must be initialized before they point to them. For example, a slice contains a pointer that points to the underlying array, length and capacity. Before these data are initialized, slice is nil, so for slice, map and channel, make initializes their underlying data and assigns some suitable values.

make returns non-zero values.

