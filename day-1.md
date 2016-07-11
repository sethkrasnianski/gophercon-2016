# Understanding nil

Is it a constant? A variable? Where is it defined? What is its type? It has no type? It has all the types?

- [Tony Hoare](https://en.wikipedia.org/wiki/Tony_Hoare) - Invented null reference.
- Go read the [go language specification](https://golang.org/ref/spec).

> Make the sero value useful
Rob Pike

## When is nil not nil?

```go
func do() error {
  return nil
}

func main() {
  err := do()
  fmt.Println(err == nil)
}
```

## Trying it out

```go
type person struct {}
func sayHi(p * person)
func (p *person) sayHi()
var p *person
```

Spoken by [Francesc Campoy Flores](https://github.com/campoy)

## Navigating unfamiliar code with the Go Guru

The Go [Guru](http://golang.org/x/tools/cmd/guru) is an “editor-integrated tool for code comprehension and navigation”.

Spoken by [Alan Donovan](https://github.com/adonovan)

## Go for Data Science

What is data science? (Two Sigma)

Leveraging data sets to make insights or predictions.

- ETL
- Data Cleaning
- Organization
- Parsing
- Extraction of Patterns
- Arithmetic

Go offered more security than a language such as Python.

Able to leverage the plethora of useful Go packages.

- [pachyderm](https://github.com/pachyderm/pachyderm)
- PFS File System
- [gonum](https://github.com/gonum)
- [regression](https://github.com/sajari/regression)
- [errors](https://github.com/pkg/errors)

Spoken by [Daniel Whitenack](https://github.com/dwhitena)

## Don’t Just Check Errors, Handle Them Gracefully

> A Frog in a Well Knows Nothing of the Great Ocean.

> Errors are just values.
- Go Proverb

### Programming with errors

Sentinel errors

- io.EOF would be an example
- Never inspect the output of `error.Error()`.
- Sentinel errors create a dependency between two packages.

```go
if err == ErrSomething { ... }
```

Conclusion: avoid sentinel errors

### Error Types

Type that you create which implements the error interface.

- Type assertion

Conclusion: avoid error types

### Opaque errors

- Assert errors for behavior not type.
- Treat all errors as opaque; assert error for behavior, not type.
- Convert errors to opaque errors with errors.Wrap.
- User errors.Cause if you need to recover the underlying cause and inspect it.

Proverbs aren't just stories with lessons.

Spoken by [Dave Cheney](https://github.com/davecheney)

## Go Vendoring Deconstructed

- Go 1.5 introduced experimental support for local vendor imports.
  - First in `vendor/` (in `$GOPATH`)
  - Then in parent's `vendor/` directory
  - `$GOROOT`
  - `$GOPATH`

Spoken by [Wisdom Omuya](https://github.com/deafgoat)

## Visualizing Concurrency in Go

Concurrency in Go has been explained many times in a variety of articles, but there is time to explain it visually using the power of 3D modeling and animations.


- People visualize abstract concepts differently.
- Gotrace - WebGL

_presentation included motion detection to move his visualizations with his hands_

Spoken by [Ivan Daniluk](https://github.com/divan)
