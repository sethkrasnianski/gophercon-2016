# Serving HTTP in GO

Go has all the tolls you need to build an API at any level of complexity in the STDlib.

## Architecture

- package net/http
- "mux" ServeMux
- Handler interface

One goroutine per incoming request. Each goroutine services the request and terminates when the request is complete.

- Really good perf because of how the scheduler handles IO waiting.

## Routing

- `DefaultServeMux` is created for you if you create an http server.
- Add handlers by adding Handle and `HandleFunc` functions.
- `ServeMux` is a Handler, and you can nest them... confusing.

## Error Handling

At the most simple level, you can send an error back tot the client by using the `Error()` function.

## Middleware

Code that runs before or after your business functionality. Simple in Go.

- Log every request.
- Enforce AAA rules (Authz, Authc, Access Control).
- Inject headers into a request or a response.
- Capture metrics about each request


## Alternative Muxes

If there is one weakness in Go's http package, it's the inflexibility of the `http.ServeMux`.

- Can't register capture variables in the path
    `/api/users/{userid}`
- Can't call different functions based on request's HTTP verb
    GET /api/users -> `getUsers()`
    POST /api/users -> `newUser()`
- Can't differentiate based on request host or scheme
    www.me.com -> `serveMe()`
    https -> `serveSecure()` 

## Alternatives

If you're not allergic to taking on a dependency, there are several great options for alternative muxes. We'll explore a few, and give a full example of our previous app with Gorilla Mux.
- gorilla Mux
- httprouter
- pat
- xmux (adds net/context support)
