# Host

The host provides an engine independent way of configuring and starting a server instance
that will listen to incoming HTTP requests. The host package must not reference
an engine implementation.

## Example

```csharp
var host = Host.Create()
               .UseKestrel() // select engine via extension
               .Handler(handler)
               .Bind(9000);

// start and stop our server
host.Start();
host.Stop();

// run our server in a blocking way until the process is exited
host.Run();
```

## Host Implementation

After creating the host, the following methods and properties must be provided by a binding:

| Member | Implementation |
|---|---|
| `Engine(...)` | Specifies how to create the `Engine` instance, e.g. by passing a lamdba function that accepts the host configuration and returns an engine instance.  |
| `Handler(Handler \| HandlerBuilder)` | Sets the root handler that will be invoked to actually execute requests. If a `HandlerBuilder` is passed, it will be built to get a `Handler` instance. |
| `Start()` | Creates an `Engine` instance, therefore listening for incoming requests. |
| `Stop()` | Stops an already started `Engine` instance. If not started, behaves like a NOP. |
| `Run()` | Creates an `Engine` instance and blocks execution until the process receives an exit signal. |
| `Bind(int, IP?, CertificateProvider?, CertificateValidator?, ...)` | Configures the engine to listen to the specified port. If an IP address is specified, the server should only listen to connections on this IP, otherwise to any IP. Call multiple times to listen to multiple endpoints. For details on this method see the binding details and security sections below. |
| `Development()` | Enables development mode on the server. |

## Binding Details

If not specified otherwise, the server listenes on port 8080 on any IP. As soon as `Bind()` is called, the server will no longer listen on port 8080 but only on the specified port. Multiple calls to `Bind()` will cause the server to listen on multiple endpoints.

An implementation may add additional parameters if relevant for an engine (e.g. whether QUIC should be supported). Those parameters must have sane defaults and must be allowed to be omitted. If parameters are not read by an engine specifying them must not throw an error.

## Security / TLS

The `Bind()` method must allow the user to configure a TLS secured endpoint. Therefore, the user must be allowed to pass a `CertificateProvider` and optionally a `CertficateValidator` interface implementation to configure mutual TLS (mTLS). As soon as the user passes a `CertificateProvider`, the endpoint is considered secure.

### CertificateProvider

| Member | Contract |
|---|---|
| `Provide(string?)` | Returns the certificate to be used for the specified host name, using a platform type for the certificate. Returning `null` will cause the engine to abort the TLS connection. |

### CertificateValidator

| Member | Contract |
|---|---|
| `RequireCertificate` | If this property returns `true`, the engine must fail the handshake if no client certificate has been passed. Otherwise the request will pass. |
| `Validate(...)` | Invoked by the engine with platform specific types to determine, whether the certificates presented by the client are accepted by the server. If this method returns `true`, the request will pass, otherwise fail. |

Not supplying a `CertificateValidator` allows the client to pass any certificate (or none). The binding may add useful properties where needed (e.g. to configure a revocation check), as long as the general idea of the contract is not violated. Passing a validator without a provider behaves as a NOP.

## Engine Interaction

The protocol between the `Engine` and the host is up to the binding implementation.
It is recommended that the host creates some kind of configuration structure that is then
passed to the engine.

// TBD: Where to place? Model?
