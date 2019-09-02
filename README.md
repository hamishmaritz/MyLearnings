# MyLearnings
My Own Personal Learnings

🚀 Introduction
=================
* [OOP](#creational-design-patterns)
* [Algorithms](#creational-design-patterns)
* [RestJS/Javascript](#creational-design-patterns)
* [Dependency Injection](#creational-design-patterns)
* [C#/.NET Frameworks](#creational-design-patterns)
* [.NET MVC](#creational-design-patterns)
* [REST/API Programming](#creational-design-patterns)
* [Azure](#creational-design-patterns)
* [Test Driven Development](#creational-design-patterns)
* [SOLID](#structural-design-patterns)
* [Design Patterns](#Introduction-To-Design-Patterns)



OOP
=================

Basics of OOP (Catered to Air NZ)
-----------------

What is an Object?
-----------------
An object is a self-contained, useable instance of a class
A class is an entity that can be made up of data variables and/ or functions
To create a new instance (object) of that class is called instantiation

To put into simple terms:
* A class is a blueprint
* An object is a building made from that blueprint
* There can be multiple buildings from the same blueprint
* Classes themselves are NOT objects but are used to instantiate objects.
* Some properties and methods of a class:

```csharp
public class MyClass
{
    public string myStringField = string.Empty;

    public void MyMethod(int parameter1, string parameter2)
    {
        Console.WriteLine($"Something about {parameter1} and {parameter2}");
    }

    public int AutoImplementedProperty {get;set;}

    private int myProperty;

    public int MyProperty
    {
        get{return myProperty;}
        set{myProperty = value;}
    }
}
```

What is an Interface?
-----------------
An Interface can have methods, properties, events and indexes as it's members.
However, it will contain ONLY the declaration of these members. The implementation will be given by the Class that implements the interface.
This is used to achieve:
```csharp 
public interface IVehicle
{
    public string Make {get;set;}
    public string Model {get;set;}
    public int Wheels {get;set;}
    public void Drive();
    /// ...etc
}

public class Car : IVehicle
{}

public class Truck : IVehicle
{
    public void Load();
}

static void Main(string[] args)
{
    Truck garbageTruck = new Truck()
    {
        // fill in data for Make, Model, Wheels, call methods Drive and Load
    };

    Car hatchback = new Car()
    {
        // fill in data for Make, Model, Wheels, call methods Drive
    };
} 
```

Encapsulation
-----------------
Is combining related methods, properties and other members to be treated as a single group.

```csharp
public class TaxIncomeCalculations
{
    public decimal GetGrossIncome(decimal salary)
    {
        return GetRoundedCalculationAsInteger(salary / 12);
    }

    public decimal GetNetIncome(decimal grossIncome, decimal incomeTax)
    {
        var netIncome = grossIncome - incomeTax;

        return GetRoundedCalculationAsInteger(netIncome);
    }

    public decimal GetSuperAmount(decimal grossIncome, decimal payRate)
    {
        var superAmount = grossIncome * payRate / 100;

        return GetRoundedCalculationAsInteger(superAmount);
    }
}
```
Encapsulation also is a way to create Information Hiding through the privatisation of the states of some of the classes members.

This ensures that other objects cannot affect the state of that data. Only by calling the public methods/functions of that object can they have access. The object thus manages it's own state.


Abstraction
-----------------
Can be seen as an extension of Encapsulation.
Where Encapsulation defines the desired level of abstraction, abstraction allows only making the releveant information visable.

An example of Abstraction would be:

A User knows that in order to GetCoffee() they need to put in the coffee and enter a button on the machine, however all the needed methods and background work is hidden to them, as they don't need to know all the complex implementations in order for them to GetCoffee().

Another example:

A simple search function to a database.
A User enters the information they wish to find from the database. Say it is searching for the product invoices for a particular company.
That could call for Search() using the name of that particular company.
Internally, that search would then execute a series of steps to call the database, or server, in order to search perhaps using multiple calls to different methods in order to Get that list of invoice information and send it back to the user, perhaps changing it in some way in order to make it more readable for the user.
All of this implementation goes on behind the scenes for the user. For them, they only had to know to enter the name of the company and press Search().

This is Abstraction.
It is the hiding, not of the Information at the class level like with Encapsulation, but of the complexity; abstracting the low levels of implementation from the user.
This is particularly helpful when using larger code bases.
The way things are done behind the scenes, should rarely change the way the user uses them.

Another example of this is a phone:

The average person does not understand the complexity of a phones lower-level implementation functions, however they will understand the abstracted high-level functions that are needed to use said phone.
Things such as how a call or text is sent and received, pressing buttons to adjust volume or enter an application. The complex implementations that go on behind the scenes are not needed to be known by the user, only that pressing a button, or sending a text message, will do exactly what they expect.

This becomes a very useful principle when things such as an update for the phone (i.e.: changes being made to the background implementation), in that these changes should not need to change or affect the abstracted functions that the user knows about.

Going back to using the search example for instance; a change to the type of database or server that the company uses, should not necessarily need to affect the way a user searches for something.

Inheritance
-----------------
The ability to "inherit" the data properties and behaviours (functions) from another class or interface.

Class A "is a" or "has a" Class B relationship

```csharp
public class Person
{
    public string Name {get;set;}
    public int Age {get;set;}
}

public class Student: Person
{
    public string Grade {get;set;}
}

public class Teacher: Person
{
    public string Teaches {get;set;}
}

// ...

public static Main()
{
    Student student = new Student();
    student.Name = "Bill";
    student.Age = 15;
    student.Grade = "A";

    Teacher teacher = new Teacher();
    teacher.Name = "Mrs Foo";
    teacher.Age = 50;
    teacher.Teaches = "English";
}
```

Polymorphism
-----------------
Polymorphism is the ability to process objects differently depending on the data type or class.
It is the ability to redefine methods for a derived class using method overloading and method overriding.\

Example:

```csharp
public class Shape
{
    public virtual decimal CalculateArea();
}

public class Rectangle: Shape
{
    public decimal Height {get; set;}
    public decimal Width {get;set;}

    public override decimal CalculateArea()
    {
        return Height * Width;
    }
}

public class Square: Shape
{
    public decimal Length {get;set;}

    public override decimal CalculateArea()
    {
        return Math.Pow(Length, 2);  
    }
}
```

In this way, multiple shapes are able to inherit from the base of Shape and be treated as the same type of object, even though they all have differences in the way that the calculation method must be calculted.

Note:
* However, using the keyword base is a derived class able to access the base class method, if say the method was declared there.
* Using this with multiple-level inheritance, the virtual method will remain virtual throughout the levels of inheritance. The virtual method from class X will remain virtual if class Y inherits from X, and Z inherits from Y. The method in Z will not be the method from Y unless the keyword sealed is used.

```csharp
public class Z : Y
{
    public sealed override void Method() {}
}
```


Interview Questions
-----------------

* What is the difference between an interface and an abstract class?
> Answer

* Define polymorphism and explain how you can take advantage of it in a .NET application.
> Answer

* What is Entity Framework and how does it work on a basic level?
>Answer

* Explain the difference between overriding and overloading a method.
> Answer

* Value Vs Reference
> Answer

Constructors
-----------------
* What is a default constructor?
> Answer

* Can you overload constructors?
> Answer

* Can a constructor be private?
> Answer

* Is it legal to call a virtual method from within a constructor?
> Answer

Interfaces and Abstracts
-----------------
* What is an Interface?
> Answer

* Can an Interface contain fields?
> Answer

* Can an Interface be instantiated?
> Answer

* Can an Interface derive from another interface?
> Answer

* How does an abstract class differ from an interface?
> Answer

* When and why to use Inheritance vs Interface
> Answer


Multiple Inheritance
-----------------
* What is multiple inheritance?
> Answer

* Is it legal in C#?
> Answer

* Can you implement two interfaces with the same method name and signature?
> Answer

* Explain the difference between encapsulation and composition and when you would use each
> Answer

Polymorphism
-----------------
What is Polymorphism?
> Answer

Data Structures
-----------------
* Why would I use a HashSet instead of a List
> Answer

* How does List<T> work
> Answer
	
* How does a Hash Set (ie Dictionary<TKey,TValue>) work
> Answer

* Difference between Stack Vs Queue
> Answer

* Difference between Stack Vs Heap
> Answer

Generics
-----------------
* What is a Generic?
> Answer

* Why use a Generic?
> Answer

🚀 Algorithms 
=================
List
Stack
Queue
Heap


Lists
-----------------
Lists allow duplicate items, can be accessed by index, and support linear traversal.
List can hold duplicate objects.
> If you just want a list and don't care about any duplicates, i.e list of people, shopping list, list of things to do in life.

* ArrayList
An array-based list that doesn't support generic types. It does not enforce type safety and should generally be avoided.
Is just for compatibility with older versions of the framework where IList didn't exist
* List 
An array list that supports generic types and enforces type-safety. Since it is non-contiguous, it can grow in size without re-allocating memory for the entire list. This is the more commonly used list collection.

Hashes/Dictionary
-----------------
Hashes are look-ups in which you give each item in a list a "key" which will be used to retrieve it later. Think of a hash like a table index where you can ask questions like "I'm going to find this object by this string value. Duplicate keys are not allowed.
Is used to store pairs of key/value. You cannot have duplicate keys.
* HashTable
A basic key-value-pair map that functions like an indexed list.
Is basically a List with no possibility of duplicates (and better performance in some scenarios)
* Dictionary
A hashtable that supports generic types and enforces type-safety.

Queues
-----------------
Queues control how items in a list are accessed. You typically push/pop records from a queue in a particular direction (from either the front or back). Not used for random access in the middle.
>  If you want to simulate a queue for example, in a hospital you have a queue and also priority queue (in emergency departments). The triage would determine who is in critical condition and needs to be treated.
> Another example is a shopping queue, first person in line is 'usually' the first one to checkout.

* Stack
A LIFO (last in, first out) list where you push/pop records on top of each other.
Stores objects in order they were added (through Push()), and when you retrieve an object (through Pop()) it is removed from the stack in a LIFO manner.
> Used in your internal memory to push and pop values as you pass them to functions/methods.

* Queue
A FIFO (first in, first out) list where you push records on top and pop them off the bottom.
Quite similar to a Stack except it is FIFO.

🧳 C# / .NET CORE (Frameworks)
=================

⛓️ REST / Web API Programming
=================
* What is REST?
REpresentational State Transfer, is an architectural style for providing standards between computer systems on the web, making it easier for systems to communicate with each other.

* Why use REST?
With REST, the server is free to change the exposed resources at will. There is no fixed API above and beyond what REST itself defines. The client needs only know the initial URI, and subsequently chooses from server-supplied choices to navigate or perform actions.

Using REST correctly can help your system components remain properly decoupled and can be evolved more easily in the future than if you had tied them directly together in a typical RPC-like fashion.


HTTP Methods
-----------------
* GET
* POST

Headers
-----------------

Body/Content
-----------------

url-parameters
-----------------

HTTP Response Codes
-----------------

Server Side vs Clientside
-----------------

Interview Questions
-----------------
* Explain the architectural style for creating web API
> The architectural style for creating web api are
> * HTTP for client server communication
> * XML/JSON as formatting language
> * Simple URI as the address for the services
> * Stateless communication
	
* What tools are required to test your web API?
> Postman/SoapUI

* What are the HTTP methods supported by REST?
> GET: It requests a resource at the request URL. It should not contain a request body as it will be discarded. Maybe it can be cached locally or on the server.
> POST: It submits information to the service for processing; it should typically return the modified or new resource.
> PUT:  At the request URL it update the resource.
> DELETE: At the request URL it removes the resource.
> OPTIONS: It indicates which techniques are supported.
> HEAD: About the request URL it returns meta information.

* Can use GET request instead of PUT to create a resource
> No, you are not supposed to use POST or GET. GET operations should only have view rights.

* What are resources in a REST architecture?
> Resources are identified by logical URLs; it is the key element of a RESTful design. Unlike, SOAP web services in REST, you view the product data as a resource and this resource should contain all the required information.

* Some key characteristics of REST?
> Some key characteristics of REST includes
> * REST is stateless, therefore the SERVER has no state (or session data)
> * With a well-applied REST API, the server could be restarted between two calls as every data is passed to the server
> * Web service mostly uses POST method to make operations, whereas REST uses GET to access resources

* what is the difference between PUT and POST?
> "PUT" puts a file or resource at a particular URI and exactly at that URI. If there is already a file or resource at that URI, PUT changes that file or resource. If there is no resource or file there, PUT makes one

> POST sends data to a particular URI and expects the resource at that URI to deal with the request. The web server at this point can decide what to do with the data in the context of specified resource

* Which markup language can be used in Restful Web Api?
> JSON and XML are the two markup language that can be used


🤝🏼 ReactJS/JavaScript 
=================

💉 Dependency Injection
=================
* What is Dependency Injection?
> Dependency Injection, at least in programming, is just where you make sure to give each bit of "code" exactly what it depends on to do it's job.

Think of it like legos and I asked you to build a pirate ship for a lego boat race. I could let you do it however you wanted, finding the pieces, building out the pirate ship how you saw fit.
You'd have to go around and find pieces, maybe pieces that other builders want to use or that other builders changed when they last used that piece. You're pirate ship may not even float or meet the requirements for the boat race we're having.
But if I give you a box with the instructions and stickers and rules and all the pieces you needed to build your pirate ship, you don't have to go searching and you don't have to worry about something you need being broken or taken by someone else. I've given you everything you depend on to get the job (build the ship) done correctly.

This allows you to specialize in only following directions and building pirate ships. Not space ships. Or skyscrapers. And it allows us to measure how good you really are at building ships since we've eliminated as many things that could change as possible.
You might become the best and fastest lego pirate ship builder in the world but if the kit or rules change, you don't have to worry about finding pieces or learning the rules. I'm giving you the instructions and the pieces so you just have to keep doing what you were doing and nothing changes, to you.
Or I could swap in test pieces to see how they work with other existing pieces, or to measure how fast you built your ships or if there were any structural weaknesses. If I put the test pieces in a bucket, there's no guarantee that you'd use them. Or if you did use them and they broke, we wouldn't know exactly why. You may have used off brand legos. Or giant legos. Or broken legos.

In a nutshell, what it means is that any given piece of code you write should be provided everything it needs to do its job, instead of creating things for itself.
So say I'm writing a forum, and I'm specifically writing the code that adds a new user record to the database and sends them an email to confirm their registration.

If I used dependency injection, that piece of code would be given a data model/database connecton to work with (instead of creating a new instance of one) and a external class with a pre-defined interface to send email instead of creating an SMTP client object.

* Dependency Injection with Dependency Inversion
For a lot of reasons, it makes sense to break any significant piece of software up into pieces. This is because humans can only deal with a certain amount of complexity at one time. If every developer on a project had to know everything about every piece of the project, they wouldn't get much done.
So code is broken up into modules. The size and relationships between these modules depends on the problem the software is trying to solve. It turns out that a significant source of complexity in software projects is how these different modules change over time (from version to version), and how those changes affect the other modules that depend upon them.


For instance, let's say that you are writing software that manages cruise ships for a cruise business. A call at the top layer might do something like take customer info and cruise info a book passage on that cruise for that customer. This is a very high level operation that directly implements a "use case" (a customer-facing capability that provides a complete user interaction).
That top layer calls several things in the middle layer to accomplish this; it does things like call a billing module that places a hold on the customer's credit card to authorize payment, then updates a schedule to reserve a cabin on a particular ship for a particular trip, then charges the credit card, then calls an excursion planner module to get a bunch of suggestions for other things the customer can book in various ports, then finally calls an email module to send a confirmation email to the customer with all trip info.
If you follow any particular call into any particular system, at some point you'l get to a point where you see many of these modules are calling into modules that no longer directly relate to the business at all. These modules provide generic functionality like "trim the whitespace off both ends of this string" or "sum this list of numbers".
Note the direction of dependencies: the top layer that books passage depends upon stuff in the middle layer, the middle layer that reserves cabins relies on the string and math libraries. This might seem fine at first, but it means whenever some low level piece of functionality changes, every other part of the codebase is affected. This is not good for a variety of reasons. Good, modular design should isolate modules from the effects of changes that don't matter in other modules.
This is what dependency inversion does. Instead of relying upon the code that does string manipulation directly, instead you rely on a very abstract interface that defines what the string code should do, but doesn't actually provide the code itself. Then, you have the code which implements that string manipulation functionality rely on that same definition. In this way, both the code that calls the functionality and the code that provides it rely on this piece in the middle that is very highly abstract, and only defines the contract between the two. This way, if the contract doesn't change, then either module on either side is able to change things in a way that doesn't affect the other.



🧨 SOLID Principles
=================
* Single Responsibility
* Open - Closed
* Liskov Substitution
* Interface Segregation
* Dependency Inversion
These are the 5 principles that help software designs be more understandable, flexible and adaptable.


Solid Responsibility Principle
-----------------
The basic idea with this principle is that every module, class or function, should have the responsibilty for only a single piece of functionality.
That responsibility should therefore be encapsulated entirely within something such as a class.
Thus there should be only a single reason why this piece of functionality should change (Business and Logic changes separated).

> Why do this? 

* Makes it easier to verify that this single piece of functionality is doing as it should.
* Splits a bigger process into smaller more manageable parts
* Creates reusable pieces 


Open - Closed Principle
-----------------
The idea that modules, class and functions should be open for extension but closed for modification.
This pertains a lot to inheritance (Meyer's) and polymorphism.

Polymorphic Open - Closed Principle refers to dealing with abstracted interfaces. Whereby various implementations of such an abstracted base class can be created through inheritance.

An example of such a thing would be having an abstracted base Shape() with a declared function of CalculateArea().
The implementations of this base could be Square(), Triangle() and Circle() that use CalculateArea().
However, CalculateArea() may be different functions throughout these different implementations, dependent on the needs of the derived class.

Square(): CalculateArea() => height ^ 2
Triangle(): CalculateArea() => (height * base) / 2
Circle(): CalculateArea() => (pi) * radius ^ 2

Here we know that for each of the classes derived from Shape() needs to CalculateArea(), but not all in the same way or how they will go about it, so the CalculateArea() function is inherited, but overwritten in the derived classes.
The existing interface is closed to modifications but new implementations of it are open to extension upon an unbounded group of possibilities of this function.


> Why Do This?

* Reduces fragility
* Reduces the need to make smaller repeated changes everywhere

Liskov Substitution Principle
-----------------
A statement that
> S is a subtype of T, then objects of type T must be replaced with objects of type S

In a nutshell, the relationship between S and T is that subtype S "is substitutional for" type T, rather than a "is a" relationship.
That the child class is the parent class and should thus be able to reference the child class as the base class,

```csharp
BaseClass child = new ChildClass();
// should have the same results as
ChildClass chile = new ChildClass();
```
A violation of this principle would be that if a parent class' behaviour is changed within a child class.

Interface Segregation Principle
-----------------

The concept of this principle is that no client should be forced to depend on methods it doesn't use.
The idea of this is to split larger interfaces into smaller and more specific interfaces called role interfaces, in for derived classes to only concern themselves with the methods and data that relates to them.

This principle means thinking about how changes to the interface could affect the derived classes and how these classes may force changes upon their inherited interfaces and what we can do to minimise that.

Example:
```csharp
public interface IVehicle
{
    void Drive();
    void Fly();
    void Sail();
}

public class ChittyBangBang : IVehicle
{
    public void Drive()
    {
        // actions
        Console.WriteLine("It can drive like a car!");
    }
    public void Fly()
    {
        // actions
        Console.WriteLine("It can fly like a plane!");
    }
    public void Sail()
    {
        // actions
        Console.WriteLine("It can sail like a boat!");
    }
}

//However
public class Car : IVehicle
{
    public void Drive()
    {
        // actions
        Console.WriteLine("It can drive like a car!");
    }

    public void Fly(){ throw new NotImplementedException();}

    public void Sail(){ throw new NotImplementedException();}
}

public class Airplane : IVehicle
{
    public void Drive(){ throw new NotImplementedException();}

    public void Fly()
    {
        // actions
        Console.WriteLine("It can fly like a plane!");
    }

    public void Sail(){ throw new NotImplementedException();}
}
```

This example shows that while there is one user that implements all three methods of Drive, Fly and Sail, the other users that inherit this interface have no need for them and must throw exceptions.

The solution is to adopt this Interface Segregation Principle and separate these Interfaces.

```csharp
public interface ICar { void Drive(); }
public interface IPlane { void Fly(); }
public interface IBoat { void Sail(); }

public class ChittyBangBang : ICar, IPlane, IBoat 
{
    public void Drive(){/* actions...  */}
    public void Fly(){/* actions...  */}
    public void Sail(){/* actions...  */}
}

public class Car : ICar { public void Drive(){/* actions...  */} }
public class Plane : IPlane { public void Fly(){/* actions...  */} }
public class Boat : IBoat { public void Sail(){/* actions...  */} }
```

Whereas here we can see that the Vehicles are only needing the Interfaces which have the relevant methods that that particular class needs.
Though this results in having many interfaces, it does indeed help overall when changes are needing to be made and prevents us from having larger interfaces where methods are redundant for many inherited classes.

> Why Do This?

* Helps keep a system decoupled (preventing unneccessary dependencies)
* Helps keep things easier to refactor, change and redeploy
* Reduces interface pollution (polluted with things that derived classes do not require)

Dependency Inversion Principle
-----------------
Consequently if the Liskov Substitution and Open - Closed Principles are followed and applied into a software design, the code will also comply with the Dependency Inversion Principle.

It focuses on interface abstraction between higher and lower level software components in order to remove the dependencies between them.

Robert C. Martin's definition for this principle is made up of two parts:
> High-level modules should not depend on low-level modules. Both should depend on abstractions
> Abstractions should not depend on details. Details should depend on abstractions.

Say you have different types of Coffee Machines that all perform differing levels of ability and functions. This example will look at a basic and complex coffee machine.

One can create an interface for CoffeeMachine, which is implemented in both a BasicCoffeeMachine and a ComplexCoffeeMachine.
CoffeeMachine has a single method to BrewFilterCoffee. And each implementation of the CoffeeMachine interface also has more specfic methods for them.

While both machines essentially brew types of coffee, espresso brewing is quite different and the ComplexCoffeeMachine can both BrewFilterCoffee and BrewEspressoCoffee.
A way to abstract these from one another would be to create separate interfaces.


```csharp
public interface CoffeeMachine
{
    void brewFilterCoffee();
}

public interface EspressoMachine
{
    void brewEspressoCoffee();
}
```

This enables then for both the BasicCoffeeMachine and the ComplexCoffeeMachine to take the interfaces and methods that they requires, without the higher level interface depending on the details of the lower-level implementations.

It also allows the addition of new functionality in terms of the brewEspressoCoffee, without needing to change the existing functionality of brewFilterCoffee that is already implemented elsewhere.


```csharp
public class BasicCoffeeMachine : CoffeeMachine
{
    public void brewFilterCoffee() { /* some action here */};
}

public class ComplexCoffeeMachine : CoffeeMachine, EspressoMachine
{
    public void brewEspressoCoffee() { /* some action here */};
    public void brewFilterCoffee() { /* some action here */};
}
```



🚀 Introduction To Design Patterns
=================
Design patterns are solutions to recurring problems; guidelines on how to tackle certain problems. They are not classes, packages or libraries that you can plug into your application and wait for the magic to happen. These are, rather, guidelines on how to tackle certain problems in certain situations.

> Design patterns solutions to recurring problems; guidelines on how to tackle certain problems

Types of Design Patterns
-----------------

* [Creational](#creational-design-patterns)
* [Structural](#structural-design-patterns)
* [Behavioral](#behavioral-design-patterns)

* MVC, Singleton, Factory
* Strategy, Template Method, Bridge


Creational Design Patterns
==========================

In plain words
> Creational patterns are focused towards how to instantiate an object or group of related objects.

 * [Simple Factory](#-simple-factory)
 * [Factory Method](#-factory-method)
 * [Abstract Factory](#-abstract-factory)
 * [Builder](#-builder)
 * [Prototype](#-prototype)
 * [Singleton](#-singleton)

🏠 Simple Factory
--------------
Real world example
> Consider, you are building a house and you need doors. It would be a mess if every time you need a door, you put on your carpenter clothes and start making a door in your house. Instead you get it made from a factory.

In plain words
> Simple factory simply generates an instance for client without exposing any instantiation logic to the client

**Programmatic Example**

First of all we have a door interface and the implementation
```csharp
public interface IDoor
{
    float Width { get; set; }
    float Height { get; set; }
}

public class WoodenDoor : IDoor
{
    public float Width { get; set; }
    public float Height { get; set; }

    public WoodenDoor(float width, float height)
    {
        Width = width;
        Height = height;
    }
}
```
Then we have our door factory that makes the door and returns it
```csharp
class DoorFactory
{
   public static IDoor MakeDoor(float width, float height)
   {
       return new WoodenDoor(width, height);
   }
}
```
And then it can be used as
```csharp
var door = DoorFactory.makeDoor(100, 200);
Console.WriteLine("Width: " + door.Width);
Console.WriteLine("Height: " + door.Height);
```

**When to Use?**

When creating an object is not just a few assignments and involves some logic, it makes sense to put it in a dedicated factory instead of repeating the same code everywhere. 

🏭 Factory Method
--------------

Real world example
> Consider the case of a hiring manager. It is impossible for one person to interview for each of the positions. Based on the job opening, she has to decide and delegate the interview steps to different people. 

In plain words
> It provides a way to delegate the instantiation logic to child classes. 

Wikipedia says
> In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.
 
 **Programmatic Example**
 
Taking our hiring manager example above. First of all we have an interviewer interface and some implementations for it

```csharp
interface IInterviewer
{
    void AskQuestions();
}

class Developer : IInterviewer
{
    public void AskQuestions()
    {
        Console.WriteLine("Asking about design patterns!");
    }
}

class CommunityExecutive : IInterviewer
{
    public void AskQuestions()
    {
        Console.WriteLine("Asking about community building");
    }
}
```

Now let us create our `HiringManager`

```csharp
abstract class HiringManager
{
    // Factory method
    abstract public IInterviewer MakeInterviewer();
    
    public void TakeInterview()
    {
        var interviewer = MakeInterviewer();
        interviewer.AskQuestions();
    }
}
```
Now any child can extend it and provide the required interviewer
```csharp
class DevelopmentManager : HiringManager
{
    public IInterviewer MakeInterviewer()
    {
        return new Developer();
    }
}

class MarketingManager : HiringManager
{
    public IInterviewer MakeInterviewer()
    {
        return new CommunityExecutive();
    }
}
```
and then it can be used as

```csharp
var devManager = new DevelopmentManager();
devManager.TakeInterview(); // Output: Asking about design patterns

var marketingManager = new MarketingManager();
marketingManager.TakeInterview(); // Output: Asking about community building.
```

**When to use?**

Useful when there is some generic processing in a class but the required sub-class is dynamically decided at runtime. Or putting it in other words, when the client doesn't know what exact sub-class it might need.

🔨 Abstract Factory
----------------

Real world example
> Extending our door example from Simple Factory. Based on your needs you might get a wooden door from a wooden door shop, iron door from an iron shop or a PVC door from the relevant shop. Plus you might need a guy with different kind of specialities to fit the door, for example a carpenter for wooden door, welder for iron door etc. As you can see there is a dependency between the doors now, wooden door needs carpenter, iron door needs a welder etc.

In plain words
> A factory of factories; a factory that groups the individual but related/dependent factories together without specifying their concrete classes. 
  
Wikipedia says
> The abstract factory pattern provides a way to encapsulate a group of individual factories that have a common theme without specifying their concrete classes

**Programmatic Example**

Translating the door example above. First of all we have our `Door` interface and some implementation for it

```csharp
interface IDoor
{
    void GetDescription();
}

class WoodenDoor : IDoor
{
    public void GetDescription()
    {
        Console.WriteLine("I am a wooden door");
    }
}

class IronDoor : IDoor
{
    public void GetDescription()
    {
        Console.WriteLine("I am a iron door");
    }
}
```
Then we have some fitting experts for each door type

```csharp
interface IDoorFittingExpert
{
    void GetDescription();
}

class Welder : IDoorFittingExpert
{
    public void GetDescription()
    {
        Console.WriteLine("I can only fit iron doors");
    }
}

class Carpenter : IDoorFittingExpert
{
    public void GetDescription()
    {
        Console.WriteLine("I can only fit wooden doors");
    }
}
```

Now we have our abstract factory that would let us make family of related objects i.e. wooden door factory would create a wooden door and wooden door fitting expert and iron door factory would create an iron door and iron door fitting expert
```csharp
interface IDoorFactory
{
    IDoor MakeDoor();
    IDoorFittingExpert MakeFittingExpert();
}

// Wooden factory to return carpenter and wooden door
class WoodenDoorFactory : IDoorFactory
{
    public IDoor MakeDoor()
    {
        return new WoodenDoor();
    }

    public IDoorFittingExpert MakeFittingExpert() 
    {
        return new Carpenter();
    }
}

// Iron door factory to get iron door and the relevant fitting expert
class IronDoorFactory : IDoorFactory
{
    public IDoor MakeDoor()
    {
        return new IronDoor();
    }

    public IDoorFittingExpert MakeFittingExpert()
    {
        return new Welder();
    }
}
```
And then it can be used as
```csharp
var woodenFactory = new WoodenDoorFactory();

var door = woodenFactory.MakeDoor();
var expert = woodenFactory.MakeFittingExpert();

door.GetDescription();  // Output: I am a wooden door
expert.GetDescription(); // Output: I can only fit wooden doors

// Same for Iron Factory
var ironFactory = new IronDoorFactory();

var door = ironFactory.MakeDoor();
var expert = ironFactory.MakeFittingExpert();

door.GetDescription();  // Output: I am an iron door
expert.GetDescription(); // Output: I can only fit iron doors
```

As you can see the wooden door factory has encapsulated the `carpenter` and the `wooden door` also iron door factory has encapsulated the `iron door` and `welder`. And thus it had helped us make sure that for each of the created door, we do not get a wrong fitting expert.   

**When to use?**

When there are interrelated dependencies with not-that-simple creation logic involved

👷 Builder
--------------------------------------------
Real world example
> Imagine you are at Hardee's and you order a specific deal, lets say, "Big Hardee" and they hand it over to you without *any questions*; this is the example of simple factory. But there are cases when the creation logic might involve more steps. For example you want a customized Subway deal, you have several options in how your burger is made e.g what bread do you want? what types of sauces would you like? What cheese would you want? etc. In such cases builder pattern comes to the rescue.

In plain words
> Allows you to create different flavors of an object while avoiding constructor pollution. Useful when there could be several flavors of an object. Or when there are a lot of steps involved in creation of an object.
 
Wikipedia says
> The builder pattern is an object creation software design pattern with the intentions of finding a solution to the telescoping constructor anti-pattern.

Having said that let me add a bit about what telescoping constructor anti-pattern is. At one point or the other we have all seen a constructor like below:
 
```csharp
public Burger(size, cheese = true, pepperoni = true, tomato = false, lettuce = true)
{
}
```

As you can see; the number of constructor parameters can quickly get out of hand and it might become difficult to understand the arrangement of parameters. Plus this parameter list could keep on growing if you would want to add more options in future. This is called telescoping constructor anti-pattern.

**Programmatic Example**

The sane alternative is to use the builder pattern. First of all we have our burger that we want to make

```csharp
class Burger
{
    public int Size { get; }

    public bool Cheese { get; }
    public bool Pepperoni { get; }
    public bool Lettuce { get; }
    public bool Tomato { get; }
    
    public Burger(BurgerBuilder builder)
    {
        Size = builder.Size;
        Cheese = builder.Cheese;
        Pepperoni = builder.Pepperoni;
        Lettuce = builder.Lettuce;
        Tomato = builder.Tomato;
    }
}
```

And then we have the builder

```csharp
class BurgerBuilder
{
    public int Size { get; }

    public bool Cheese { get; private set; }
    public bool Pepperoni { get; private set; }
    public bool Lettuce { get; private set; }
    public bool Tomato { get; private set; }

    public BurgerBuilder(int size)
    {
        Size = size;
    }
    
    public BurgerBuilder AddPepperoni()
    {
        Pepperoni = true;
        return this;
    }
    
    public BurgerBuilder AddLettuce()
    {
        Lettuce = true;
        return this;
    }
    
    public BurgerBuilder AddCheese()
    {
        Cheese = true;
        return this;
    }
    
    public BurgerBuilder AddTomato()
    {
        Tomato = true;
        return this;
    }
    
    public Burger Build()
    {
        return new Burger(this);
    }
}
```
And then it can be used as:

```csharp
var burger = new BurgerBuilder(14)
		.AddPepperoni()
		.AddLettuce()
		.AddTomato()
		.Build();
```

**When to use?**

When there could be several flavors of an object and to avoid the constructor telescoping. The key difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.

🐑 Prototype
------------
Real world example
> Remember dolly? The sheep that was cloned! Lets not get into the details but the key point here is that it is all about cloning

In plain words
> Create object based on an existing object through cloning.

Wikipedia says
> The prototype pattern is a creational design pattern in software development. It is used when the type of objects to create is determined by a prototypical instance, which is cloned to produce new objects.

In short, it allows you to create a copy of an existing object and modify it to your needs, instead of going through the trouble of creating an object from scratch and setting it up.

**Programmatic Example**

In C#, it can be easily done using `ICloneable`
  
```csharp
class Sheep : ICloneable
{
    public string Name { get; set; }
    public string Category { get; set; }

    public Sheep(string name, string category = "Mountain Sheep")
    {
        Name = name;
        Category = category;
    }
	
    public object Clone()
    {
    	return this.MemberwiseClone();
    }
}
```
Then it can be cloned like below
```csharp
var original = new Sheep('Jolly');
Console.WriteLine(original.Name); // Jolly
Console.WriteLine(original.Category); // Mountain Sheep

// Clone and modify what is required
var cloned = original.Clone();
cloned.Name = "Dolly";
Console.WriteLine(cloned.Name); // Dolly
Console.WriteLine(cloned.Category); // Mountain Sheep
```

Also you could use the magic method `Clone` to modify the cloning behavior.

**When to use?**

When an object is required that is similar to existing object or when the creation would be expensive as compared to cloning.


💍 Singleton
------------
Real world example
> There can only be one president of a country at a time. The same president has to be brought to action, whenever duty calls. President here is singleton.

In plain words
> Ensures that only one object of a particular class is ever created.

Wikipedia says
> In software engineering, the singleton pattern is a software design pattern that restricts the instantiation of a class to one object. This is useful when exactly one object is needed to coordinate actions across the system.

Singleton pattern is actually considered an anti-pattern and overuse of it should be avoided. It is not necessarily bad and could have some valid use-cases but should be used with caution because it introduces a global state in your application and change to it in one place could affect in the other areas and it could become pretty difficult to debug. The other bad thing about them is it makes your code tightly coupled plus it mocking the singleton could be difficult.

**Programmatic Example**

To create a singleton, make the constructor private, disable cloning, disable extension and create a static variable to house the instance
```csharp
// Example taken from http://csharpindepth.com/Articles/General/Singleton.aspx
// There is a lot of caveat. So read it!
public sealed class President
{
    private static readonly President instance = new President();

    // Explicit static constructor to tell C# compiler
    // not to mark type as beforefieldinit
    static President()
    {
    }

    private President()
    {
    }

    public static President Instance
    {
        get
        {
            return instance;
        }
    }
} 
```
Then in order to use
```csharp
var president1 = President.Instance;
var president2 = President.Instance;

Console.WriteLine(President1 == President2); // true
```
