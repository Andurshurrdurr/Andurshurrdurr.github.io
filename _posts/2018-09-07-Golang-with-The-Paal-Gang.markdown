---
layout: post
title: "Golang with the Pålgang"
date: 2018-09-07
author: Anders
category: Golang
tags: go software web
finished: false
img: covers/paalsgo.png
---

*Just a short intro to the basics of golang with Pål*

# This is Pål

![paal]({{site.baseurl}}/assets/img/blog/paalsgo/paal.jpg)

*(He is the normal looking one by the window)*

Pål is the superhero developer keeping the Sensario backend operational.

I have worked Pål on his right hand side since late 2017 and have enjoyed every
second of it.  We have been getting coffee together nearly every day, spoken
and learned about software engineering together and discovered the magic of Vim
and Chad memes together.

![chad linux]({{site.baseurl}}/assets/img/blog/paalsgo/chad_linux.png)

*From alg0001 on [reddit](https://www.reddit.com/r/virginvschad/comments/7rkm5n/the_virgin_windows_peasant_vs_the_chad_gnulinux/)*

Pål joined the Sensario company late 2017 with the goal of building the backend of
the company so it could handle and process the incoming traffic from both our
IoT sensor nodes with LTE (which I am programming), users and he has provided
development services for the the engineering team. To do this, he has shown great 
mastery of Golang.

So join us in discovering this great programming language!

## Main characteristics of Golang
- General purpose programming language
- Compiled languate w/ great compile time and performance
- Static types
- Strings, chars, pointers, mutant for loops
- Implicit interfaces, structs, maps, slices and arrays
- Made with concurrency in mind
- Nice utilities: Defer, multiple returns

## Whats in $GOPATH?

Golang has an environment variable which determines the workspace of your go
project. Coming from a C and Python background, this system took a bit getting
used to for me, and the Golang package system is something that stopped me from
getting too much into it in the start. Anyway, in the GOPATH you create the
following folders:

     * src: source => This is where we keep our projects
     * pkg: Object files => We dont usually touch this, its for the go toolchain
     * bin: Binary files => We dont usually touch this, its for the go toolchain

This creates a $GOPATH workflow:

     * With golang we import from $GOPATH/src/...
     * Normal structure is this:
          -> $GOPATH/src/myProject/vendor/3rdpartypackage
          -> protip: Use godep instead of `$ go get` to maintain better structure.  I wont get to much into the use of this in this post
     * Note: Go 1.11 introduces experimental support for projects outside $GOPATH

## Golang Syntax

A few of my main takeaways/heads up from the basics of golang syntax

- When returning multiple values, either give all returns a declaration in function prototype, or none (just datatypes types).  Declaring return variables in function prototype will return them implicitly.

```

```

- go fmt is the standard for golang formatting/convention: `$ go fmt myfile.go`
- Golang scope rules are very simple, everything between {} is a scope
- The difference between pointers in C and Go is that go pointers (...)
- In switch case statements, break is implicit/default and to ignore a break one writes the `fallthrough` keyword

```

```

- Exported variables, constants and functions from packages must start with a capital letter

```

```

## Golang datatypes

- Basics
  * uints/ints
  * floats
  * string: always utf-8
  * char: called rune, utf-8 => int32 under the hood

### Arrays
  1. Arrays are lists of values
  2. var myArray [<optional len>]<datatype>{<optional initializer>}
  * myArray :=  [<optional len>]<datatype>{<optional initializer>}
  3. Array utils: 
    -> len(myArray) => int length
    -> for idx, val := range myArray {} // foreach with enumerate

### Slices
  1. Slices are parts of an array
  2. array := [<len>]<datatype>{<optional initializer>}
      * slice := array[<begin>:<end>]
      * slices point to the underlying array
  3. Slice utils:
    -> len(slice)  // length of slice
    -> cap(slice) // capacity of slice
    -> append(<slice>, <value>[, <more values>]) // This returns a new instance
      * When using append, it is adviced to return to the same slice as appended to
slice = append(slice, value)

### Maps
  1. Maps are like python dictionaries, but they are type sensitive
  2. myMap := map[<key datatype>]<value datatype>{<optional key>: <optional value>}
    * forExample := map[string]float64{"myKey": 33}
    * Getting/setting : myMap["myKey"] = <myValue>
  3. Map utils
     -> for <key>, <value> := range myMap {...}
     -> for <key> := range myMap {...}

## Working with datatypes

Here comes some of the nice golang features into play.  So far we've only
looked at the basic capabilities and mechanics of the language

### Custom types
  * Custom types is like typedef in C
  * Syntax: type <MyType> <ActualType>
  * Example: type Hours int
  * Custom types can be compared to same custom type or underlying type, but cannot be compared with different custom even if they share the same underlying type

### Methods

But Go isn't object oriented?

  * Methods are implicit methods on types.  It is a function with a specific receiver argument, which tells which types implement the method
  * func (t <MyType>) <MyMethod>(<MyArgs>) <MyReturn> {...}
  * Now <MyType> vars will implement the <MyMethod> method
  * In Go it is common to write methods that gracefully handle being called with nil receiver
  * Example: 
```
func (v Vertex) Abs() float64 {...}
/* (using) --> */ vert.Abs()
```

### Structs


* In concept pretty much like structs in C -> structured data
* Convention to make all struct methods take either values or pointers as recv
* Declaring struct:
```
      type MyStruct struct {
         myArg string
     }
```
* Initializing struct:
```
      myStruct := MyStruct{MyArg: "Hello World!"}
      myStruct := MyStruct{"Hello World"} // Does the same, but need order of args
```
* Using struct:
      -> Non cap members of struct are private
      -> Accessing struct members are the same for pointers and value based structs
          myStruct.MyArg

### Interfaces

  * The interface type is a set of method signatures
  * Interfaces are implemented implicitly, if a datatype has the methods to satisfy the interface, it automatically implements the interface
  * Syntax for declaring interface: type <MyInterface> interface {/*methods*/}
  * Describing interfaces:  fmt.Printf("(%v, %T)\n", i, i) // i is an interface
  * a variable declared as an interface may be initialized with all types with the corresponding methods

## Golang concurrency

Golang is built with concurrency in mind, and thus has some cool features for
building stuff concurrently, namely Goroutines and channels

- Goroutines
    * Basically a concurrent function
    * Syntax: go <funcion>()
    * Goroutines must be void
- Channels
    * Allows us to do IPC
    * Syntax:
          -> Making channel: channel := make(chan <type>)
          -> Reading from channel: `<-chan`
          -> Writing to channel: `chan<- <value>`

## Utilies worth mentioning

- `pprof` for analyzing load
- `reflect` for inspecting stuff
- `encoding` and `json` for serializing structured data
- Reader/Writer interfaces which are quite common

