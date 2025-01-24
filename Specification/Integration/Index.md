# Integration

The main entry points for using a binding within a programming language. 
An integration may use one or multiple web server technologies to actually serve HTTP requests.

| Element | Description |
|---|---|
| [Host](./Host.md) | Configures a standalone server instance provided by an `Engine` and manages its lifecycle. Implemented once per binding. |
| [Engine](./Engine.md) | Integrates an existing web server engine so it can be used with a `Host`. One implementation per engine. |
| [Adapter](./Adapter.md) | Bridges calls from existing web server frameworks into the `Request` / `Response` model. Can be used without an engine or host. Typically used by an engine to serve requests. One implementation per web server framework. |
