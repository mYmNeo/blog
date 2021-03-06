---
title: golang memo
date: 2016-04-28 18:06:41
tags: 
    - programme
    - golang
---
+ tell you file and line number like C

```golang
runtime.Caller(0)
```

+ iterate over some field in structure

```golang
package main

import "fmt"
import "reflect"
import "strings"

type MyStruct struct {
    A,B,C string
    I int
    D string
    J int
}

func main() {
    ms := MyStruct{"Green ", " Eggs", " and ", 2, " Ham      ", 15}
    // Print it out now so we can see the difference
    fmt.Printf("%s%s%s%d%s%d\n", ms.A, ms.B, ms.C, ms.I, ms.D, ms.J)

    // We need a pointer so that we can set the value via reflection
    msValuePtr := reflect.ValueOf(&ms)
    msValue := msValuePtr.Elem()

    for i := 0; i < msValue.NumField(); i++ {
        field := msValue.Field(i)

        // Ignore fields that don't have the same type as a string
        if field.Type() != reflect.TypeOf("") {
            continue
        }

        str := field.Interface().(string)
        str = strings.TrimSpace(str)
        field.SetString(str)
    }
    fmt.Printf("%s%s%s%d%s%d\n", ms.A, ms.B, ms.C, ms.I, ms.D, ms.J)
}
```

+ underscore usage

1. used in import

- invoke the `init` function but not import other function of this package

```go
import _ "net/http/pprof"
```

1. user in returned value

- ignore the some value

```go
for _, v := range Slice{}
```

1. used in variable

- type assertion

```go
type T struct{}
var _ I = T{} # judge whether type T has implements I interface, if not, raise an error while compiling
```

+ cgo

1. Refer to a C struct field named `type`

> Within the Go file, C identifiers or field names that are keywords in 
> Go can be accessed by prefixing them with an underscore: if x points 
> at a C struct with a field named "type", x._type accesses the field

2. export go function to c library

```golang
//export <function>
```

> Notice, you can't add space between // and export, but you can add space when import c header file 
> or add `#cgo`

3. when convert Go string to char* or Go []byte slice to C array, don't forget free the memory, other transformation doesn't has to do so

```golang
cstr := C.CString("hello")
C.free(unsafe.Pointer(cstr))

cbytes := C.CBytes([]byte)
C.free(cbytes)

// C string to Go string
func C.GoString(*C.char) string

// C data with explicit length to Go string
func C.GoStringN(*C.char, C.int) string

// C data with explicit length to Go []byte
func C.GoBytes(unsafe.Pointer, C.int) []byte
```

4. basic type of C in different package is not the same type, that means

```golang
package pkg1

func test(arg C.char) {}

package pkg2

func test(arg C.char) {}
```

the type of `arg` is not the same

+ goroutine

goroutine use a small stack to save variables and current procedure. It will generate a new thread if current goroutine is blocked by some reason such as `Open` or `Write` (https://groups.google.com/forum/#!topic/golang-nuts/2IdA34yR8gQ)

If you change the namespace(network etc) in goroutine by `setns`, the current thread's namespace is changed, next time a new goroutine maybe execute it code in this thread, but it does not work well because the thread's namespace has been changed. And also if you change environment in goroutine. It will affect the whole process environment.

Here is an example:

```golang
package main

import (
	"fmt"
	"io"
	"os"
	"os/exec"
	"syscall"
	"time"
)

var (
	forked = false
)

func init() {
	if len(os.Args) > 1 {
		forked = true
	}
}

func main() {
	if forked {
		forklnk, _ := os.Readlink(fmt.Sprintf("/proc/%d/task/%d/ns/net", os.Getpid(), syscall.Gettid()))
		fmt.Printf("forked network namespace: %s\n", forklnk)
		os.Exit(0)
	}

	origin, _ := os.Readlink(fmt.Sprintf("/proc/%d/task/%d/ns/net", os.Getpid(), syscall.Gettid()))
	fmt.Printf("origin network namespace: %s\n", origin)

	r, w, err := os.Pipe()
	if err != nil {
		fmt.Printf("pipe: %+v\n", err)
	}

	start := make(chan int, 1)

	go func() {
		start <- 1
		f, _ := syscall.Open("/proc/1/ns/net", syscall.O_RDONLY, 0)
		init, _ := os.Readlink("/proc/1/ns/net")
		fmt.Printf("init network namespace: %s\n", init)

		os.Setenv("HELLO", "k")

		syscall.Syscall(308, uintptr(f), uintptr(0x40000000), 0)
		cmd := exec.Command("/proc/self/exe", "fork")
		cmd.Stdout = w
		cmd.Run()
		cmd.Wait()
		r.Close()
		w.Close()
	}()

	afterlnk, _ := os.Readlink(fmt.Sprintf("/proc/%d/task/%d/ns/net", os.Getpid(), syscall.Gettid()))
	fmt.Printf("after network namespace: %s\n", afterlnk)

	<-start
	for {
		_, err := io.Copy(os.Stdout, r)

		if err != nil {
			break
		}
	}

	if len(os.Getenv("HELLO")) > 0 {
		fmt.Printf("outer env: %s\n", os.Getenv("HELLO"))
	}

	for {
		go func() {
			if len(os.Getenv("HELLO")) > 0 {
				fmt.Printf("inter env: %s\n", os.Getenv("HELLO"))
			}

			inner, _ := os.Readlink(fmt.Sprintf("/proc/%d/task/%d/ns/net", os.Getpid(), syscall.Gettid()))
			fmt.Printf("inner network namespace: %s\n", inner)
		}()
		time.Sleep(time.Second)
	}
}
```

Outputs:

```bash
# go build test.go && unshare -n ./test
origin network namespace: net:[4026532300]
after network namespace: net:[4026532300]
init network namespace: net:[4026531969]
forked network namespace: net:[4026531969]
outer env: k
inter env: k <- environment changed
inner network namespace: net:[4026532300] <- origin namespace
inter env: k
inner network namespace: net:[4026531969]
inter env: k
inner network namespace: net:[4026531969] <- change namspace
inter env: k
inner network namespace: net:[4026531969]
inter env: k
inner network namespace: net:[4026531969]
```

To avoid this situation happened, you must be careful about your code. DO NOT CHANGE THE CONTEXT IN GOROUTINES

+ golang bit operation

1. revert bits
```golang
a := ^a // ~a in C
```
2. change sign
```golang
a := ^a + 1 // ~a + 1 in C
```
3. shift
```golang
a := a << 1 // a << 1 in C
a := a >> 1 // a >> 1 in C
```

+ resolve error: "no buildable Go source files in"

Check if the package which shows error “no buildable Go source files in” is using C code, like

```golang
import "C"
```

in the source file, in that case, we might see an error, when we try to compile as “go build”, most probably when we try to cross compile that code,

The solution is to add “CGO_ENABLED=1” while building the code,

```golang
CGO_ENABLED=1 go build
```

+ Use the reflect package to get the string keys from a map with arbitrary value type

```golang
func Keys(v interface{}) ([]string, error) {
  rv := reflect.ValueOf(v)
  if rv.Kind() != reflect.Map {
    return nil, errors.New("not a map")
  }
  t := rv.Type()
  if t.Key().Kind() != reflect.String {
    return nil, errors.New("not string key")
  }
  var result []string
  for _, kv := range rv.MapKeys() {
    result = append(result, kv.String())
  }
  return result, nil
}
```

+ Custom Tag

```golang
package main

import (
  "fmt"
  "reflect"
)

// Name of the struct tag used in examples
const tagName = "validate"

type User struct {
  Id    int    `validate:"-"`
  Name  string `validate:"presence,min=2,max=32"`
  Email string `validate:"email,required"`
}

func main() {
  user := User{
    Id:    1,
    Name:  "John Doe",
    Email: "john@example",
  }

  // TypeOf returns the reflection Type that represents the dynamic type of variable.
  // If variable is a nil interface value, TypeOf returns nil.
  t := reflect.TypeOf(user)

  // Get the type and kind of our user variable
  fmt.Println("Type:", t.Name())
  fmt.Println("Kind:", t.Kind())

  // Iterate over all available fields and read the tag value
  for i := 0; i < t.NumField(); i++ {
    // Get the field, returns https://golang.org/pkg/reflect/#StructField
    field := t.Field(i)

    // Get the field tag value
    tag := field.Tag.Get(tagName)

    fmt.Printf("%d. %v (%v), tag: '%v'\n", i+1, field.Name, field.Type.Name(), tag)
  }
}
```

+ Iterate slice

```golang
package main

import "fmt"
import "reflect"

func main() {
    data := []string{"one","two","three"}
    test(data)
    moredata := []int{1,2,3}
    test(moredata)
} 

func test(t interface{}) {
    switch reflect.TypeOf(t).Kind() {
    case reflect.Slice:
        s := reflect.ValueOf(t)

        for i := 0; i < s.Len(); i++ {
            fmt.Println(s.Index(i))
        }
    }
}
```

+ Get the Field of the Type Definition not of the Value

```golang
package main

import "fmt"
import "reflect"

type A struct {
   Foo string
}

func (a *A) PrintFoo(){
    fmt.Println("Foo value is " + a.Foo)
}

func main() {
        a := &A{Foo: "afoo"}
        val := reflect.Indirect(reflect.ValueOf(a))
        fmt.Println(val.Type().Field(0).Name)
}
```