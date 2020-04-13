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
*SIDE NOTE: This is where we link our css files!!!*<br>
Here are the things we trimmed:

```
    <header>
        <nav class="navbar navbar-expand-sm navbar-toggleable-sm navbar-light bg-white border-bottom box-shadow mb-3">
            <div class="container">
                <a class="navbar-brand" asp-area="" asp-controller="Home" asp-action="Index">MyCoolProject</a>
                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target=".navbar-collapse" aria-controls="navbarSupportedContent"
                        aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="navbar-collapse collapse d-sm-inline-flex flex-sm-row-reverse">
                    <ul class="navbar-nav flex-grow-1">
                        <li class="nav-item">
                            <a class="nav-link text-dark" asp-area="" asp-controller="Home" asp-action="Index">Home</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link text-dark" asp-area="" asp-controller="Home" asp-action="Privacy">Privacy</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </header>
```
```
    <partial name="_CookieConsentPartial" />
```
```
    <footer class="border-top footer text-muted">
        <div class="container">
            &copy; 2020 - MyCoolProject - <a asp-area="" asp-controller="Home" asp-action="Privacy">Privacy</a>
        </div>
    </footer>
```
