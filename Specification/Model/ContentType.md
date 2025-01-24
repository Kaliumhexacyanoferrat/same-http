# Content Type

The `FlexibleContentType` specifies the type of content received or sent by the server.

## Members

| Member | Implementation |
|---|---|
| `RawType` | The method as read from the wire (e.g. `application/json`), serialized as `string`. |
| `KnownType` | The parsed `ContentType` enum value, if any. |
| `Charset` | An optional `string` specifying the charset of the content, such as `utf-8`. |

## Known Values

// TBD, probably in a good way to be used by the bindings 