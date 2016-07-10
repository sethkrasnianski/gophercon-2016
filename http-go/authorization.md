# Authentication, Authorization, Access Control

Semantic matters:

- Authentication: assert identity of API user (e.g. login)
- Authorization: allow or deny access to resources (e.g. access denied for non authenticated users)
- Access Control: rules that dictate who can do what (e.g. RBAC)

## BasicAuth in Go

Support built-in in http package.

## API Key / Shared secret

Not very secure, only use as second level of defense (e.g. behind firewalls, in VPC etc.), use HTTPS. Does not allow authentication (at least not easily).

Credential is secret token known by both parties passed as header or query string value.
```
GET https://host.com/secured/resource
X-Shared-Secret: 5c4728f2b535aafc0c45b6563ef7fe424593c4cb602698b43705a1de6965c7aa
```

or

```
GET https://host.com/secured/resource?token=5c4728f2b535aafc0c45b6563ef7fe424593c4cb602698b43705a1de6965c7aa
```
## API Key / Shared secret in Go

Uses header or query string:

```go
r.Header.Get("X-Shared-Secret")

r.URL.Query().Get("token")
```
where `r` is a `*http.Request`.


## Client SSL

Uses SSL extension to allow clients to authenticate using X509 certificates.

Benefits:

- well established standard
- works everywhere
- no or very little code required.

Cons:

- does not enable authorization easily
- requires machinery for distributing and revoking certificates.

Works well if clients are known in advanced.


## JWT

Defines a way to send encrypted data ("claims") in a request, typically in the form of a header:

```
GET https://host.com/secured/resource
Authorization: Bearer <JWT>
```

where JWT is an encrypted JSON payload contains the claims and information required by the other party to assert the origin of the token and decrypt it.

Note that the JWT standard does not define how auth is performed to obtain the token in the first place.

The JWT claims may include any arbitrary data including a user identifier for authentication, roles for access control, expiry date etc

## OAuth2

OAuth2 enables 3 party auth where a client (e.g. Spotify app) may request access to a service resource (e.g. Facebook wall) on behalf of the resource owner (e.g. Facebook user).

```
+--------+                               +---------------+
|        |--(A)- Authorization Request ->|   Resource    |
|        |                               |     Owner     |
|        |<-(B)-- Authorization Grant ---|               |
|        |                               +---------------+
|        |                               +---------------+
|        |--(C)-- Authorization Grant -->| Authorization |
| Client |                               |     Server    |
|        |<-(D)----- Access Token -------|               |
|        |                               +---------------+
|        |                               +---------------+
|        |--(E)----- Access Token ------>|    Resource   |
|        |                               |     Server    |
|        |<-(F)--- Protected Resource ---|               |
+--------+                               +---------------+
```

[http://tools.ietf.org/html/rfc6749](http://tools.ietf.org/html/rfc6749)

## OAuth2 in Go

For services that need to integrate with OAuth2 providers (Facebook, Google, Twitter etc.) use the golang OAuth2 client package.

[https://github.com/golang/oauth2](https://github.com/golang/oauth2)

For services that need to be OAuth2 providers themselves use the osin package or the built-in goa support.

[https://github.com/RangelReale/osin](https://github.com/RangelReale/osin)
[https://goa.design](https://goa.design)

## What Should I Do?

For services that don't integrate with OAuth2 providers and don't need to
provide OAuth2 - JWT is a good choice as it tackles both authentication and authorization. Scopes a la OAuth2 can also be added to the claims to implement RBAC.

Use basic auth for the initial authentication then provide the client with a JWT.

As an improvement use a "2 legged OAuth2" scheme where the initial JWT (refresh token) is only good for retrieving access tokens (which could also be JWTs). These access tokens should be short lived, the client periodically re-creates access tokens using the refresh token.
