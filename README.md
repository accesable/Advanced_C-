# Advance C# Concepts

### LINQ
> Write Query (fimiliar to SQL) against strongly typed Collection Of objects




---
### Extension Method
> Adding methods to exsiting types without creating new derived type and modifying the original sources code. They are static methods, but they're called as if they were instance methods on the extended type
#### Defining an Extension Method
1. **Create a static class**: Extension methods must be defined in a static class.
2. **Define a static method**: The method should be static and the first parameter should specify the type the method operates on. This parameter is preceded by the `this` keyword.
```csharp
public static class StringExtensions
{
    public static int WordCount(this string str)
    {
        return str.Split(new char[] { ' ', '.', '?' }, StringSplitOptions.RemoveEmptyEntries).Length;
    }
}

```
In this example, WordCount is an extension method defined for string type.
#### Using an Extension Method
- **Add a using directive**: To use the extension method, you must include a using directive for the namespace that contains the static class.
- **Call like an instance method**: Once the directive is in place, you can call the extension method as if it were an instance method on the type.
```csharp
using MyExtensions; // Assuming the StringExtensions class is in this namespace

string text = "Hello, world!";
int count = text.WordCount(); // Call the extension method
```
##### Notes:
- **Namespace**: The namespace where the static class is defined must be included in your file to access the extension method.
- **Visibility**: Extension methods are subject to the usual C# visibility and accessibility rules.
- **Overriding**: An extension method will never be called if it has the same signature as a method defined in the type.

Extension methods offer a way to add functionality to a class without altering its source code, and can be especially useful when working with types that you cannot modify, such as those in the .NET Framework or third-party libraries.





---
### Delegates in C#
Delegates in C# are a type-safe way of representing references to methods. They are used to pass methods as arguments, define callback methods, and implement event handling.

#### Definition
A delegate is a reference type that defines a method signature. When you instantiate a delegate, you can associate its instance with any method that has a compatible signature.

#### Basic Syntax
Here's how you can declare and use a delegate:
```csharp
// Define a delegate
public delegate int Operation(int x, int y);

// Method that matches the delegate signature
public int Add(int a, int b)
{
    return a + b;
}

// Using the delegate
Operation op = new Operation(Add);
int result = op(5, 10); // Invoke the delegate

```
#### Multicast Delegates
Delegates in C# are multicast, which means they can hold references to more than one function. For example:
```csharp
public void ShowMessage(string message)
{
    Console.WriteLine(message);
}

Action<string> messageDelegate = ShowMessage;
messageDelegate += Console.WriteLine; // Add another method

messageDelegate("Hello, World!"); // This will call both methods

```
#### Delegate as Parameters
Delegates can be passed as parameters to methods, enabling callback functionality:
```csharp
public void PerformOperation(Operation operation)
{
    int result = operation(5, 5);
    Console.WriteLine($"Result: {result}");
}
```
#### Built-in Delegates
.NET provides several built-in delegates like `Func<>`, `Action<>`, and `Predicate<>`, which are generic and can be used instead of defining custom delegates in many cases.
```csharp
Func<int, int, int> add = (x, y) => x + y;
int sum = add(5, 10);

Action<string> display = Console.WriteLine;
display("Hello, World!");

Predicate<int> isPositive = x => x > 0;
bool result = isPositive(-5);
```
#### Event Handling
Delegates are fundamental in event handling in C#. Events in a class are typically declared as a delegate type.
```csharp
public delegate void EventHandler(string message);

public event EventHandler OnEvent;

public void TriggerEvent()
{
    if (OnEvent != null)
    {
        OnEvent("Event triggered");
    }
}
```
#### Conclusion
Delegates are a powerful feature in C# that allows for dynamic method invocation, callback mechanisms, and event handling. They are essential for understanding advanced C# programming concepts, especially in event-driven programming models.