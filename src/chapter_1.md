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
## Solid principles
### 1. Single Responsibility Principle
A class should have one responsibility. 
When a class has only one responsibility, it becomes easier to change that class without impacting other parts of the code. 

Example that violates SRP:

``` csharp
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Designation { get; set; }
    public decimal Salary { get; set; }

    public void Save(){
        //Save employee to database
    }
}
```
Better approach:
``` csharp
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Designation { get; set; }
    public decimal Salary { get; set; }
}

public class EmployeeRepository
{
    public void Save(Employee employee){
        //Save employee to database
    }
}

```

### 2. Open Closed Principle
Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.
In other words, you should be able to extend a class’s behavior, without modifying it. 
When we violate this principle, complete class needs to be retested.

Example that violates OCP:
``` csharp
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Designation { get; set; }
    public decimal Salary { get; set; }

    public decimal CalculateBonus(string employeeType){
        if(employeeType == "parmanent"){
            return Salary * .1M;
        }
        else{
            return Salary * .05M;
        }
    }
}
```
Better approach:
``` csharp
public abstract class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Designation { get; set; }
    public decimal Salary { get; set; }

    public abstract decimal CalculateBonus();
}

public class PermanentEmployee : Employee
{
    public override decimal CalculateBonus()
    {
        return Salary * .1M;
    }
}
```

### 3. Liskov Substitution Principle
Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.

Example that violates LSP:
``` csharp
class Rectangle
{
    public virtual int Width { get; set; }
    public virtual int Height { get; set; }
}

class Square : Rectangle
{
    public override int Width
    {
        get => base.Width;
        set
        {
            base.Width = value;
            base.Height = value;
        }
    }

    public override int Height
    {
        get => base.Height;
        set
        {
            base.Width = value;
            base.Height = value;
        }
    }
}

``` 

### 4. Interface Segregation Principle
Clients should not be forced to depend upon interfaces that they do not use.
Its better to have many smaller interfaces than one larger interface.

Example that violates ISP:
``` csharp
public interface IVehicle
{
    void Drive();
    void Fly();
}

public class Car : IVehicle
{
    public void Drive()
    {
        //actions to drive a car
    }

    public void Fly()
    {
        throw new NotImplementedException();
    }
}

public class Airplane : IVehicle
{
    public void Drive()
    {
        throw new NotImplementedException();
    }

    public void Fly()
    {
        //actions to fly an airplane
    }
}
```

Better approach:
``` csharp
public interface IDrive
{
    void Drive();
}

public interface IFly
{
    void Fly();
}

public class Car : IDrive
{
    public void Drive()
    {
        //actions to drive a car
    }
}

public class FlyingCar : IFly, IDrive
{
    public void Drive()
    {
        //actions to drive a car
    }

    public void Fly()
    {
        //actions to fly a car
    }
}
```

### 5. Dependency Inversion Principle
High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. 

Example:
``` csharp
public interface INotifier
{
    void Notify(string message);
}

public class EmailNotifier : INotifier
{
    public void Notify(string message) { /* Send email */ }
}

public class SMSNotifier : INotifier
{
    public void Notify(string message) { /* Send SMS */ }
}

public class WeatherApp
{
    private INotifier notifier;

    public WeatherApp(INotifier notifier)
    {
        this.notifier = notifier;
    }

    public void CheckWeather()
    {
        // ... Weather checking logic ...
        notifier.Notify("Weather alert: ...");
    }
}

```