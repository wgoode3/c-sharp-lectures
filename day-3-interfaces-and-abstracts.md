# Day 3 - C# Interfaces and Abstracts

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

## Abstract Class

By now we've probably seen how inheritance can lead to us writing <abbr title="Don't Repeat Yourself">DRY</abbr> code, often times we might end up in a situation where the base class that we use with different but closely related classes never needs to be implemented itself. In heavily OOP languages like C#, we can declare such a class `abstract` and enforce that this class is to be used soley to be inherited from.

If we define a `Person` class as abstract...

```cs
// inside of Person.cs
namespace Things.Models {
    public abstract class Person
    {
        public string Name {get;set;}

        public Person(string name)
        {
            Name = name;
        }
    }
}
```
we won't be able to make an instace of it in the `Program` class.

```cs
// inside of Program.cs
using Things.Models;
namespace Things {
    class Program
    {
        static void Main(string[] args)
        {
            Person Ed = new Person("Ed");
        }
    }
}
```

this will throw an error of...

```
Program.cs(10,25): error CS0144: Cannot create an instance of the abstract class or interface 'Person' 
```

Instead, we need to make a class that can inherate the `Person` class to use it.

```cs
// inside of Student.cs
namespace Things.Models {
    public class Student : Person
    {
        public string Name {get;set;}
        public int NumBelts {get;set;}

        public Student(string name, int numBelts) : base(name)
        {
            NumBelts = numBelts;
        }
    }
}
```

Now with this student class we can make a `Person`.

```cs
// inside of Program.cs
static void Main(string[] args)
{
    Person Ed = new Student("Ed", 1);
    Student Edd = new Student("Edd", 2);
}
```

We can say the variable that we create is a `Person` or a `Student`, but when go to create it has to be a `new Student(...)`.

## Interface

Let's say we want to be able to make a `Bird` class in addition to our `Student` class, and as part of this `Bird` class we want the bird to be able to make some sort of noises. 

As this is something that we also want students to be able to do we might think to add a `public void MakeNoise()` method into our `Person` class, but it wouldn't make sense for a `Bird` to also inherate from `Person`. 

In this case where we have unrelated classes that we want to be able to make share some functionality we can use an **Interface**. 

```cs
// inside of IVocalizable.cs
using System;
namespace Things.Models 
{
    interface IVocalizable
    {
        virtual void MakeNoise()
        {
            Console.WriteLine("DEFAULT NOISE");
        }
    }
}
```

And when we make a `Bird` we can implement this interface...

```cs
// inside of Bird.cs
using System;
namespace Things.Models 
{
    class Bird : IVocalizable
    {
        public string Name {get;set;}
        
        public Bird(string name)
        {
            Name = name;
        }
        
        public override void MakeNoise()
        {
            Console.WriteLine("Chirp chirp!");
        }
        
    }
}
```

we can also rewrite our student to use it as well

```cs
// inside of Student.cs
namespace Things.Models
{
    public class Student : Person, IVocalizable
    {
        public string Name {get;set;}
        public int NumBelts {get;set;}

        public Student(string name, int numBelts) : base(name)
        {
            NumBelts = numBelts;
        }
        
        public override void MakeNoise()
        {
            Console.WriteLine($"Hi my name is {Name}");
        }
    }
}
```

So what did this accomplish? Let's say there is some room that contains students and birds, we can hear all of the noises they might make.

```cs
// inside of Program.cs
{
    List<IVocalizable> SomeRoom = new List<IVocalizable>(){
        new Student("Ed", 1),
        new Student("Edd", 2),
        new Bird("Eddy")
    };
    // let's hear them all!
    foreach(IVocalizable thing in SomeRoom)
    {
        thing.MakeNoise();
    }
}
```

We're able to group all of the students and birds into a `List` even though they are different classes because they all implement `IVocalizable`. Once again when we loop through them we can make them all `MakeNoise()` because they all have implemented `IVocalizable`.

We can treat `IVocalizable` like a promise that any class that implements it must be able to `MakeNoise()`.

## Abstracts vs Interfaces

<img src="https://raw.githubusercontent.com/wgoode3/c-sharp-lectures/master/assets/abstracts-interfaces.png" alt="diagram" />
