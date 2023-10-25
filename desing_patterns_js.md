# Design Patterns in Javascript

## OOP and S.O.L.I.D. principles
Object-Oriented Programming is a programming style based on classes and objects. These group data (properties) and methods (actions) inside a box. 

    JavaScript is prototype-based procedural language, which means it supports both functional and object-oriented programming.

Classes were introduced to _Javascript_ with ECMAScript 2015 and they're just a syntantic sugar to **Prototypal Inheritance**. We then have an object linked to a prototype. Prototypes contain all methods and these methods are accessible to all objects linked to this prototype.

You can declare a class using the class keyword. Here's a class declaration for our Person from the previous article:
```js
class Person {
  name;

  constructor(name) {
    this.name = name;
  }

  introduceSelf() {
    console.log(`Hi! I'm ${this.name}`);
  }
}

```
The SOLID Principles are five principles of Object-Oriented class design. They are a set of rules and best practices to follow while designing a class structure. Following the SOLID acronym, they are:
- The Single Responsibility Principle:

The Single Responsibility Principle states that a class should do one thing and therefore it should have only a single reason to change. 

1. The Open-Closed Principle

The Open-Closed Principle requires that classes should be open for extension and closed to modification. Modification means changing the code of an existing class, and extension means adding new functionality.

2. The Liskov Substitution Principle

The Liskov Substitution Principle states that subclasses should be substitutable for their base classes. This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case. 

3. The Interface Segregation Principle

Segregation means keeping things separated, and the Interface Segregation Principle is about separating the interfaces. The principle states that many client-specific interfaces are better than one general-purpose interface. Clients should not be forced to implement a function they do no need. 

4. The Dependency Inversion Principle

The Dependency Inversion principle states that our classes should depend upon interfaces or abstract classes instead of concrete classes and functions. 


## ¿What are design patterns?
Design patterns are typical solutions to common problems in software design. Each pattern is like a blueprint that you can customize to solve a particular design problem in your code. You can’t just find a pattern and copy it into your program, the way you can with off-the-shelf functions or libraries. The pattern is not a specific piece of code, but a general concept for solving a particular problem. You can follow the pattern details and implement a solution that suits the realities of your own program.

