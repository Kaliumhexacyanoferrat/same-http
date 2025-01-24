# Host

The host provides an engine independent way of configuring and starting a server instance
that will listen to incoming HTTP requests.

## Builder

`Host` instances must be created using a builder. The following snippet
illustrates how a `Host` instance could be built and started:

```csharp
var host = Host.Create()
               .UseKestrel() // select engine
               .Content(handler)
               .Port(9000);

host.Start();

host.Stop();
```

## Configuration Model