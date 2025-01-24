# Host

The host provides an engine independent way of configuring and starting a server instance
that will listen to incoming HTTP requests. The host package must not reference
an engine implementation.

## Example

```csharp
var host = Host.Create()
               .UseKestrel() // select engine via extension
               .Content(handler)
               .Port(9000);

// start and stop our server
host.Start();
host.Stop();

// run our server in a blocking way until the process is exited
host.Run();
```

## Host Implementation

After creating the host, the following methods and properties must be provided by a binding:

| Method | Implementation |
|---|---|
| `Engine(...)` | Specifies how to create the `Engine` instance, e.g. by passing a lamdba function that accepts the host configuration and returns an engine instance.  |
| `Content(Handler | HandlerBuilder)` | Sets the root handler that will be invoked to actually execute requests. If a `HandlerBuilder` is passed, it will be built to get a `Handler` instance. |
| `Start()` | Creates an `Engine` instance, therefore listening for incoming requests. |
| `Stop()` | Stops an already started `Engine` instance. If not started, behaves like a NOP. |
| `Run()` | Creates an `Engine` instance and blocks execution until the process receives an exit signal. |
| `Port(int)` | Sets the port the engine should listen to. Defaults to `8080`. |
| `Bind(int, IP?, CertificateProvider?, ...)` | Configures the engine to listen to the specified port. If an IP address is specified, the server should only listen to connections on this IP, otherwise to any IP. If a `CertificateProvider` is specified, the endpoint will be secured via TLS. Also see the binding details below. |
| `Development()` | Enables development mode on the server. |

## Binding Details

## Engine Interaction

The protocol between the `Engine` and the host is up to the binding implementation.
It is recommended that the host creates some kind of configuration structure that is then
passed to the engine.