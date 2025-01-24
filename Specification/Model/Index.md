# Model

Provides the model used by the modules to actually handle requests.

| Element | Description |
|---|---|
| [Handler](./Handler.md) | An interface that will accept a `Request` and may generate a `Response` for it. |
| [Concern](./Concern.md) | A specialized `Handler` that wraps content to add behavior (e.g. authentication). |
| [Request](./Request.md) | Represents a HTTP request sent by the client. |
| [Response](./Response.md) | Represents a HTTP response sent to the client. |
| [Target](./Target.md) | An object representing the requested resource on the server. |
| [Content Type](./ContentType.md) | Specifies the kind of content sent or received by the server. |
| [Cookie](./Cookie.md) | A cookie sent or received by the server. |
