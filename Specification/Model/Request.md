# Request

A `Request` instance is created by the server engine as soon as a request
has been read from a client connection.

## Definition

A request must feature the following members:

| Member | Implementation |
|---|---|
| `Respond()` | Creates a `Response` object that can be configured and returned by the handler.  |
| `Endpoint` | The `Endpoint` the request originates from (see below). |
| `Client` | The `ClientConnection` that represents the remote client (see below). |
| `Protocol` | The `HttpProtocol` used in this connection (see below). |
| `Method` | The `FlexibleRequestMethod` of the request (see below). |
| `Target` | The `RoutingTarget` of the request (see [target](./Target.md)). |
| `Headers` | A read-only `string` dictionary containing the HTTP headers of the request. |
| `Query` | A read-only `string` dictionary containing the query parameters of the request. |
| `Cookies` | A read-only dictionary containing `Cookie` entries sent by the client (see [cookie](./Cookie.md)).
| `ContentType` | The `FlexibleContentType` of the content passed by the client, if any (see [content type](./ContentType.md)). |
| `Content` | The data passed by the client in a platform specific streaming type, if any. |

## Endpoint

| Member | Implementation |
|---|---|
| `Address` | The IP address the endpoint receiving the request is bound to (if any). |
| `Port` | The port number the endpoint receiving the request is bound to. |
| `Secure` | Boolean value that indicates whether the request has been received via a TLS secured endpoint. |

## Client Connection

| Member | Implementation |
|---|---|
| `Address` | The IP address of the connected client. |
| `Certificate` | The certificate presented by the client to connect (if any). |

## HTTP Protocol

An enum value out of HTTP `1.0`, `1.1`, `2` or `3`.

## Flexible Request Method

A combined structure consisting of the raw method read from the wire 
and the parsed enum value, if any.

| Member | Implementation |
|---|---|
| `RawMethod` | The method as read from the wire (e.g. `GET`), serialized as `string`. |
| `KnownMethod` | The parsed `RequestMethod` enum value, if any. |

The parsed value may be one of `Get`, `Head`, `Post`, `Put`, `Patch`, `Delete`, `Options`, `PropFind`, `PropPatch`, `MkCol`, `Copy`, `Move`, `Lock`, `Unlock`.
