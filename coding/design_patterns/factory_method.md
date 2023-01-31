# Factory method

- [Wikipedia](https://en.wikipedia.org/wiki/Factory_method_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)

- Type: Creational pattern
- Also known as: Virtual Constructor

In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

The Factory Method design pattern solves problems like:

- How can an object be created so that subclasses can redefine which class to instantiate?
- How can a class defer instantiation to subclasses?

The Factory Method design pattern describes how to solve such problems:

- Define a separate operation (factory method) for creating an object.
- Create an object by calling a factory method.

## Applicability:

- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method#applicability)

Use the Factory Method when you:

- don’t know beforehand the exact types and dependencies of the objects your code should work with.
- want to provide users of your library or framework with a way to extend its internal components.
- want to save system resources by reusing existing objects instead of rebuilding them each time.
