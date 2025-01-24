# Concern

While `Handler` instances generate content, `Concern` instances
add behavior to an application. Nevertheless they are handlers themselves.

## Example

```csharp
class AddHeaderConcern implements Concern
{

	public Handler Content { get; }

	AddHeaderConcern(Handler content) 
	{
		Content = content;
	}

	void Prepare() { Content.Prepare(); }

	Response? Handle(Request request) 
	{
		var response = Content.Handle(request);

		if (response != null)
		{
			response.Headers.Add("X-Custom-Header", "Custom Value");
		}

		return response;
	}

}
```

## Definition

As concerns are handlers, they provide the same members, in addition to a
`Content` property that exposes the inner handler.

## Concern Builders

As with handlers, concerns must always be built using a class implementing
the `ConcernBuilder` interface.

## Definition

| Member | Implementation |
|---|---|
| `Build(Handler)` | Creates the concern instance, using the given `Handler` as inner content.  |
