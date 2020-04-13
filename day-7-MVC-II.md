# Day 3 - C# MVC - Part Deux

<img src="https://upload.wikimedia.org/wikipedia/commons/e/ee/.NET_Core_Logo.svg" alt="asp-dot-net core logo" height="250px" />

## dotnet new mvc

By now, we should all have had practice with the web application in asp.net core.<br>
From now on, we will be using a more robust application called mvc, and we create one by the following command.

```
dotnet new mvc --no-https -o MyCoolSite
```

We will get a project that looks something like this . . .

```
├ MyCoolSite/
  ├ bin/
  ├ obj/
  ├ Controllers/
    ├ HomeController.cs
  ├ Models/
  ├ Properties/
  ├ Views/
    ├ Home/
        ├ Index.cshtml
    ├ Shared/
        ├ _Layout.cshtml
    ├ _ViewImports.cshtml
    ├ _ViewStart.cshtml
  ├ wwwroot
    ├ css
    ├ images
    ├ js
    ├ lib
  ├ appsettings.Development.json
  ├ appsettings.json
  ├ MyCoolProject.csproj
  ├ Program.cs
  ├ Startup.cs
```

This is considerably more than the web application!!!<br>
Let's take a look into the Layout file can look like after some trimming...

<img src="https://github.com/wgoode3/c-sharp-lectures/blob/master/assets/Screen%20Shot%202020-04-13%20at%201.37.11%20PM.png" alt="asp-dot-net core logo" height="600px" />
