
# Protocols

A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to conform to that protocol.
## Protocol Syntax

```swift
protocol SomeProtocol {
    // protocol definition goes here
}
```

Classes, structs, enums can adopt these protocols by placing protocol’s name after the type’s name, separated by a colon, as part of their definition. Multiple protocols can be listed, and are separated by commas:

```swift
struct SomeStructure: FirstProtocol, AnotherProtocol {
    // structure definition goes here
}
```

If a class has a superclass, list the superclass name before any protocols it adopts, followed by a comma:

```swift
class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
    // class definition goes here
}
```

A good practice is to use extensions dedicated to each protocol implementation.

```swift
class ViewController: UIViewController {}
extension ViewController: UITableViewDataSource, UITableViewDelegate
{
     // implement protocol methods and variables here
}
```
