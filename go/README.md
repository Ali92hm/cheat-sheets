# Go cheat sheet

## Setup

### $GOPATH
Go uses the `$GOPATH` directory to manage files, packages, and dependencies. 

Make sure to set `$GOPATH` in `.profile`

```
export GOPATH=${HOME}/go
```

### Useful commands
#### Pulling dependencies
```
go get github.com/<package-path>
```

#### Building project
```
go build
```

#### Build and run
```
go run
```

#### Cleaning the working directory
```
go clean
```

#### Compile and install packages
```
go install
```
This command compiles all packages and generates files, then moves them to $GOPATH/pkg or $GOPATH/bin.

#### Lint the source code
```
go fmt
```

#### Run tests
```
go test // runs all files named *_test.go
```

#### Documentation 
```
godoc -http=:8080
```

Runs the documentation on local server

## Style Guide

Go comes with an official style guide. Use `go fmt` to format files. There is Sublime package called [GoSublime](https://github.com/DisposaBoy/GoSublime) that helps with linting, code completion, etc.

## Basics
### Hello World
```
package main

import (
	"fmt"
)

func main() {
	fmt.Printf("Hello, world or 你好，世界 or Καλημέρα κόσμε or こんにちは世界\n")
}

```

### Syntax
#### Variable declaration
```GO
var variableName type
```








