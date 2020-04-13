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
<br>
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

We no longer need to use the head tag in our view files, because our _Layout.cshtml will contain it, and we will be injecting all our views into the body when `@RenderBody()` is called.

## ViewModels

A ViewModel is a way that we can keep the strict type going in our template files. But there are some guidelines to them:
<ul>
    <li>Must define them at the top of the razor file.</li>
    <li>There can be only one ViewModel.</li>
<ul>
<br>

We can even use models that we write in our project and use them in our templates.<br>
This is how we can tie a model to a form to create an object.

### User.cs
```cs
namespace MyCoolProject
{
    public class User
    {
        [Required(ErrorMessage="Name is required.")]
        public string Name {get; set;}

        [Required(ErrorMessage="Email is required.")]
        [EmailAddress]
        public string Email {get; set;}
    }
}
```

We can add validations to our Models with the bracket syntax.

### Index.cshtml
```html
@model User
 <form asp-action="Process" method="post" >
    <span asp-validation-for="Name"></span>
    <input asp-for="Name" >
    <span asp-validation-for="Email"></span>
    <input asp-for="Email">
    <input type="submit" value="Create" >
 </form>
```

With tag helpers we can bind our models or ViewModels to our forms.<br>
`asp-for="Name"` ties User.Name to the input.<br>
`asp-validation-for="Name"` ties the validation method to the form as well.

### HomeController.cs

```cs
    public class HomeController : Controller
    {
        [HttpPost("process")]
        public IActionResult Process(User newUser)
        {
            if(ModelState.IsValid)
            {
                return Redirect("/dashboard");
            }
            else
            {
                return View("Index");
            }
        }
    }
```

We now pass the model reference type into the parameters of the post method, and can validate it like so.<br>
If the ModelState isn't valid we can just re-render the form page.

## SESSION

### TRY TO SAY SESSION 5 TIMES FAST.

We use session to store variables on our browser.  We can use it to keep track of a user that is logged into our site.

### THE SETUP:

```cs
using Microsoft.AspNetCore.Http;

namespace MyCoolProject
{
    public class HomeController : Controller
    {
        [HttpGet("")]
        public IActionResult Index()
        {
            // SETS AN INTEGER INTO SESSION CALLED 'COUNT'
            HttpContext.Session.SetInt32("Count", 1);

            // SETS A STRING INTO SESSION CALLED 'NAME'
            HttpContext.Session.SetString("Name","Benny Bob");

            return View();
        }

        [HttpGet("another")]
        public IActionResult Another()
        {
            // GETS 'COUNT' OUT OF SESSION, MODIFIES IT, AND PUTS IT BACK IN.
            int? count = HttpContext.Session.GetInt32("Count");
            count ++;
            HttpContext = HttpContext.Session.SetInt32("Count",(int)count);
        }
    }
}
```
