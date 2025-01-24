# Model

Provides the model used by the modules to actually handle requests.

| Element | Description |
|---|---|
| [Handler](./Model/Handler.md) | An interface that will accept a `Request` and may generate a `Response` for it. |
| [Concern](./Model/Concern.md) | A specialized `Handler` that wraps content to add behavior (e.g. authentication). |
| [Request](./Model/Request.md) | Represents a HTTP request sent by the client. |
| [Response](./Model/Response.md) | Represents a HTTP response sent to the client. |
