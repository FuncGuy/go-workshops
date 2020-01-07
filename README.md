# Golang Training Resources

This repository contains files needed for managing Go language workshop - it's some kind of quite complete walk-through of Go language. Feel free to look on the code, there are many comments which could be useful for beginners and semi-intermediate Go developers.

## About Go

Who designed Go language?

- Rob Pike (Unix, UTF-8)
- Ken Thompson (Unix author, UTF-8, B lang)
- Robert Griesemer (V8, Java Hotspot (Oracle Java), GFS)

but those above are only ignitors of whole contributions: https://golang.org/AUTHORS

Why `go` was developed by Google? They have a lot of problems in C/Python/Java codebases:

- speed up development
- speed up compiling
- multicore systems

sources:
- https://golang.org/doc/faq#What_is_the_purpose_of_the_project
- https://talks.golang.org/2012/splash.article


## Go language characteristics

- statically compiled (one fat binary with all dependencies)
- Garbage Collected
- Strong types
- Functions as first class citizens
- Object Oriented (but without inheritance and classes)

## Why it's worth of your time?

- easy deployment (no dependencies, single binary statically linked)
- no more code style wars - `gofmt`
- integrated package downloader `go get`
- integrated code validation `go vet` and `golint` (github.com/golang/lint)
- nice playground (https://play.golang.org/)
- `gocode` intellisense server - you don't need fat IDE to write go code, you can use now editor which you love (Sublime, Atom, Vim, Emacs, VSCode)
- very fast compilation - if you're going from JAVA world you'll be really surprised
- quite complete standard library - template/html, performant www servers, json, xml, streams, io, buffers, first class citizen concurrency
- easy to use cross-compilation (x64, ARM, 386, Mac, Windows)
- easy start, bunch of editors, all things simply work
- http2 in core
- testing included
- benchmarking of code included
- very low entry barrier
- hype, one of fastest growing language, many new projects are in Go recently
- concurrency
- great documentation generator
- and many many more ...

## Workshop prerequisites

You can install `golang` and `docker` using your preferred way i.e. your OS package manager (brew, pacman, apt, snap or other) or you can simply follow installation instruction on go and docker sites.

### Golang installation

For recent installation instructions please refer to [Golang installation guide](https://golang.org/doc/install)

You'll need `git` to be installed

### Docker install

> Docker is the company driving the container movement and the only container platform provider to address every application across the hybrid cloud. Today’s businesses are under pressure to digitally transform but are constrained by existing applications and infrastructure while rationalizing an increasingly diverse portfolio of clouds, datacenters and application architectures. Docker enables true independence between applications and infrastructure and developers and IT ops to unlock their potential and creates a model for better collaboration and innovation.



For recent docker installation please follow [Docker installation guide](https://docs.docker.com/install/) for your OS.

Docker is needed for some parts of workshops for running databases or other needed dependencies. Also will be needed to complete homework.

### Docker Compose Installation

> Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

To install docker compose please follow [Docker compose installation guide](https://docs.docker.com/compose/install/)

## Init workshops to play on your machine with code

    go get github.com/naqvijafar91/go-workshops
    cd $GOPATH/src/github.com/naqvijafar91/go-workshops

## Go Tools

### Included

- go test - included testing framework
- go fmt - code formater - only one valid coding standard -  [fmt library website](https://golang.org/pkg/fmt/)
- go vet - code validator and fixer - [vet library website](https://golang.org/cmd/vet/)
- go oracle - dependencies analyser (can be integrated in editor) [oracle web site](http://golang.org/s/oracle-user-manual)
- godoc - great documentation generator and viewer
- gocode - autocomplete service - [gocode library website](https://github.com/mdempsky/gocode)

### IDEs

- IntelliJ Go plugin https://plugins.jetbrains.com/plugin/9568-go
- GoLand - https://www.jetbrains.com/go/
- Emacs - go-mode
- Vim - vim-go
- Visual Studio Code (really great UX)
- LiteIDE
- SublimeText
- Atom

### Auto reload

- BRA (Brilliant Ridiculous Assistant) https://github.com/Unknwon/bra - it's good to setup it when you're working on some webservers to auto reload your app when changes in code are made.


## Github style - project structure

In go, idiomatic way is to organise code in "github style", so part of the path is looking like server address to library. Of course if you want you don't need to do this, but whole ecosystem works that way.

```sh
src/
    github.com
        naqvijafar91
            mysuperproject
    ioki.com.pl
            mnmel
                 nmelinium
bin/
    superappbinary
pkg/
    compiled packages
```

Environment variable `$GOPATH` is responsible for path to the root dir of `src`, `bin` and `pkg` directories.


## Packages and Importing

`package` in go is in form of files with directive `package package_name` on top of each file. Package by default is imported as full path to package.

    import "github.com/naqvijafar91/go-workshops/010-basics-importing/sub"

## Getting and installing external packages

To get external package we need to run go install which will get sources and binaries and put them to `src`/`bin`/`pkg` directories

```sh
go install external.package.com/uri/to/package
```

## `sub` example package

As we can see our `sub` package is in directory `sub` (obvious) and have two files; `sub1.go` and `sub2.go` each of them also have `package sub` directive which tells compiler that they are in one package.



([code for: Basics Importing](https://github.com/naqvijafar91/go-workshops/tree/master/010-basics-importing))

## Package managers

Currently most advanced in go ecosystem is `dep` https://github.com/golang/dep

You can init your project:

	$ dep init
	$ ls
	Gopkg.toml Gopkg.lock vendor/

after that dep will add vendor dir where all dependencies will be loaded (In go after 1.5 `vendor` dir have preference over "github style `$GOPATH` based directories - when compiler will not find library in vendor dir it'll try to take it from `$GOPATH`).

For more details please refer to `dep` documentation at https://golang.github.io/dep/docs/daily-dep.html


([code for: Package Management](https://github.com/naqvijafar91/go-workshops/tree/master/011-package-management))



### Tools

As in middle 2019 editors have still issues with new modules, you need
to install proper `gocode` or can use `gopls` (language server) for
autocompletition



([code for: Modules](https://github.com/naqvijafar91/go-workshops/tree/master/012-modules))

## Variables

### What is a variable

Variable is the name given to a memory location to store a value of a specific type. There are various syntaxes to declare variables in go.

### Declaring a single variable

**var name type**  is the syntax to declare a single variable.

```go
package main

import "fmt"

func main() {  
    var age int // variable declaration
    fmt.Println("my age is", age)
}

```

[Run in playground](https://play.golang.org/p/XrveIxw_YI)

The statement  `var age int`  declares a variable named  _age_  of type  _int_. We have not assigned any value for the variable. If a variable is not assigned any value, go automatically initialises it with the  **zero value**  of the variable's type. In this case, age is assigned the value  `0`. If you run this program, you can see the following output

```
my age is 0  

```

A variable can be assigned to any value of its type. In the above program age can be assigned any integer value.

```go
package main

import "fmt"

func main() {  
    var age int // variable declaration
    fmt.Println("my age is ", age)
    age = 29 //assignment
    fmt.Println("my age is", age)
    age = 54 //assignment
    fmt.Println("my new age is", age)
}

```

[Run in playground](https://play.golang.org/p/z4nKMjBxLx)

The above program will produce the following output.

```
my age is  0  
my age is 29  
my new age is 54  

```

### Declaring a variable with initial value

A variable can also be given a initial value when it is declared.

**var name type = initialvalue**  is the syntax to declare a variable with initial value.

```go
package main

import "fmt"

func main() {  
    var age int = 29 // variable declaration with initial value

    fmt.Println("my age is", age)
}

```

[Run in playground](https://play.golang.org/p/TFfpzsrchh)

In the above program, age is variable of type int and has initial value 29. If you run the above program, you can see the following output. It shows that age has been initialised with the value 29.

```
my age is 29  

```

### Type inference

If a variable has an initial value, Go will automatically be able to infer the type of that variable using that initial value. Hence if a variable has an initial value, the  _type_  in the variable declaration can be omitted.

If the variable is declared using the syntax  **var name = initialvalue**, Go will automatically infer the type of that variable from the initial value.

In the following example, you can see that the type  _int_  of the variable  _age_  has been removed in line no. 6. Since the variable has a initial value of 29, go can infer that it is of type int.

```go
package main

import "fmt"

func main() {  
    var age = 29 // type will be inferred

    fmt.Println("my age is", age)
}

```

[Run in playground](https://play.golang.org/p/FgNbfL3WIt)

### Multiple variable declaration

Multiple variables can be declared in a single statement.

**var name1, name2 type = initialvalue1, initialvalue2**  is the syntax for multiple variable declaration.

```go
package main

import "fmt"

func main() {  
    var width, height int = 100, 50 //declaring multiple variables

    fmt.Println("width is", width, "height is", height)
}

```

[Run in playground](https://play.golang.org/p/4aOQyt55ah)

The  _type_  can be omitted if the variables have initial value. The program below declares multiple variables using type inference.

```go
package main

import "fmt"

func main() {  
    var width, height = 100, 50 //"int" is dropped

    fmt.Println("width is", width, "height is", height)
}

```

[Run in playground](https://play.golang.org/p/sErofTJ6g-)

The above program will print  `width is 100 height is 50`  as the output.

As you would have probably guessed by now, if the initial value is not specified for width and height, they will have  `0`  assigned as their initial value.

```go
package main

import "fmt"

func main() {  
    var width, height int
    fmt.Println("width is", width, "height is", height)
    width = 100
    height = 50
    fmt.Println("new width is", width, "new height is ", height)
}

```

[Run in playground](https://play.golang.org/p/DM00pcBbsu)

The above program will print

```undefined
width is 0 height is 0  
new width is 100 new height is  50  

```

There might be cases where we would want to declare variables belonging to different types in a single statement. The syntax for doing that is

```go
var (  
      name1 = initialvalue1
      name2 = initialvalue2
)

```

The following program uses the above syntax to declare variables of different types.

```go
package main

import "fmt"

func main() {  
    var (
        name   = "naveen"
        age    = 29
        height int
    )
    fmt.Println("my name is", name, ", age is", age, "and height is", height)
}

```

[Run in playground](https://play.golang.org/p/7pkp74h_9L)

Here we declare a variable  **name of type string, age and height of type int**. (We will discuss about the various types available in golang in the next tutorial). Running the above program will produce the output  `my name is naveen , age is 29 and height is 0`

### Short hand declaration

Go also provides another concise way for declaring variables. This is known as short hand declaration and it uses  **:=**  operator.

**name := initialvalue**  is the short hand syntax to declare a variable.

```go
package main

import "fmt"

func main() {  
    name, age := "naveen", 29 //short hand declaration

    fmt.Println("my name is", name, "age is", age)
}

```

[Run in playground](https://play.golang.org/p/ctqgw4w6kx)

If you run the above program, you can see  `my name is naveen age is 29`  as the output.

Short hand declaration requires initial values for all variables in the left hand side of the assignment. The following program will thrown an error  `cannot assign 1 values to 2 variables`. This is because  **age has not been assigned a value.**

```go
package main

import "fmt"

func main() {  
    name, age := "naveen" //error

    fmt.Println("my name is", name, "age is", age)
}

```

[Run in playground](https://play.golang.org/p/wZd2HmDvqw)

Short hand syntax can only be used when at least one of the variables in the left side of  **:=**  is newly declared. Consider the following program,

```go
package main

import "fmt"

func main() {  
    a, b := 20, 30 // declare variables a and b
    fmt.Println("a is", a, "b is", b)
    b, c := 40, 50 // b is already declared but c is new
    fmt.Println("b is", b, "c is", c)
    b, c = 80, 90 // assign new values to already declared variables b and c
    fmt.Println("changed b is", b, "c is", c)
}

```

[Run in playground](https://play.golang.org/p/MSUYR8vazB)

In the above program, in line no. 8,  **b**  has already been declared but  **c**  is newly declared and hence it works and outputs

```
a is 20 b is 30  
b is 40 c is 50  
changed b is 80 c is 90  

```

Whereas if we run the program below,

```go
package main

import "fmt"

func main() {  
    a, b := 20, 30 //a and b declared
    fmt.Println("a is", a, "b is", b)
    a, b := 40, 50 //error, no new variables
}

```

[Run in playground](https://play.golang.org/p/EYTtRnlDu3)

it will throw error  `no new variables on left side of :=`  This is because both the variables  **a**  and  **b**  have already been declared and there are no new variables in the left side of  **:=**

Variables can also be assigned values which are computed during run time. Consider the following program,

```go
package main

import (  
    "fmt"
    "math"
)

func main() {  
    a, b := 145.8, 543.8
    c := math.Min(a, b)
    fmt.Println("minimum value is ", c)
}

```

[Run in playground](https://play.golang.org/p/7XojAtrpH9)

In the above program, the value of c is calculated during run time and it's the minimum of a and b. The program above will print

```
minimum value is  145.8  

```

Since Go is strongly typed, variables declared as belonging to one type cannot be assigned a value of another type. The following program will throw an error  `cannot use "naveen" (type string) as type int in assignment`  because age is declared as type int and we are trying to assign a string value to it.

```go
package main

func main() {  
    age := 29      // age is int
    age = "naveen" // error since we are trying to assign a string to a variable of type int
}

```

[Run in playground](https://play.golang.org/p/K5rz4gxjPj)




([code for: Basics Variables](https://github.com/naqvijafar91/go-workshops/tree/master/020-basics-variables))

## Constants

Use `const` to define new constant, mechanics looks like in other languages. What is worth to mention that we have `iota` keyword which could be used as some kind of iterator in constant definition.



([code for: Basics Constants](https://github.com/naqvijafar91/go-workshops/tree/master/030-basics-constants))

## Functions

Functions in Go are "First class citizen".

- function definition
- multiple returns
- named multiple returns
- deferred calls
- variadic functions


([code for: Basics Functions](https://github.com/naqvijafar91/go-workshops/tree/master/040-basics-functions))

## Packages initialisation

`func init() {}` is responsible for package initialisation, it's called only once when import statement for given package is called.



([code for: Basics Init](https://github.com/naqvijafar91/go-workshops/tree/master/041-basics-init))

## Closures aka anonymous functions

Go supports anonymous functions, which can form closures. Anonymous functions are useful when you want to define a function inline without having to name it.

Functions in Go are first class citizens so it can be:
- passed as parameters
- created as types
- assigned as values to variables
- called anonymously
 


([code for: Basics Closures](https://github.com/naqvijafar91/go-workshops/tree/master/042-basics-closures))

## Data structures: Arrays

In Go, an `array` is a **numbered sequence of elements** of a specific
length. Arrays are "low level" data structures with slices over them
which simplifies creating and managing.



([code for: Basics Arrays](https://github.com/naqvijafar91/go-workshops/tree/master/050-basics-arrays))

## Slices


Slices are a key data type in Go, giving a more powerful interface to sequences than arrays.

Unlike arrays, slices are typed only by the elements they contain (not the number of elements). To create an empty slice with non-zero length, use the builtin make. Here we make a slice of strings of length 3 (initially zero-valued).

sources:

- https://blog.golang.org/slices
- https://github.com/golang/go/wiki/SliceTricks
- https://blog.golang.org/go-slices-usage-and-internals
- http://research.swtch.com/godata
- http://blog.golang.org/go-slices-usage-and-internals
- http://www.dotnetperls.com/slice-go



([code for: Basics Slices](https://github.com/naqvijafar91/go-workshops/tree/master/051-basics-slices))

## Loops

In go there is only one loop keyword: `for`. It's often used with `range` keyword to iterate over array like elements.


([code for: Basics Loops](https://github.com/naqvijafar91/go-workshops/tree/master/052-basics-loops))

## Data structures: Maps

One of the most useful data structures in computer science is the hash table. Many hash table implementations exist with varying properties, but in general they offer fast lookups, adds, and deletes. Go provides a built-in map type that implements a hash table.



([code for: Basics Maps](https://github.com/naqvijafar91/go-workshops/tree/master/055-basics-maps))

## Basics Overriding Internal Types



There is no README.md for Basics Overriding Internal Types use ([code for: Basics Overriding Internal Types](https://github.com/naqvijafar91/go-workshops/tree/master/057-basics-overriding-internal-types)) link to follow code examples



## `make` and `new` keywords

`new(T)` allocates zeroed storage for a new item of type T and returns its address. In Go terminology, it returns a pointer to a newly allocated zero value of type T.

`make(T)` For slices, maps, and channels, make initializes the internal data structure and prepares the value for use.

### `make`

Things you can do with make that you can't do any other way:

- Create a channel
- Create a map with space preallocated
- Create a slice with space preallocated or with len != cap


### `new`

It's a little harder to justify new. The main thing it makes easier is creating pointers to non-composite types. The two functions below are equivalent. One's just a little more concise:

    func newInt1() *int { return new(int) }

    func newInt2() *int {
        var i int
        return &i
    }


Go has multiple ways of memory allocation and value initialization:

    &T{...}, &someLocalVar, new, make

Allocation can also happen when creating composite literals.

new can be used to allocate values such as integers, &int is illegal:

    new(Point)
    &Point{}      // OK
    &Point{2, 3}  // Combines allocation and initialization

    new(int)
    &int          // Illegal

    // Works, but it is less convenient to write than new(int)
    var i int
    &i

In terms of channels there you can use make and new

    p := new(chan int)   // p has type: *chan int
    c := make(chan int)  // c has type: chan int


([code for: Basics New And Make](https://github.com/naqvijafar91/go-workshops/tree/master/059-basics-new-and-make))

## Structs

A struct is a sequence of named elements, called fields, each of which has a name and a type. Field names may be specified explicitly (IdentifierList) or implicitly (EmbeddedField). Within a struct, non-blank field names must be unique.



([code for: Basics Structs Defining](https://github.com/naqvijafar91/go-workshops/tree/master/060-basics-structs-defining))


([code for: Basics Struct Composition](https://github.com/naqvijafar91/go-workshops/tree/master/062-basics-struct-composition))

## Struct tags (annotations like)

A tag for a field allows you to attach meta-information to the field which can be acquired using reflection. Usually it is used to provide transformation info on how a struct field is encoded to or decoded from another format (or stored/retrieved from a database), but you can use it to store whatever meta-info you want to, either intended for another package or for your own use.



([code for: Basics Struct Tags](https://github.com/naqvijafar91/go-workshops/tree/master/064-basics-struct-tags))

## Basics Anonymous Structs



There is no README.md for Basics Anonymous Structs use ([code for: Basics Anonymous Structs](https://github.com/naqvijafar91/go-workshops/tree/master/065-basics-anonymous-structs)) link to follow code examples



## Interface

Go have "implicit interfaces". To implement an interface in Go, we
just need to implement all the methods in the interface.

So what is an interface? An interface is two things: it is a set of
methods, but it is also a type.

### The `interface{}` type

The `interface{}` type, the empty interface, is the source of much
confusion. The interface{} type is the interface that has no
methods. Since there is no implements keyword, all types implement at
least zero methods, and satisfying an interface is done automatically,
all types satisfy the empty interface. That means that if you write a
function that takes an `interface{}` value as a parameter, you can
supply that function with any value. So this function:

    func DoSomething(v interface{}) {
    // ...
    }

will accept any parameter whatsoever.

### Type assertions

- https://medium.com/golangspec/type-assertions-in-go-e609759c42e1



([code for: Basics Interfaces](https://github.com/naqvijafar91/go-workshops/tree/master/065-basics-interfaces))

## Error handling

There is no exceptions in Go, errors are returned by value, or aggregated in intermediate objects. In go error is simply value which should be handled programatically as quick as possible.

Sources:
- https://blog.golang.org/errors-are-values
- http://blog.golang.org/error-handling-and-go
- http://davidnix.io/post/error-handling-in-go/



([code for: Basics Errors](https://github.com/naqvijafar91/go-workshops/tree/master/067-basics-errors))

## Panics

- Used when we want to stop the program.
- We can check if there was a `panic` occurence in function defer chain



([code for: Basics Panics](https://github.com/naqvijafar91/go-workshops/tree/master/068-basics-panics))

## Strings

In Go, a string is in effect a **read-only slice of bytes**.

It's important to state right up front that a string holds arbitrary bytes. It is not required to hold Unicode text, UTF-8 text, or any other predefined format. As far as the content of a string is concerned, it is exactly equivalent to a slice of bytes.

More on https://blog.golang.org/strings



([code for: Basics Strings](https://github.com/naqvijafar91/go-workshops/tree/master/070-basics-strings))

## Go routines

A goroutine is a lightweight thread of execution.

Goroutines run in the same address space, so access to shared memory must be synchronized. The sync package provides useful primitives, although you won't need them much in Go as there are other primitives (channels).

Channels are a typed conduit through which you can send and receive values with the channel operator, <-.



([code for: Basics Goroutines](https://github.com/naqvijafar91/go-workshops/tree/master/080-basics-goroutines))

## Using 3rd parties

In go we can get packages to our $GOPATH with use of `go get` command.


## DEP

```sh
go dep init
```

`dep` is fully-fledged dependency manager. It downloads all dependencies source code to `vendor` directory and then compilator includes those code during compilation process.



([code for: Basics 3rd Party Packages](https://github.com/naqvijafar91/go-workshops/tree/master/090-basics-3rd-party-packages))

## Basics Pointers



There is no README.md for Basics Pointers use ([code for: Basics Pointers](https://github.com/naqvijafar91/go-workshops/tree/master/090-basics-pointers)) link to follow code examples



## Other concurrency patterns

You've lerned about channels primitive on previous chapter of this workshops, now it's time to learn about some other ways of creating concurrent programs in go.

We'll be doing some code with:
- data races errors
- atomic counters
- mutexes
- wait groups



([code for: Concurrency Other](https://github.com/naqvijafar91/go-workshops/tree/master/100-concurrency-other))

## Channels

Channels are a typed conduit through which you can send and receive values with the channel operator, <-.

    ch <- v    // Send v to channel ch.
    v := <-ch  // Receive from ch, and
            // assign value to v.

(The data flows in the direction of the arrow.)

Like maps and slices, channels must be created before use:

    eventsChannel := make(chan int)

By default, **sends and receives block until the other side is ready**. This allows goroutines to synchronize without explicit locks or condition variables.

### Buffered Channels

Channels can be buffered. Provide the buffer length as the second argument to make to initialize a buffered channel:

    ch := make(chan int, 100)

Sends to a buffered channel **block only when the buffer is full**. Receives block when the buffer is empty.

### In this workshops you'll learn about:

- channels mechanics
- receiving data from channel
- channels length
- buffers
- channel closing
- generate data with channels
- timers, tickers with channels
- worker pool
- rate limiting with channels
- selecting proper channel stream
- pipeline and fan-in/fan-out patterns

Feel free to browse [channels chapter source code](100-concurrency-channels/)


([code for: Concurrency Channels](https://github.com/naqvijafar91/go-workshops/tree/master/101-concurrency-channels))

## Date time

Go has very powerful standard library, first and one of awesome library are is Date time.


([code for: Stdlib Date Time](https://github.com/naqvijafar91/go-workshops/tree/master/110-stdlib-date-time))

## Running commands in shell



([code for: Stdlib Os Processes](https://github.com/naqvijafar91/go-workshops/tree/master/110-stdlib-os-processes))

## Args and flags

One of important thing when runnein your program is to get some arguments from user.

in Go you can easily get those data using `os.Args` slice or more powerful package `flags`.

Additionally you can get environment variables from `os.Getenv` function in `os` package


([code for: Stdlib Args](https://github.com/naqvijafar91/go-workshops/tree/master/114-stdlib-args))

# Streams

Streams in go are very powerful feature, very large part of standard library is written as some kind of stream reader or stream writer.

Go have two basic interfaces shaping all world of data streams `io.Reader` and `io.Writer`.

In this section of workhops we'll try to cover some of use cases for each of them.



([code for: Stdlib Streams](https://github.com/naqvijafar91/go-workshops/tree/master/115-stdlib-streams))

## Basic IO operations

- `bufio` examples
- directory traversal
- merging files with use of `buffers`



([code for: Stdlib Io](https://github.com/naqvijafar91/go-workshops/tree/master/116-stdlib-io))

## Stdlib Logging package

Go has basic logging package to log what's happening in your program.


([code for: Stdlib Logging](https://github.com/naqvijafar91/go-workshops/tree/master/120-stdlib-logging))

## HTTP library

Package http provides HTTP client and server implementations.

HTTP is one of fundamental lib in programming. Go has implemented very powerful HTTP primitives which allows creation of full-fledged HTTP powered servers.

Info: there is no routing in stdlib so you need to implement your own or use third party libraries (Gorilla mux, Gin, Echo are ones who can help you)



([code for: Stdlib Http](https://github.com/naqvijafar91/go-workshops/tree/master/140-stdlib-http))

## HTTP Middlewares

Go is using the term `middleware`, but each language/framework calls the concept differently. `NodeJS` and `Rails` calls it `middleware`. In the `Java EE` (i.e. Java Servlet), it’s called `filters`. `C#` calls it `delegate handlers`.

Essentially, the middleware **performs some specific function** on the HTTP request or response **at a specific stage in the HTTP pipeline** before or after the user defined controller. Middleware is a design pattern to eloquently add cross cutting concerns like logging, handling authentication, or gzip compression without having many code contact points.



([code for: Stdlib Http Middlewares](https://github.com/naqvijafar91/go-workshops/tree/master/141-stdlib-http-middlewares))

## Stdlib Encoding Json



There is no README.md for Stdlib Encoding Json use ([code for: Stdlib Encoding Json](https://github.com/naqvijafar91/go-workshops/tree/master/150-stdlib-encoding-json)) link to follow code examples



## Stdlib Encoding Xml



There is no README.md for Stdlib Encoding Xml use ([code for: Stdlib Encoding Xml](https://github.com/naqvijafar91/go-workshops/tree/master/151-stdlib-encoding-xml)) link to follow code examples



## Templates

In programming we need often some meta templates who help us with interoperability between our code and many output formats. One example could be template engine for generating HTML files for web sites.

In Go there are template engines (yes plural!) implemented in `stdlib`!

We'll go in this chapter by some `html` and `text` template engines.


([code for: Stdlib Templates](https://github.com/naqvijafar91/go-workshops/tree/master/170-stdlib-templates))

## Stdlib Math



There is no README.md for Stdlib Math use ([code for: Stdlib Math](https://github.com/naqvijafar91/go-workshops/tree/master/180-stdlib-math)) link to follow code examples



## Stdlib Regexp



There is no README.md for Stdlib Regexp use ([code for: Stdlib Regexp](https://github.com/naqvijafar91/go-workshops/tree/master/180-stdlib-regexp)) link to follow code examples



## Context package

Context is very powerful package, in this section i've implemented HTTP client and server which handles cancelling both sides when client e.g. press Ctrl+C during request.


([code for: Stdlib Context](https://github.com/naqvijafar91/go-workshops/tree/master/181-stdlib-context))

## Stdlib Sort



There is no README.md for Stdlib Sort use ([code for: Stdlib Sort](https://github.com/naqvijafar91/go-workshops/tree/master/181-stdlib-sort)) link to follow code examples



## Stdlib Signal



There is no README.md for Stdlib Signal use ([code for: Stdlib Signal](https://github.com/naqvijafar91/go-workshops/tree/master/182-stdlib-signal)) link to follow code examples



## MySQL

Install instructions to run this section:

```sh
cd docker/mysql
docker-compose up
docker exec -it mysql_app_1 mysql -uroot -proot -P7701 -hlocalhost
```



([code for: Databases Mysql](https://github.com/naqvijafar91/go-workshops/tree/master/210-databases-mysql))

## ORMs in Go

### GORM the most popular Go ORM.

gorm have [some nice converntions](http://gorm.io/docs/conventions.html) to start with new project

full documentation is on http://gorm.io/docs/


### GORP - Go Object Relational Persistence

If you need some lighter abstraction on SQL driver (than full-fledged ORM)

https://github.com/go-gorp/gorp



([code for: Databases Orm](https://github.com/naqvijafar91/go-workshops/tree/master/215-databases-orm))

## Databases Redis


There is no README.md for Databases Redis use ([code for: Databases Redis](https://github.com/naqvijafar91/go-workshops/tree/master/240-databases-redis)) link to follow code examples



## Databases Bolt



There is no README.md for Databases Bolt use ([code for: Databases Bolt](https://github.com/naqvijafar91/go-workshops/tree/master/241-databases-bolt)) link to follow code examples



## Databases Postgresql



There is no README.md for Databases Postgresql use ([code for: Databases Postgresql](https://github.com/naqvijafar91/go-workshops/tree/master/250-databases-postgresql)) link to follow code examples



## Testing Unit Task



There is no README.md for Testing Unit Task use ([code for: Testing Unit Task](https://github.com/naqvijafar91/go-workshops/tree/master/300-testing-unit-task)) link to follow code examples



## Testing Unit Examples



There is no README.md for Testing Unit Examples use ([code for: Testing Unit Examples](https://github.com/naqvijafar91/go-workshops/tree/master/302-testing-unit-examples)) link to follow code examples



## Testing Unit Dependencies



There is no README.md for Testing Unit Dependencies use ([code for: Testing Unit Dependencies](https://github.com/naqvijafar91/go-workshops/tree/master/305-testing-unit-dependencies)) link to follow code examples



## Testing Http Handler



There is no README.md for Testing Http Handler use ([code for: Testing Http Handler](https://github.com/naqvijafar91/go-workshops/tree/master/310-testing-http-handler)) link to follow code examples



## Testing Http Server



There is no README.md for Testing Http Server use ([code for: Testing Http Server](https://github.com/naqvijafar91/go-workshops/tree/master/310-testing-http-server)) link to follow code examples



## Testing Benchmarking



There is no README.md for Testing Benchmarking use ([code for: Testing Benchmarking](https://github.com/naqvijafar91/go-workshops/tree/master/320-testing-benchmarking)) link to follow code examples



## Testing Parallel Benchmark



There is no README.md for Testing Parallel Benchmark use ([code for: Testing Parallel Benchmark](https://github.com/naqvijafar91/go-workshops/tree/master/380-testing-parallel-benchmark)) link to follow code examples



## Patterns Pipeline



There is no README.md for Patterns Pipeline use ([code for: Patterns Pipeline](https://github.com/naqvijafar91/go-workshops/tree/master/400-patterns-pipeline)) link to follow code examples



## Patterns Glow Map Reduce



There is no README.md for Patterns Glow Map Reduce use ([code for: Patterns Glow Map Reduce](https://github.com/naqvijafar91/go-workshops/tree/master/401-patterns-glow-map-reduce)) link to follow code examples



## Fullstack Html And Angular



There is no README.md for Fullstack Html And Angular use ([code for: Fullstack Html And Angular](https://github.com/naqvijafar91/go-workshops/tree/master/510-fullstack-html-and-angular)) link to follow code examples



## Fullstack Rest Angular Resource



There is no README.md for Fullstack Rest Angular Resource use ([code for: Fullstack Rest Angular Resource](https://github.com/naqvijafar91/go-workshops/tree/master/520-fullstack-rest-angular-resource)) link to follow code examples



## Fullstack Json Event Stream



There is no README.md for Fullstack Json Event Stream use ([code for: Fullstack Json Event Stream](https://github.com/naqvijafar91/go-workshops/tree/master/530-fullstack-json-event-stream)) link to follow code examples



## Fullstack Websockets



There is no README.md for Fullstack Websockets use ([code for: Fullstack Websockets](https://github.com/naqvijafar91/go-workshops/tree/master/540-fullstack-websockets)) link to follow code examples



## Fullstack Wiki



There is no README.md for Fullstack Wiki use ([code for: Fullstack Wiki](https://github.com/naqvijafar91/go-workshops/tree/master/560-fullstack-wiki)) link to follow code examples



## Beego

Bee init script - inicjuje podstawową strukturę katalogów.
hot compile.

```
go get github.com/astaxie/beego
go get github.com/beego/bee
bee new hello
cd hello
bee run hello
```



([code for: Fullstack Beego](https://github.com/naqvijafar91/go-workshops/tree/master/570-fullstack-beego))

## Perks for Go (golang.org)

> Perks contains the Go package quantile that computes approximate quantiles over an unbounded data stream within low memory and CPU bounds.



([code for: Libs Quantile Percentiles](https://github.com/naqvijafar91/go-workshops/tree/master/602-libs-quantile-percentiles))

## Libs Beep



There is no README.md for Libs Beep use ([code for: Libs Beep](https://github.com/naqvijafar91/go-workshops/tree/master/610-libs-beep)) link to follow code examples



## BRA

autoreload of your services on file change

### Install first

```
go get -u github.com/Unknwon/bra

bra init
bra run
```



([code for: Libs Bra](https://github.com/naqvijafar91/go-workshops/tree/master/610-libs-bra))

## Libs Slack



There is no README.md for Libs Slack use ([code for: Libs Slack](https://github.com/naqvijafar91/go-workshops/tree/master/611-libs-slack)) link to follow code examples



## Libs Vegeta



There is no README.md for Libs Vegeta use ([code for: Libs Vegeta](https://github.com/naqvijafar91/go-workshops/tree/master/620-libs-vegeta)) link to follow code examples



# go readline implementation

https://github.com/chzyer/readline



([code for: Libs Readline](https://github.com/naqvijafar91/go-workshops/tree/master/630-libs-readline))

## Libs Termbox



There is no README.md for Libs Termbox use ([code for: Libs Termbox](https://github.com/naqvijafar91/go-workshops/tree/master/640-libs-termbox)) link to follow code examples



## Caddy webserver



([code for: Libs Caddy](https://github.com/naqvijafar91/go-workshops/tree/master/650-libs-caddy))

## Libs Http Echo



There is no README.md for Libs Http Echo use ([code for: Libs Http Echo](https://github.com/naqvijafar91/go-workshops/tree/master/651-libs-http-echo)) link to follow code examples



## Libs Http Iris



There is no README.md for Libs Http Iris use ([code for: Libs Http Iris](https://github.com/naqvijafar91/go-workshops/tree/master/651-libs-http-iris)) link to follow code examples



## Libs Jobrunner



There is no README.md for Libs Jobrunner use ([code for: Libs Jobrunner](https://github.com/naqvijafar91/go-workshops/tree/master/660-libs-jobrunner)) link to follow code examples



## Libs Cron



There is no README.md for Libs Cron use ([code for: Libs Cron](https://github.com/naqvijafar91/go-workshops/tree/master/665-libs-cron)) link to follow code examples



## Validator package

- https://github.com/go-playground/validator

- https://github.com/go-validator/validator

- https://github.com/asaskevich/govalidator



([code for: Libs Validator](https://github.com/naqvijafar91/go-workshops/tree/master/670-libs-validator))

## Libs Gographviz



There is no README.md for Libs Gographviz use ([code for: Libs Gographviz](https://github.com/naqvijafar91/go-workshops/tree/master/677-libs-gographviz)) link to follow code examples



## Libs Fasthttp



There is no README.md for Libs Fasthttp use ([code for: Libs Fasthttp](https://github.com/naqvijafar91/go-workshops/tree/master/680-libs-fasthttp)) link to follow code examples



## Libs Uiprogress



There is no README.md for Libs Uiprogress use ([code for: Libs Uiprogress](https://github.com/naqvijafar91/go-workshops/tree/master/681-libs-uiprogress)) link to follow code examples



## Libs Termui



There is no README.md for Libs Termui use ([code for: Libs Termui](https://github.com/naqvijafar91/go-workshops/tree/master/682-libs-termui)) link to follow code examples



## Libs Emoji



There is no README.md for Libs Emoji use ([code for: Libs Emoji](https://github.com/naqvijafar91/go-workshops/tree/master/688-libs-emoji)) link to follow code examples



## Libs Go Rpm



There is no README.md for Libs Go Rpm use ([code for: Libs Go Rpm](https://github.com/naqvijafar91/go-workshops/tree/master/690-libs-go-rpm)) link to follow code examples



## Libs Grpc



There is no README.md for Libs Grpc use ([code for: Libs Grpc](https://github.com/naqvijafar91/go-workshops/tree/master/690-libs-grpc)) link to follow code examples



## Libs Logrus



There is no README.md for Libs Logrus use ([code for: Libs Logrus](https://github.com/naqvijafar91/go-workshops/tree/master/690-libs-logrus)) link to follow code examples



## Libs Consul



There is no README.md for Libs Consul use ([code for: Libs Consul](https://github.com/naqvijafar91/go-workshops/tree/master/692-libs-consul)) link to follow code examples



## Libs Language Bindings



There is no README.md for Libs Language Bindings use ([code for: Libs Language Bindings](https://github.com/naqvijafar91/go-workshops/tree/master/693-libs-language-bindings)) link to follow code examples



## Libs Bigcache



There is no README.md for Libs Bigcache use ([code for: Libs Bigcache](https://github.com/naqvijafar91/go-workshops/tree/master/695-libs-bigcache)) link to follow code examples



## Libs Complete



There is no README.md for Libs Complete use ([code for: Libs Complete](https://github.com/naqvijafar91/go-workshops/tree/master/696-libs-complete)) link to follow code examples



## Libs Prometheus



There is no README.md for Libs Prometheus use ([code for: Libs Prometheus](https://github.com/naqvijafar91/go-workshops/tree/master/696-libs-prometheus)) link to follow code examples



# AWS Lambda Golang

https://aws.amazon.com/blogs/compute/announcing-go-support-for-aws-lambda/

## Remember to build your handler executable for Linux!

    GOOS=linux GOARCH=amd64 go build -o main main.go
    zip main.zip main


## Deploying

https://docs.aws.amazon.com/lambda/latest/dg/deploying-lambda-apps.html

    aws lambda create-function \
    --region us-west-1 \
    --function-name HelloFunction \
    --zip-file fileb://./main.zip \
    --runtime go1.x \
    --tracing-config Mode=Active \
    --role arn:aws:iam::<account-id>:role/<role> \
    --handler main


aws lambda create-function --region us-west-1 --function-name HelloFunction --zip-file fileb://./deployment.zip --runtime go1.x --tracing-config Mode=Active --role arn:aws:iam::270605981035:role/<role> --handler main



([code for: Lambda Simple](https://github.com/naqvijafar91/go-workshops/tree/master/700-lambda-simple))

## How To Run On Production



There is no README.md for How To Run On Production use ([code for: How To Run On Production](https://github.com/naqvijafar91/go-workshops/tree/master/800-how-to-run-on-production)) link to follow code examples



## Debugging with Delve

https://github.com/derekparker/delve/tree/master/Documentation


([code for: Debugging Delve](https://github.com/naqvijafar91/go-workshops/tree/master/950-debugging-delve))



## Profiling

### Command

Profilowanie standardowego programu

```
import (
	"runtime/pprof"
)

var cpuprofile = flag.String("cpuprofile", "", "write cpu profile to file")

func init() {
	flag.Parse()
	if *cpuprofile != "" {
		f, err := os.Create(*cpuprofile)
		if err != nil {
			log.Fatal(err)
		}
		pprof.StartCPUProfile(f)
	}
}

func main() {
	defer pprof.StopCPUProfile()

```


Następnie budujemy binarkę i odpalamy ją z flagą cpuprofile

```
go build command.go && ./command -cpuprofile=data.prof
```

po czym możemy włączyć nasz profiler

```
go tool pprof command data.prof
```

Możemy do naszego programu dodać memory profile

```
var memprofile = flag.String("memprofile", "", "write memory profile to this file")


func memProfile() {
	if *memprofile != "" {
		f, err := os.Create(*memprofile)
		if err != nil {
			log.Fatal(err)
		}
		pprof.WriteHeapProfile(f)
		f.Close()
		return
	}
}
```

informacje o pamięci zbierane są zbierane na końcu więc dorzucamy do defer list
```
func main() {
    defer memProfile()

```

Teraz możemy zbierać informacje o obu profilach

```
go build command.go && ./command -cpuprofile=cpu.prof -memprofile=mem.prof

go tool pprof command cpu.prof

go tool pprof command mem.prof
```


### Web

```
package main

import (
	"fmt"
	"net/http"
	_ "net/http/pprof"
)

func handler(w http.ResponseWriter, r *http.Request) {
	for i := 0; i < 100000000; i++ {
		w.Write([]byte(fmt.Sprintf("%d - %d, ", i, i)))
	}
}

func main() {
	http.HandleFunc("/", handler)
	http.ListenAndServe(":8080", nil)
}

```


run in shell:

```
go tool pprof http://localhost:8080/debug/pprof/profile
```



([code for: Profiling](https://github.com/naqvijafar91/go-workshops/tree/master/960-profiling))

## New Project



There is no README.md for New Project use ([code for: New Project](https://github.com/naqvijafar91/go-workshops/tree/master/999-new-project)) link to follow code examples



## Shooting Yourself In The Foot



There is no README.md for Shooting Yourself In The Foot use ([code for: Shooting Yourself In The Foot](https://github.com/naqvijafar91/go-workshops/tree/master/999-shooting-yourself-in-the-foot)) link to follow code examples

