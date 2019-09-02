# MyLearnings
My Own Personal Learnings

🚀 Introduction
=================
* [OOP](#creational-design-patterns)
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

🧳 C# / .NET CORE (Frameworks)
=================

⛓️ REST / API Programming
=================

🤝🏼 ReactJS/JavaScript 
=================

💉 Dependency Injection
=================

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
