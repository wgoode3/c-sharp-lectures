# Day 2 - C# OOP

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

### OOP Questions

1. <details>
    <summary>What are the four pillars of OOP?</summary>
    <ul>
        <li>Encapsulation</li>
        <li>Abstraction</li>
        <li>Polymorphism</li>
        <li>Inheritance</li>
    </ul>
</details>

2. <details>
    <summary>What are the benefits of OOP?</summary>
    <ul>
        <li>Resuability</li>
        <li>Simplicity</li>
        <li>Easily Maintainable</li>
        <li>Security for Class Variables</li>
    </ul>
</details>

### Class Construction in C#

We can make class members accessible with access modifiers.<br>
If a member is private then it can only be accessed with that class.<br>
This means that even the instance of the object can't access the private member.

#### Modularization with Classes

```
├ HelloWorld/
  ├ bin/
  ├ obj/
  ├ Models/
    ├ Person.cs
  ├ HelloWorld.csproj
  ├ Program.cs
```

If we want to access the classes in our Program.cs file, then we need to add a using statement at the top of the file.

```cs
using System;
using System.Collections.Generic;
using MyCoolProject.Models;

namespace MyCoolProject
{
    class Program
    {
        static void Main(string[] args)
        {
            Person adrien = new Person("Adrien",38);
        }
    }
}

```

#### Access Modifiers

* public
* private
* protected
* internal

#### Class Memebers

* Fields
* Properties
* Methods


```cs

public class Person
{
    public string Name;
    private int age;

    public Person(string _name,int _age)
    {
        Name = _name;
        age = _age;
    }

    public int Age
    {
        get
        {
            return age;
        }
        set
        {
            if(value < 0)
            {
                Console.WriteLine($"{Name} isn't Benjiman Button!!!")
            }
            else
            {
                age = value;
            }
        }
    }

    public virtual void SayName()
    {
        Console.WriteLine($"Hello, my name is {Name}");
    }
}
```

We can make the age field private so that it is shielded from the outside, and then make it accessible through a property.

#### But why are we making a field private only to make it accessible in a property?

By making the private variable accessible through the property, the class can control how the age field is set.<br>



### Class Inheritance

Classes can inherit fields, properties, and methods from other classes.<br>
Below the Ninja class inherits from the Person class.

```cs


public class Ninja : Person
{
    public int Strength;
    public int Dexterity;
    public int Speed;

    public Ninja(string name, int age, int str, int dex, int spd) : base(name,age)
    {
        Strength = str;
        Dexterity = dex;
        Speed = spd;
    }

    public override void SayName()
    {
        Console.WriteLine($"Hello my name is {Name}, and I'm a ninja!")
    }

    
}

```

The parent class is refered to as the base class, and in our constructors, we call on the base.  Now we can reuse the Name and Age fields from the Person class in our Ninja class, and not rewrite the code again.<br>

We implement the virtual keyword on a base class method if we want to be able to customize it in our child class.<br>
We then use the override keyword in our child class.<br>

*side note: We can call the base method SayName from the child class with base.SayName()*

When it comes to inheritance...

<img src="https://i.imgflip.com/3v4xco.jpg" alt="base class" height="500px" />

