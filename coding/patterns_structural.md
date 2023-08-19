# Structural patterns

Resources:

- [Wikipedia](https://en.wikipedia.org/wiki/Structural_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/structural-patterns)

Content:

- [Adapter](#adapter)
- [Bridge](#bridge)
- [Composite](#composite)
- [Decorator](#decorator)

---

## Adapter

- [Wikipedia](https://en.wikipedia.org/wiki/Factory_method_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)

An adapter allows two incompatible interfaces to work together. This is the real-world definition for an adapter. 

Interfaces may be incompatible, but the inner functionality should suit the need. The adapter design pattern allows 
otherwise incompatible classes to work together by converting the interface of one class into an interface expected by the clients. 

Also known as wrapper, an alternative naming shared with the decorator pattern. An adapter wraps one of the objects
to hide the complexity of conversion happening behind the scenes. 

### Problems

- How can a class be reused that does not have an interface that a client requires?
- How can classes that have incompatible interfaces work together?
- How can an alternative interface be provided for a class?

### Implementation

- Define a separate adapter class that converts the (incompatible) interface of a class (adaptee) into another interface (target) clients require.
- Work through an adapter to work with (reuse) classes that do not have the required interface.

### Applicability

- Use the Adapter class when you want to use some existing class, but its interface isn’t compatible with the rest of your code.
- Use the pattern when you want to reuse several existing subclasses that lack some common functionality that can’t be added to the superclass.

---

## Bridge

- [Wikipedia](https://en.wikipedia.org/wiki/Bridge_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/bridge)

The bridge pattern is meant to "decouple an abstraction from its implementation so that the two can vary independently". The bridge uses encapsulation, aggregation, and can use inheritance to separate responsibilities into different classes, which can be developed independently of each other.

Abstraction (also called interface) is a high-level control layer for some entity. This layer isn’t supposed to do any real work on its own. It should delegate the work to the implementation layer (also called platform).

Note that we’re not talking about interfaces or abstract classes from your programming language.

### Problems

- An abstraction and its implementation should be defined and extended independently from each other.
- A compile-time binding between an abstraction and its implementation should be avoided so that an implementation can be selected at run-time.
    
### Implementation

- Separate an abstraction (Abstraction) from its implementation (Implementor) by putting them in separate class hierarchies.
- Implement the Abstraction in terms of (by delegating to) an Implementor object.

### Applicability

- Use the Bridge pattern when you want to divide and organize a monolithic class that has several variants of some functionality (for example, if the class can work with various database servers).
- Use the pattern when you need to extend a class in several orthogonal (independent) dimensions.
- Use the Bridge if you need to be able to switch implementations at runtime.

---

## Composite

- [Wikipedia](https://en.wikipedia.org/wiki/Composite_pattern)
- [Refactoring Guru](https://refactoring.guru/design-patterns/composite)

Composite is a structural design pattern that lets you compose objects into tree structures and then work with these structures as if they were individual objects.

Using the Composite pattern makes sense only when the core model of your app can be represented as a tree.

### Problems

- A part-whole hierarchy should be represented so that clients can treat part and whole objects uniformly.
- A part-whole hierarchy should be represented as tree structure.
    
### Implementation

- Define a unified Component interface for both part (Leaf) objects and whole (Composite) objects.
- Individual Leaf objects implement the Component interface directly, and Composite objects forward requests to their child components.
    
### Applicability

- Use the Composite pattern when you have to implement a tree-like object structure.
- Use the pattern when you want the client code to treat both simple and complex elements uniformly.

---

## Decorator

Also known as: Wrapper 

The decorator pattern is a design pattern that allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class.

The decorator pattern is often useful for adhering to the *Single Responsibility Principle*, as it allows functionality to be divided between classes with unique areas of concern as well as to the *Open-Closed Principle*, by allowing the functionality of a class to be extended without being modified.

### Problems

- Responsibilities should be added to (and removed from) an object dynamically at run-time.
- A flexible alternative to subclassing for extending functionality should be provided.

Inheritance has following problems:

- Inheritance is static. You can’t alter the behavior of an existing object at runtime. You can only replace the whole object with another one that’s created from a different subclass.
- Subclasses can have just one parent class. In most languages, inheritance doesn’t let a class inherit behaviors of multiple classes at the same time.

### Implementation

Define Decorator objects that

- implement the interface of the extended (decorated) object (Component) transparently by forwarding all requests to it
- perform additional functionality before/after forwarding a request.

This allows working with different Decorator objects to extend the functionality of an object dynamically at run-time.

### Applicability

- Use the Decorator pattern when you need to be able to assign extra behaviors to objects at runtime without breaking the code that uses these objects.
- Use the pattern when it’s awkward or not possible to extend an object’s behavior using inheritance.
