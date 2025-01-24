# Target

The target specifies the resource requested by the client and allows modules
to perform routing. The target is initialized by the engine with a `WebPath` that consists
of `WebPathParts` (the segments of the requested URI, separated by slashes).

## Web Path

Stores information about a requested resource without routing information.

| Member | Implementation |
|---|---|
| `Parts` | The parts the web path consists of. |
| `TrailingSlash` | Whether the client passed a trailing slash when requesting the resource. |

## Web Path Part

A single segment in a requested resource path.

| Member | Implementation |
|---|---|
| `Original` | The original segment value as read from the client (might be URL encoded). |
| `Value` | The non-encoded value of the segment. |

## Routing Target

Stores the current routing state that can get manipulated by the module implementations.

| Member | Implementation |
|---|---|
| `Path` | The requested `WebPath`. |
| `Current` | The currently processed `WebPathPart`, if any is left or available. |
| `Last` | `true`, if the current segment is the last one to be processed. |
| `Advance()` | Moves to the next `WebPathPart` or throws an exception if already at the end. |
| `Remaining` | Returns a `WebPath` representing the path that is still to be routed (not including `Current`). |