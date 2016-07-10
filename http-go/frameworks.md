# Frameworks

## Why?

- Reduce boilerplate
- Leverage components (middlewares, logging, auth, etc.)
- Benefit from work and experience of others
- Consistent methodology across teams

## Why not?

- Additional layer of complexity
- Go stdlib support is very good

Boils down to:

*Do not use a web framework because of old habits*

## Review Of Frameworks

*Disclaimer*: the Go web framework landscape tends to be volatile with new
frameworks coming up and other frameworks being obsoleted all the time. Part
of that volatility can be attributed to the fact that many developers coming
to Go feel compelled to fill what seems to be a gap only to realize later that
Go - for the most part - does not need such frameworks.

This section makes an attempt at covering some of the more "established"
frameworks that have been around for a little while.

## Gin

- One of the most popular frameworks
- Full featured
- "All in one"

[https://github.com/gin-gonic/gin](https://github.com/gin-gonic/gin)

## Echo

- Popular framework
- "swiss army knife" request context
- Similar in many ways to Gin, a bit more modular

[https://github.com/labstack/echo](https://github.com/labstack/echo)

## Goji

- Minimalistic and idiomatic API
- Leverages Go context

[https://github.com/goji/goji](https://github.com/goji/goji)

## goa

- Newcomer
- Design first
- Code generation

[https://github.com/goadesign/goa](https://github.com/goadesign/goa)
