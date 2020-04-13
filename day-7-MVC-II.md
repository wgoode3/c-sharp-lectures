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
├ HelloWorld/
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
        ├ @_Layout.cshtml
    ├ @_ViewImports.cshtml
    ├ @_ViewStart.cshtml
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

