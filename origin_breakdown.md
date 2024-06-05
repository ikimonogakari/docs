# Domain, host, origin - what is what?

Navigating through CORS and other browser-enforced limitations is tough when you don't have this terminology locked down, so I've summarized what's what.

This sample URL is used as a reference below
`https://developer.apple.com/documentation/accelerate?language=objc`

## Domain
`com` = top-level domain or TLD

`apple` = domain

`developer` = sub-domain (not always present)

`developer.apple.com` = fully qualified domain name or FQDN

Sometimes just "domain" is used when referring to the fully qualified domain.

## Host
`developer.apple.com` = host, but would include port if there was one

`developer.apple.com` = hostname, which doesn't include port and in some documentation it appears to only refer to the sub-domain

## URL scheme
`https` = scheme

A scheme is an identifier or designator of a protocol, not the protocol itself. For example, `https` is the identifier used to tell the browser to follow the Hypertext Transfer Protocol Secure protocol for our reference URL. Other identifiers are used to tell the browser to follow other protocols, like mailto and ftp.

## Origin
`https://developer.apple.com` = origin

The origin includes scheme, hostname (if present), host, and port (if present). Like this:
```html
<scheme>://[<hostname>.]<host>[:<port>]
```
"Same-origin" means the client has the same origin as the server it's calling, for example:
```js
// Browser JavaScript running on https://foo.bar.com making this call is same-origin
fetch('https://foo.bar.com')
```
"Cross-origin" means the client origin is different than the server it's calling. Assuming the same JavaScript from above we get:
```js
// Cross-origin because the scheme is different
fetch('http://foo.bar.com')

// Cross-origin because the domains differ (sub-domains don't get a free pass)
fetch('https://bar.com')

// Cross-origin because the port is different
fetch('https://foo.bar.com:80')
```

## Path
`/documentation/accelerate` = path

Browsers don't enforce any communication rules as far as the path is concerned (they do set a really long max length though). The path references what is considered a "resource" and the server, not the browser, determines if the request is authorized to access those resources.

## Parameters
`?language=objc` = query parameter string

Like path, there's no communication rules being enforced.

---

Well, I hope that helps someone. Feel free to suggest corrections/clarifications (host still seems ambiguous at times).

If you need to get more details on CORS, I highly recommend Javascript.info's [excellent explanation](https://javascript.info/fetch-crossorigin).
