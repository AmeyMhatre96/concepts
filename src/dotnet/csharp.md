# C# Lang

### Explain the differences between value types and reference types in C#. Provide examples of each.

#### Value Types:

**Stored Value**: Value types store the actual data value itself directly in the memory location where the variable is allocated. The value is assigned to the variable directly.

**Stack vs. Heap**: Value type variables are typically stored on the stack, a small, fast, and fixed-size area of memory.

**Immutable**: Value types are usually immutable, meaning their values cannot be changed once they are assigned.

**Copy by Value**: When you pass a value type as an argument to a method or assign it to another variable, a copy of the value is made.

Examples of Value Types:

**Integral Types**: int, long, short, byte, char, uint, ulong, ushort, sbyte.

**Floating-Point Types**: float, double.

**Boolean Type**: bool.

**Enum Types**: Custom enumeration types.

**Structs**: Custom value types defined using the struct keyword.

### Reference Types:

**Stored Reference**: Reference types store a reference (memory address) to the actual data in memory, which is stored on the heap, a larger and more flexible area of memory.

**Mutable**: Reference types are mutable, and their data can be changed through the reference.

**Passing by Reference**: When you pass a reference type as an argument to a method or assign it to another variable, you are working with the same data in memory, not a copy.

>To be clear, you are passing a copy of the reference, but the reference itself points to the same data in memory. If you want to pass the same reference to a method, you must use the ref or out keywords.

Examples of Reference Types:

**Class Types**: Custom classes defined using the class keyword.

**Interface Types**: Custom interfaces.

**Delegate Types***: Custom delegate types.

**String Type**: The string type is a reference type, even though it behaves like a value type in many ways.


#### String Type:

The 'string' type in C# is indeed a reference type, but it behaves in ways that are similar to value types in some respects. This is due to various optimizations and language features implemented to make working with strings more efficient. Here are some of the ways in which 'string' behaves like a value type:

**Immutable**: Strings are immutable, meaning their values cannot be changed once they are assigned. When you assign a new value to a string variable, you are actually creating a new string object in memory and assigning it to the variable.
 
```csharp
string original = "Hello";
string modified = original + ", World"; // A new string object is created
```

**Value Equality**: Strings are compared for value equality, meaning that two string instances with the same content are considered equal, even if they are different objects in memory.

```csharp
string a = "Hello";
string b = "Hello";
bool areEqual = (a == b); // true, both strings have the same value
```

**String Interpolation**: String interpolation (e.g., $"Hello, {name}") allows you to create new strings by inserting values into a template string. The result is a new string object, just like with value types.

```csharp
string name = "Alice";
string greeting = $"Hello, {name}"; // A new string object is created
```
**Pass-by-Value Semantics**: When you pass a string as an argument to a method, you're effectively passing a copy of the reference, but you cannot modify the original string within the method because it's immutable.

```csharp
void ModifyString(string text)
{
    text = "Modified"; // Creates a new string, does not modify the original
}

string original = "Unmodified";
ModifyString(original);
Console.WriteLine(original); // Output: Unmodified
```

**String Interning**: C# uses a concept called string interning, where it reuses existing string objects with the same value to save memory and improve performance. This can make string comparisons faster and more memory-efficient.

**Operators Overloading**: You can use operators like + for string concatenation, and == for string comparison, which makes working with strings feel similar to value types.

```csharp
string hello = "Hello";
string world = "World";
string greeting = hello + ", " + world;
bool areEqual = (hello == world);
```

#### ref vs out 

**`ref` Parameter:**
- Requires variable initialization.
- Supports two-way communication.
- Used for both input and output.

**`out` Parameter:**
- Doesn't require variable initialization.
- Supports one-way communication.
- Primarily used for output values.

Example:

```csharp
// Using ref
void ModifyWithRef(ref int x) { /* ... */ }

int value1 = 5;
ModifyWithRef(ref value1);

// Using out
void GetOutput(out int x, out int y) { /* ... */ }

int value2;
int value3;
GetOutput(out value2, out value3);
```

In summary, `ref` is for two-way communication, `out` is for one-way output, and `out` doesn't require variable initialization.

### Deligates, Events, and Lambdas

#### Delegates

A delegate is a type that represents references to methods with a particular parameter list and return type. When you instantiate a delegate, you can associate its instance with any method with a compatible signature and return type. You can invoke (or call) the method through the delegate instance.

Delegates are used to pass methods as arguments to other methods. Event handlers are nothing more than methods that are invoked through delegates. You create a custom method, and a class such as a windows control can call your method when a certain event occurs. The following example shows a delegate declaration:

```csharp
public delegate void Print(int value);

public static void PrintNumber(int num)
{
    Console.WriteLine("Number: {0,-12:N0}", num);
}

public static void Main(string[] args)
{
    Print printDel = PrintNumber;
    printDel(100000);
    printDel(200);

    printDel = PrintMoney;
    printDel(10000);
    printDel(200);
}
```

#### Events

An event is a notification sent by an object to signal the occurrence of an action. The object that raises the event is called the event sender. The event sender doesn’t know which object or method will receive (handle) the events it raises. The event is typically a member of the event sender.

The event receiver is called the event handler. An event handler is a method that is executed when an event is raised. The event handler is the method that responds to the event. The event handler must be registered with the event sender, and this registration enables the event sender to call the event handler when the event occurs.

An event is a higher-level abstraction built on top of delegates.

The following example shows how to declare an event and raise it:

```csharp
using System;

public class Publisher
{
    public event Action SomethingHappened; // Event declaration

    public void DoSomething()
    {
        Console.WriteLine("Doing something...");
        OnSomethingHappened(); // Raise the event
    }

    protected virtual void OnSomethingHappened()
    {
        SomethingHappened?.Invoke(); // Raise the event
    }
}

public class Subscriber
{
    public void Subscribe(Publisher publisher)
    {
        publisher.SomethingHappened += HandleSomethingHappened;
    }

    public void Unsubscribe(Publisher publisher)
    {
        publisher.SomethingHappened -= HandleSomethingHappened;
    }

    private void HandleSomethingHappened()
    {
        Console.WriteLine("Something happened!");
    }
}

public class Program
{
    public static void Main()
    {
        Publisher publisher = new Publisher();
        Subscriber subscriber = new Subscriber();

        subscriber.Subscribe(publisher);

        publisher.DoSomething();

        subscriber.Unsubscribe(publisher);

        publisher.DoSomething();
    }
}
```

#### Lambdas

a lambda is a method without a permanent name.

Lambdas are very much like other methods, except for a couple subtle differences.

A normal method is defined in a "statement" and tied to a permanent name, whereas a lambda is defined "on the fly" in an "expression" and has no permanent name.
Some lambdas can be used with .NET expression trees, whereas methods cannot.
A delegate is defined like this:
```csharp
delegate Int32 BinaryIntOp(Int32 x, Int32 y);
```
A variable of type BinaryIntOp can have either a method or a labmda assigned to it, as long as the signature is the same: two Int32 arguments, and an Int32 return.

A lambda might be defined like this:
```csharp
BinaryIntOp sumOfSquares = (a, b) => a*a + b*b;
```