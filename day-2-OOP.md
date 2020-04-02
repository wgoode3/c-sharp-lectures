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

```cs

public class Person
{
    public string Name;
    private int age;

    public Person(string _name,int _age)
    {
        Name = _name;
        Age = _age;
    }

    public int Age
    {
        get{
            return age;
        }
    }

    public int Birthday()
    {
        age ++;
        return age;
    }


    
}

```

### Quiz Time: 

1. <details>
    <summary>What are four common access modifiers?</summary>
    <ul>
        <li>public</li>
        <li>private</li>
        <li>protected</li>
        <li>internal</li>
    </ul>
</details>

2. <details>
    <summary>What are the three memebers of a class?</summary>
    <ul>
        <li>Fields</li>
        <li>Properties</li>
        <li>Methods</li>
    </ul>
</details>

### Class Inheritance

Classes can inherit fields, properties, and methods from other classes.
Below the Ninja class inherits from the Person class.

```cs

public class Person
{
    public string Name;
    protected int Age;
    public int Age
    {
        get{
            return age;
        }
    }

    public virtual int Birthday()
    {
        age ++;
        return age;
    }
}

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

    public override int Birthday()
    {
        age += 2;
        return age;
    }
}

```

The parent class is refered to as the base class, and in our constructors, we call on the base.  Now we can reuse the Name and Age fields from the Person class in our Ninja class, and not rewrite the code again.

When it comes to inheritance...

<img src="https://i.imgflip.com/3v4xco.jpg" alt="base class" height="500px" />

