+++
title = "Type-safe enums in Go using generics"
date = "2024-04-16"
description = "An attempt at building enums with generics in Go"

[taxonomies]
tags = ["go", "types"]
+++

I've always had some gripes with how `enums` are implemented in Go. They are not treated as first class citizens and are not fully type safe either. This could potentially lead to bugs that are undetectable by the compiler.

To demonstrate this, let's create an enum in the most Go idiomatic way possible by using type aliasing and `iota` for incremental constants.

```go
type Direction int

const (
	North Direction = iota
	South
	East
	West
)
```

Here, we basically define a set of constants with the shared type `Direction` to enumerate the four directions. However, because the `Direction` type itself is an alias for `int`, one can easily create new unintended directions by creating variables of type `Direction` with new integer values. This not only breaks the invariant of `enums` being a *fixed* list of values but also leads to a loss in type safety at compile time. 

Here's an example:
```go
func (d Direction) String() string {
	switch d {
	case North:
		return "North"
	case South:
		return "South"
	case East:
		return "East"
	case West:
		return "West"
	default:
		return "Invalid"
	}
}

func main() {
	direction := West
	fmt.Println("Direction is", direction)
	//Output: Direction is West
	
	var Midwest Direction = 10
	fmt.Println("Direction is", Midwest)
	//Output: Direction is Invalid
}
```

In this code bite, we are able to create a new invalid `Direction` called Midwest which is outside the intended list of directions. We are also able to use it with the `String` implementation on `Direction`. While we do end up getting 'invalid' as output for printing the string representation for `Midwest` at runtime, it would've been even better if this was caught at compile time itself!

The compiler assumes that any `int` can be a `Direction` and thereby any method implementation for `Direction` will have to be able to work with any `int` value. This can have unintended side effects at runtime! Compile-time type safety is important here.

## Generics

One way to enable full type safety is to make `Direction` a generic type!
We use the same example as above but implemented using generics.

First, we define each direction as its own type. 
```go
// Define the enum values as types
// TODO: Difference between struct{} and interface{}
type (
	North struct{}
	South struct{}
	East  struct{}
	West  struct{}
)
```
Then we create a generic type that takes a type parameter `T` constrained by the above type set.
```go
// Set a type constraint
type Direction[T North | South | East | West] struct {
	Name T
}
```

We can now define any function on `Direction[T]`

```go
func (d Direction[T]) String() string {
	switch any(d.Name).(type) {
	case North:
		return "North"
	case South:
		return "South"
	case East:
		return "East"
	case West:
		return "West"
	default:
		return "Invalid"
	}
}
```
This function will only accept `Direction` with a valid type parameter `T` from `North | South | East | West`. 
In fact, we will not even be able to create a new invalid `Direction`. So if we run the below code, it will not compile!
```go
type Midwest struct{}

func main() {
    direction := Direction[West]{}
	fmt.Println("Direction is", direction)
	// Output: Direction is West
	invalidDirection := Direction[Midwest]{}
    // Compile time error: Midwest does not satisfy North | South | East | West (Midwest missing in main.North | main.South | main.East | main.West)
}
```
And voilà! We've created fully type safe `enums` with generics! Play with the code [here](https://go.dev/play/p/bfWdV7KAhuF)

Bonus: Here's another [approach](https://go.dev/play/p/hHDIGBIM0dD) to `enums` with generics.
I went with the first approach because it seemed closer to the usual idiomatic way and slightly more readable.

## References
- https://go.dev/blog/intro-generics
- https://dev.to/ankitmalikg/implementing-enums-in-golang-40ie



