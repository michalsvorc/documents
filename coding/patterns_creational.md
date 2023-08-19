# Creational patterns

Resources:

- [Wikipedia](https://en.wikipedia.org/wiki/Creational_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/creational-patterns)

Content:

- [Factory method](#factory-method)
- [Builder](#builder)
- [Prototype](#prototype)
- [Singleton](#singleton)

---

## Factory method

- [Wikipedia](https://en.wikipedia.org/wiki/Factory_method_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)

Also known as: Virtual Constructor

In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

### Problems

- How can an object be created so that subclasses can redefine which class to instantiate?
- How can a class defer instantiation to subclasses?

### Implementation

- Define a separate operation (factory method) for creating an object.
- Create an object by calling a factory method.

### Applicability

- don’t know beforehand the exact types and dependencies of the objects your code should work with.
- want to provide users of your library or framework with a way to extend its internal components.
- want to save system resources by reusing existing objects instead of rebuilding them each time.

---

## Builder

- [Wikipedia](https://en.wikipedia.org/wiki/Builder_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/builder)

The intent of the Builder design pattern is to separate the construction of a complex object from its representation. The pattern allows you to produce different types and representations of an object using the same construction code. The Builder pattern lets you build objects step by step, using only those steps that you really need.

The Builder pattern suggests that you extract the object construction code out of its own class and move it to separate objects called builders.

The director class defines the order in which to execute the building steps, while the builder provides the implementation for those steps. Having a director class in your program isn’t strictly necessary.

### Problems

- How can a class (the same construction process) create different representations of a complex object?
- How can a class that includes creating a complex object be simplified?
- Eliminates need for considerable number of subclasses or giant constructor in the base class with all possible parameters.

### Applicability

The Builder pattern can be applied when construction of various representations of the product involves similar steps that differ only in the details.

---

## Prototype

- [Wikipedia](https://en.wikipedia.org/wiki/Prototype_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/prototype)

Prototype is a creational design pattern that lets you copy existing objects without making your code dependent on their classes. It is used when the type of objects to create is determined by a prototypical instance, which is cloned to produce new objects.

The Prototype pattern delegates the cloning process to the actual objects that are being cloned, you don't have to know the object’s class to create a duplicate.

The Prototype pattern lets you use a set of pre-built objects configured in various ways as prototypes. Instead of instantiating a subclass that matches some configuration, the client can simply look for an appropriate prototype and clone it.

### Problems

- How can objects be created so that which objects to create can be specified at run-time?
- How can dynamically loaded classes be instantiated?

### Implementation

- Define a Prototype object that returns a copy of itself.
- Create new objects by copying a Prototype object.

### Applicability

- Use the Prototype pattern when your code shouldn’t depend on the concrete classes of objects that you need to copy.

---

## Singleton

- [Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/singleton)

Singleton pattern allows objects to:

- Ensure they only have one instance
- Provide easy access to that instance
- Control their instantiation (for example, hiding the constructors of a class)

The most common reason for this is to control access to some shared resource—for example, a database or logging service.

Singletons are often preferred to global variables because they do not pollute the global namespace.

### Implementation

- Make the default constructor private, to prevent other objects from using the new operator with the Singleton class.
- Create a static creation method that acts as a constructor. Under the hood, this method calls the private constructor 
  to create an object and saves it in a static field. All following calls to this method return the cached object.

### Note

The pattern requires special treatment in a multithreaded environment so that multiple threads won’t create a singleton object several times.
