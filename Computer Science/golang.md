## packages
Base Go code exists within *packages*. All programs begin running package `main`. 

#### function syntax
Functions within a package are defined as follows:
```
package main

import "fmt"

func split (sum int) {
	x = sum * 4 + 9
	y = sum - x

	return x, y
}

func main () {
	fmt.Print(split(18))
}
```

A few key syntactic takeaways from this code snippet:
- A function definition takes the form `func funcName (arg*) {}`
- Go functions can return as many values as it wants, or it can return nothing
- Arguments are specific with the name *before* the type

Additionally, we can see that the `Print` function within the `fmt` package is capitalized; functions within a package that are capitalized get exported with the package. If the function is not capitalized, then we cannot access it when the package is imported elsewhere.

###### naked return statements
As a short aside, the following function is equivalent to the `split` function shown above.
```
func split (sum int) (x, y int) {
	x = sum * 4 + 9
	y = sum - x

	return
}
```

Here, we use *named return values* in the function header, so that we don't need to specify what values to return in the body. This syntax should only be used in short functions because it makes the code less readable.

#### variables
```
var i, j, k int                //declare three variables of type int, 
								 defaulted to the 0-like value of the type
var l, m bool = true, false    //initialize two bool variables with values
var n, p = "no", 2             //initialize two variables with implicit types

n, p := "no", 2                //initialize two variables with implicit types
```

As with most low-level languages, go allows for type specifications including the size of each variable. For example, we can use `int`, `int8`, `int16`, `int32`, and `int64`, as well as the unsigned versions of each type, denoted `uintXX`.

###### explicit type conversion
Go requires explicit type conversions. To convert between types, use the form `float64(i)` if you are trying to convert `int i` into type `float64`.

#### control
The `for` loop is all you need in Go. Here, we can define a traditional `for` loop:
```
for i := 0; i < n; i++ {
	fmt.Println(i)
}
```

We can also repurpose them to act as `while` loops (Go doesn't actually have `while` loopes):
```
sum := 1
for sum < 100 {
	sum += sum
}
```

And we can also define forever loops
```
for {
	fmt.Println("forever")
}
```

###### defer statements
A `defer` statement pauses the execution of a given line until the rest of the function body has executed. If multiple `defer` statements exist in a function body, they are executed in a last-in, first-out order.
