# Day 1 - C# Fundamentals

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

*fun fact: C# has no offial logo*

### dotnet

```sh
dotnet new console -o HelloWorld
```

```
- HelloWorld/
| - bin/
| - obj/
| - HelloWorld.csproj
| - Program.cs
```

### Console Programs

```cs
using System;

namespace HelloWorld 
{
  class Program 
  {
    static void Main(string[] args)
    {
      Console.WriteLine("Hello World");
    }
  }
}
```

### C# Types

* int
* double
* string
* bool

### Arrays and Lists

#### Arrays

In C# we have to tell our arrays what type of data to expect...

```cs
string[] foods = new string[4];
foods[0] = "bagels";
foods[1] = "cream cheese";
foods[4] = "smoked salmon";
foods[3] = "capers";
```

Or more conveniently we could write this as...

```cs
string[] foods = new string[]{
  "bagels",
  "cream cheese",
  "smoked salmon",
  "capers"
};
```

If we go to print this out ```Console.WriteLine(foods);``` we get...

```
System.String[]
```

Helpful right? C# makes no assumptions about what we want to see here and instead tells us that "yep, it's a string array alright".

<img src="https://i.kym-cdn.com/photos/images/original/000/816/782/cce.jpg" alt="wood" height="500px" />

To see the contents of the array we might instead do something like this...

```cs
Console.WriteLine(String.Join(", ", foods));
```

#### Changing the size of an array

You don't. Once you've created the array you've promised C# this is how big the array needs to be. We weren't lying to C# when we told it our array was size 4 right? 

If we need a bigger array we'll have to make a new one, or what if there were something else we could do?

#### Lists

### Loops and Conditionals

### static
