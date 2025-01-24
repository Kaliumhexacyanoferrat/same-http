# Modules

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
| [Layouting](./Layouting.md) | Structures an application and provides routing. |
