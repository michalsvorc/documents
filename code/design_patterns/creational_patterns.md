# Creational patterns

## Factory method

---

- [Wikipedia](https://en.wikipedia.org/wiki/Factory_method_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)

Also known as: Virtual Constructor

In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

### Problem

- How can an object be created so that subclasses can redefine which class to instantiate?
- How can a class defer instantiation to subclasses?

### Solution

- Define a separate operation (factory method) for creating an object.
- Create an object by calling a factory method.

### Applicability

- don’t know beforehand the exact types and dependencies of the objects your code should work with.
- want to provide users of your library or framework with a way to extend its internal components.
- want to save system resources by reusing existing objects instead of rebuilding them each time.

## Builder

---

- [Wikipedia](https://en.wikipedia.org/wiki/Builder_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/builder)

The intent of the Builder design pattern is to separate the construction of a complex object from its representation. The pattern allows you to produce different types and representations of an object using the same construction code. The Builder pattern lets you build objects step by step, using only those steps that you really need.

### Problem

- How can a class (the same construction process) create different representations of a complex object?
- How can a class that includes creating a complex object be simplified?
- Eliminates need for considerable number of subclasses or giant constructor in the base class with all possible parameters.

### Solution

The Builder pattern suggests that you extract the object construction code out of its own class and move it to separate objects called builders.

The director class defines the order in which to execute the building steps, while the builder provides the implementation for those steps. Having a director class in your program isn’t strictly necessary.

### Applicability

The Builder pattern can be applied when construction of various representations of the product involves similar steps that differ only in the details.


