# Day 1 - C# Fundamentals

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

*fun fact: C# has no official logo*

### dotnet

Dotnet is a pretty awesome platform, and once we have it installed we can quickly generate a number of different types of projects. We will start out making `console` (terminal based) programs.

```sh
dotnet new console -o HelloWorld
```

This will generate a project that looks much like this...

```
├ HelloWorld/
  ├ bin/
  ├ obj/
  ├ HelloWorld.csproj
  ├ Program.cs
```

#### To interprete or to compile?

|               | Compiled Languages                     | Interpreted Languages                  |
|---------------|----------------------------------------|----------------------------------------|
| Advantages    | speed <br> checks code at compile time | flexibility <br> source code is public |
| Disadvantages | source code is private                 | tends to be slower                     |

C# will compile our program into an intermediate language (we can see it in the `bin/` folder) that can then be run by Dotnet for us.  

When we use the `dotnet run` command all of this will happen. 

If we want to just run the compile step without running the code we can use `dotnet build`. 

#### Errors

Compile Time vs. Runtime

### `Program.cs`

<img src="https://raw.githubusercontent.com/wgoode3/c-sharp-lectures/master/assets/cs-anatomy.png" alt="c sharp hello world" />

### C# Types

* int
* double
* char
* string
* bool

Declaring variables...

```cs
int favoriteNumber = 3;
double averageTemperature = 18.2;
char selectedLetter = 'x';
string welcomeMessage = "Hello World!";
bool likesCSharp = true;
```

will work about how we'd expect. One thing to note is that `'` and `"` can't be used interchangebly like we could in other languages, the single quote is used for `char`s (1 character) and the double quote is used for `string`s (any number of chacaters). C# is also capable of inferring what type our variables are if we use the keyword `var`...

```cs
var someNumber = 5;
var someString = "Howdy Planet?";
```

However we still won't be able to change a variable from one type to another...

```cs
someNumber = false;
someString = -33.33;
```

both of these will surely fail.

### Arrays and Lists and Dictionaries, oh my!

#### Arrays

In C# we have to tell our arrays what type of data to expect...

```cs
string[] foodArray = new string[4];
foodArray[0] = "bagels";
foodArray[1] = "cream cheese";
foodArray[4] = "smoked salmon";
foodArray[3] = "capers";
```

Or more conveniently we could write this as...

```cs
string[] foodArray = new string[]{
    "bagels",
    "cream cheese",
    "smoked salmon",
    "capers"
};
```

If we go to print this out `Console.WriteLine(foodArray);` we get...

```
System.String[]
```

Helpful right? C# makes no assumptions about what we want to see here and instead tells us that "yep, it's a string array alright".

<img src="https://i.kym-cdn.com/photos/images/original/000/816/782/cce.jpg" alt="wood" height="500px" />

To see the contents of the array we might instead do something like this...

```cs
Console.WriteLine(String.Join(", ", foodArray));
```

#### Changing the size of an array

We don't. Once we've created the array we've promised C# this is how big the array needs to be. We weren't lying to C# when we told it our array was size 4 right? 

If we need a bigger array we'll have to make a new one, or what if there were something else we could do?

#### Lists

C# fortunately has a `List` we can store things in much like the array, and it is a good bit more flexible for us to use. In order to make use of this though, we will be needing to import something...

```cs
using System.Collections.Generic;
```

The syntax might look a bit strange at first, but we still need to let the `List` know what type of data it will hold...

```cs
List<string> foodList = new List<string>() {
    "bagels",
    "cream cheese",
    "smoked salmon",
    "capers"
};
```

But now we can add more things in when we want to...

```cs
foodList.Add("dill");
foodList.Add("onion");
```

#### Dictionaries

Once again, we'll need to make sure we've imported `System.Collections.Generic` but this time we also need to specify what the type of our key and value will be...

```cs
Dictionary<string, string> user = new Dictionary<string, string>();
user["name"] = "Example McExampleface";
user["email"] = "example@example.com";
```

Otherwise it will work about how we're used to from JavaScript and Python.

### Loops and Conditionals

#### for

We can write loops just about how we might be used to from other languages...

```cs
for(int i=0; i<3; i++)
{
    Console.WriteLine(i);
}
```

If we want to loop over an Array or a List we can reference their sizes like so...

```cs
// array
for(int i=0; i<myArray.Length; i++)
{
    Console.WriteLine(myArray[i]);
}
// list
for(int i=0; i<myList.Count; i++)
{
    Console.WriteLine(myList[i]);
}
```

The thing to remember is that arrays have `Length` and that lists have `Count`. 

If we don't need to know about the index we could use the more convenient method called `foreach()`.

```cs 
foreach(int value in myArray){
    Console.writeLine(value);
}
foreach(int value in myList){
    Console.writeLine(value);
}
```

`foreach` will work just fine with both Arrays and Lists, in fact it'll work with any `IEnumerable` (we'll be discussing these later). 

#### while

We can still write `while` loops too!

```cs
string input = "";
while(!input.Equals("uncle"))
{
    Console.WriteLine("Say uncle!");
    input = Console.ReadLine();
}
```

#### Conditionals

```cs
int numberOfLights = 4;
Console.WriteLine($"There are {numberOfLights} lights!");
numberOfLights = 1;
Console.WriteLine($"There are {numberOfLights} lights!");
```

If we want the grammar to sound right, we'll need to be able to change the wording a bit if there is only 1 light... we can use a conditional for this.

```cs
if(numberOfLights == 1) 
{
    Console.WriteLine("There is 1 light!");
}
else
{
    Console.WriteLine($"There are {numberOfLights} lights!");
}
```

We will find that we can use `if / else if / else` as we've been used to in other languages.

### static

Any method that has the `static` keyword belongs to the class. What this means is that we won't have to make an instance of the class `Program` to be able to run a given method.

```cs
using System;

namespace HelloWorld 
{
    class Program 
    {
    
        static void Print1To255()
        {
            for(int i=0; i<256; i++)
            {
                Console.WriteLine(i);
            }
        }
  
        static void Main(string[] args)
        {
            Print1To255();
        }
    
    }
}
```

For now this will be a good way for us to structure our code. If we didn't include `static`, we would have to make an instance of `HelloWorld` in order to run `Print1To255()`.

```cs
HelloWorld hello1 = new HelloWorld();
hello1.Print1To255();
```
