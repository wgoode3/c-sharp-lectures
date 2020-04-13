# Day 5 - ASP.Net Core 

<img src="https://upload.wikimedia.org/wikipedia/commons/e/ee/.NET_Core_Logo.svg" alt="asp-dot-net core logo" height="250px" />

## dotnet new web

We're going to get started by running this command

```
dotnet new web --no-https -o HelloWorld
```

This will create a file structure that looks like...

```
├ HelloWorld/
  ├ bin/
  ├ obj/
  ├ Properties/
  ├ appsettings.Development.json
  ├ appsettings.json
  ├ HelloWorld.csproj
  ├ Program.cs
  ├ Startup.cs
```

These files are mostly familiar to us from when we were using `dotnet new console`, but there is one notable addition...

## Startup.cs

There is a lot going on in this file and we will be modifying this file quite a bit.

### public void Configure()

```cs
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
```

This method will be run when we start the project, and the first conditional is checking something from a `IHostingEnvironment`. This will check if the environment where the project is being run is set to "development" if not the project will suppress detailed error messages like we'll want it to when deployed. 

**Note:** We only need to set this variable once, and we can do it like so...

| Windows CMD                               |  MacOS / BASH                               |
|-------------------------------------------|---------------------------------------------|
| `setx ASPNETCORE_ENVIRONMENT Development` | `export ASPNETCORE_ENVIRONMENT=Development` |

The next part of the configure method will be something we need to rewrite...

```cs
app.Run(async (context) =>
{
    await context.Response.WriteAsync("Hello World!");
});
```

We'll talk about C# lamba functions `=>` in more depth later on, but this is a *callback function* that returns the string "Hello World!" to any request that our server receives.

### Running our project

We can run our project with `dotnet watch run` which will then be accessible on `http://localhost:5000/`.

## Adding MVC

First up we need to modify the `ConfigureServices` method...

```cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
}
```

Then we go to the ```Configure``` method and replace the ```app.Run()``` we saw previously with...

```cs
app.UseMvc();
```

Essentially all we need here is the following...

```cs
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseMvc();
}
```

## Putting the "C" in MVC

Start out by creating a folder called `Controllers` and inside of it create a file called `HomeController.cs`.

```
├ HelloWorld/
  ├ bin/
  ├ Controllers/           <--- this folder is new
    ├ HomeController.cs    <--- this file is new
  ├ obj/
  ├ Properties/
  ├ appsettings.Development.json
  ├ appsettings.json
  ├ HelloWorld.csproj
  ├ Program.cs
  ├ Startup.cs
```

And inside of the `HomeController.cs` file we're going to add in the following...

```cs
using Microsoft.AspNetCore.Mvc;

namespace HelloWorld.Controllers     
{
    public class HomeController : Controller   
    {
        [HttpGet("")]
        public string Index()
        {
            return "Hello World from HomeController!";
        }
    }
}
```

This will create a controller that has one route set up, when a user makes a `GET` request to `http://localhost:5000/` it will run this `Index` method and return the string "Hello World from HomeController!". We can control each route by using C# attributes `[HttpGet("")]` right above the method we want to run when we receive a request to that route.

## Putting the "V" in MVC

To get started using views, we need to add some folders...

```
├ HelloWorld/
  ├ bin/
  ├ Controllers/           
    ├ HomeController.cs    
  ├ obj/
  ├ Properties/
  ├ Views/                          <--- this folder is new
    ├ Home/                         <--- this folder is new
      ├ Index.cshtml                <--- this file is new
  ├ appsettings.Development.json
  ├ appsettings.json
  ├ HelloWorld.csproj
  ├ Program.cs
  ├ Startup.cs
```

Inside of the `Index.cshtml` we'll want to paste in the following...

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>This is the Index view!</h1>
</body>
</html>
```

And if we want our `Index` method we have written previously to host this file we can change it like so...

```cs
[HttpGet("")]     
public IActionResult Index()
{
    return View();
}
```

### CSHTML

We can write all sorts of C# code inside of these files...

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>This is still the Index view!</h1>
    @{
        List<string> Names = new List<String>(){
            "Adrien", "Anne", "Benny", "Chris", "Daisy", "Phil", "Saurabh", "Will"
        };
        <ul>
            @foreach(var name in Names)
            {
                if(name == "Benny")
                {
                    <li style="color:red;">@name</li>
                }
                else
                {
                    <li>@name</li>
                }
            }
        </ul>
    }
</body>
</html>
```

This file will be read by the `Razor` templating and display a list of names highlighting `Benny` in red text. `Razor` is a pretty awesome thing to use because we can nest C# inside HTML inside C# as much as we want. The important thing to note, is that whenever we go from writing HTML to C# we have to use an `@`.  
