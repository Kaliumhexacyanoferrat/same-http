# Same HTTP

Same HTTP is a language independent HTTP API service specification with bindings for various programming languages. This allows

- Developers to re-use their knowledge as they try out new languages or shift languages on their work projects
- Programming languages to quickly provide a well-tested HTTP service stack
- Middleware developers to make their solutions widely available

## Bindings

| Language | Link | Status |
|---|---|---|
| Kotlin | same-http-kotlin | In Progress |

## Specification

The [specification](./Specification/Index.md) declares key elements such as `Engine`, `Host`, `Adapter` or `Handler` and defines how an integration should "feel like". It also specifies a set of modules a binding should provide in order to allow developers to switch between lanuages without losing functionality.
