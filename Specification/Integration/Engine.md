# Engine

Provides the implementation to actually listen for HTTP requests and to
feed them into the handler pipeline. Created and managed by the `Host`.

## Example

```csharp
// managed by host
var engine = new SomeEngine(config);

engine.Start();

// destroy the instance using a pattern depending on the platform
engine.Dispose(); 
```

## Engine Implementation

Engines will be created by the host with a binding specific 
configuration object that contains all information about 
endpoints and other settings to be respected by the engine. 
After the engine has been created, it can be started to actually 
start listening.

As engines are not intended to be directly used by app
developers there are not strict implementation rules for them.

## Adapters

For each web server technology there should be a an adapter that allows to map requests
without the overhead of a full engine. This allows developers to use Same HTTP modules
within their existing applications without the need of replacing the engine alltogether.

The syntax for adapters is not defined in this specification as it is probably quite specific
to the web server technology. Example:

```csharp
return Adapter.MapRequest(frameworkRequest);
```

## Preparation

Before the engine is started, it must `Prepare()` the given handler instance.

## Error Handling

Engines must wrap the `Handler` passed by the user into the default `ErrorHandler` to ensure that
the server will always generate HTTP responses.

## Dependency Free

An engine implementation must not rely on any external dependency
such as configuration files or static variables. Creating a `Host` instance
and registering the engine must be sufficient.