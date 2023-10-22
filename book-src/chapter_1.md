# Object oriented

OOPS is a programming technique that employees objects to develop programs. It is a way of modularizing programs by creating partitioned memory area for both data and functions that can be used as templates for creating copies of such modules on demand.

## Components of OOP
### 1. Class
Class is a blueprint of an object. It is a template or a set of instruction to build a specific type of object.


### 2. Object
Object is an instance of a class. When a class is defined, no memory is allocated but when it is instantiated (i.e. an object is created) memory is allocated.

### 3. Interface
Interface is a collection of abstract methods. A class implements an interface, thereby inheriting the abstract methods of the interface.

## Properties of OOP
### 1. Encapsulation
Encapsulation is a way to restrict the direct access to some components of an object, so users cannot access state values for all of the variables of a particular object. Encapsulation can be used to hide both data members and data functions or methods associated with an instantiated class or object.
Key Points:
It enforces information hiding and protects the integrity of an object's data.
It restricts direct access to object properties, promoting controlled interaction.
It helps maintain the object's internal consistency by enforcing validation and rules through methods.
meaningful example in C#:
```csharp
public class BankAccount
{
    private decimal maxDeposit = 1000000;

    private decimal balance = 0;

    public void Deposit(decimal amount)
    {
        if (amount > maxDeposit)
        {
            throw new Exception("Deposit amount exceeds maximum deposit allowed");
        }
        balance += amount;
    }

    public void Withdraw(decimal amount)
    {
        if (balance >= amount)
        {
            balance -= amount;
        }
    }

    public decimal GetBalance()
    {
        return balance;
    }
}

```
### 2. Abstraction
Abstraction occurs when a programmer hides any irrelevant data about an object or an instantiated class to reduce complexity and help users interact with a program more efficiently.
> "Abstraction and encapsulation are complementary concepts: abstraction focuses on the observable behavior of an object...encapsulation focuses on the implementation that gives rise to this behavior"

### 3. Inheritance
Inheritance is a mechanism that allows one class to gain the properties of another class, in the same way, that a child inherits some attributes from each of their parents. Inheritance allows programmers to create a new class that reuses the data members and methods of an existing class.

#### Use Abstract Classes When:

You want to provide a common base class with some shared functionality for subclasses.
There is a need for code reuse among related classes.
You have some methods with a default implementation that can be inherited by subclasses.

#### Use Interfaces When:

You want to define a contract that multiple unrelated classes must adhere to.
You need to ensure a consistent API across different classes.
You want to allow classes to implement multiple contracts (interfaces).

example of abstract class:
```csharp
using System;

abstract class Shape
{
    public string Name { get; private set; }

    public Shape(string name)
    {
        Name = name;
    }

    public abstract double Area();
    public abstract double Perimeter();

    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}");
        Console.WriteLine($"Area: {Area()}");
        Console.WriteLine($"Perimeter: {Perimeter()}");
    }
}

class Rectangle : Shape
{
    public double Width { get; }
    public double Height { get; }

    public Rectangle(string name, double width, double height)
        : base(name)
    {
        Width = width;
        Height = height;
    }

    public override double Area()
    {
        return Width * Height;
    }

    public override double Perimeter()
    {
        return 2 * (Width + Height);
    }
}

class Circle : Shape
{
    public double Radius { get; }

    public Circle(string name, double radius)
        : base(name)
    {
        Radius = radius;
    }

    public override double Area()
    {
        return Math.PI * Radius * Radius;
    }

    public override double Perimeter()
    {
        return 2 * Math.PI * Radius;
    }
}

class Program
{
    static void Main()
    {
        Rectangle rectangle = new Rectangle("Rectangle", 4, 5);
        Circle circle = new Circle("Circle", 3);

        rectangle.DisplayInfo();
        Console.WriteLine();
        circle.DisplayInfo();
    }
}
```


### 4. Polymorphism
it has two distinct aspects:

At run time, objects of a derived class may be treated as objects of a base class in places such as method parameters and collections or arrays. When this polymorphism occurs, the object's declared type is no longer identical to its run-time type.
Base classes may define and implement virtual methods, and derived classes can override them, which means they provide their own definition and implementation. At run-time, when client code calls the method, the CLR looks up the run-time type of the object, and invokes that override of the virtual method. In your source code you can call a method on a base class, and cause a derived class's version of the method to be executed.

``` csharp
using System;

class Animal
{
    public string Name { get; set; }

    public Animal(string name)
    {
        Name = name;
    }

    public virtual void MakeSound()
    {
        Console.WriteLine("The animal makes a sound.");
    }
}

class Dog : Animal
{
    public Dog(string name) : base(name) { }

    public override void MakeSound()
    {
        Console.WriteLine($"{Name} barks: Woof woof!");
    }
}

class Cat : Animal
{
    public Cat(string name) : base(name) { }

    public override void MakeSound()
    {
        Console.WriteLine($"{Name} meows: Meow meow!");
    }
}

class Program
{
    static void Main()
    {
        Animal[] animals = new Animal[]
        {
            new Dog("Buddy"),
            new Cat("Whiskers"),
            new Dog("Rex"),
            new Cat("Mittens")
        };

        foreach (Animal animal in animals)
        {
            Console.WriteLine($"{animal.Name} says:");
            animal.MakeSound();
            Console.WriteLine();
        }
    }
}

```