# Response

Represents a `Response` to be sent to the connected client.

## Definition

A response must feature the following members:

| Member | Implementation |
|---|---|
| `Status` | The status code of the response (see below). |
| `Upgraded` | If set, the engine will surrender this connection, e.g. to a websocket that generated this response. |
| `Headers` | A `string` dictionary with the headers to be sent. |
| `Cookies` | A list of [cookies](./Cookie.md) to be sent. |
| `ContentType` | The type of content to be sent (see [content type](./ContentType.md)). |
| `ContentEncoding` | The encoding of the content, if any. |
| `Content` | The actual body of the response (see below). |

## Flexible Response Status

Allows to send a custom response status to the client.

| Member | Implementation |
|---|---|
| `Phrase` | The phrase to be sent, such as `OK`, serialized as `string`. |
| `RawStatus` | The code to be sent, such as `200`. |
| `KnownStatus` | The response status represented by a enum value, if possible. |

The enum is defined as in the HTTP specification.

## Response Content

An interface that can be implemented by modules to actually serve content.
Will be processed by the engine to actually write the body.

| Member | Implementation |
|---|---|
| `Length` | The size of the content in bytes, if known. |
| `Write(...)` | Writes the data to the passed platform type representing the response body (e.g. a stream). | 
| `CalculateChecksum()` | Generates a integer checksum for the content, used for caching purposes. |

If the response content does not indicate a content length, the engine must apply chunked transfer encoding.