# Handler

As a core concept of the framework, `Handler` instances 
implement the functionality of the modules by inspecting a `Request`
and generating a `Response` to be returned to the client.

The `Host` expects a single handler to be passed on root level,
which may use other handlers internally to eventually build
the structure of the web application.

## Example

```csharp
class HelloHandler implements Handler 
{

	void Prepare() { }

	Response? Handle(Request request) 
	{
		var response = request.Respond();

		response.Content = new StringContent("Hello World");
		
		return response;
	}

}
```

## Definition

| Member | Implementation |
|---|---|
| `Prepare()` | Called by the engine during start-up to perform expensive initialization tasks.  |
| `Handle(Request)` | Inspects the request and generates a response. May return `null` to indicate a `404 Not Found`. |

## Handler Builders

As a choice of design, every handler must be created using a `HandlerBuilder`
class. This builder is mainly intended to provide a certain style when
creating projects using the framework and automatically allows concerns to be added anywhere
through the application.

| Member | Implementation |
|---|---|
| `Add(ConcernBuilder)` | Adds a `Concern` that will be executed before the handler is actually executed.   |
| `Build()` | Creates the actual `Handler` instance. |

As builders are lazy, the handler tree will be generated directly before
passing it to the `Host` instance. 

Adding multiple concerns to a `HandlerBuilder` causes them to be chained from inner to outer, which means
that the concern added the last will be executed the first when requests are handled. Bindings will probably
have a single utility class to implement this chaining.