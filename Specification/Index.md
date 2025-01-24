# Specification

This document describes how a binding has to be implemented.

## Integration

The main entry points for using a binding within a programming language. 
An integration may use one or multiple web servers to actually serve HTTP requests.

| Element | Description |
|---|---|
| [Host](./Integration/Host.md) | Configures a standalone server instance provided by an `Engine` and manages its lifecycle. Implemented once per binding. |
| [Engine](./Integration/Engine.md) | Integrates an existing web server engine so it can be used with a `Host`. One implementation per engine. |
| [Adapter](./Integration/Adapter.md) | Bridges calls from existing web server frameworks into the `Request` / `Response` model. Typically used by an engine to serve requests. One implementation per web server framework. |

## Model

Provides the model used by the modules to actually handle requests.

| Element | Description |
|---|---|
| [Handler](./Model/Handler.md) | An interface that will accept a `Request` and may generate a `Response` for it. |
| [Concern](./Model/Concern.md) | A specialized `Handler` that wraps content to add behavior (e.g. authentication). |
| [Request](./Model/Request.md) | Represents a HTTP request sent by the client. |
| [Response](./Model/Response.md) | Represents a HTTP response sent to the client. |

## Modules

Provide `Handler` or `Concern` instances to implement some functionality. One functionality per module, may
contain multiple handlers and concerns. The following list describes the modules
that a binding should provide, not implementing a module will cause a binding
to be marked as incomplete.

Module developers may provide their own implementations
outside of the binding projects as needed. Developers may submit a request
to add a module to the specification when they are useful to develop web services in general
and not vendor specific.

| Element | Description |
|---|---|
| [Layouting](./Modules/Layouting.md) | Structures an application and provides routing. |

## Concepts

Additional functionality and behavior shared between modules.

| Element | Description |
|---|---|
| TBD | TBD |
