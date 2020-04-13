# Day 5 - ASP.Net Core 

<img src="https://upload.wikimedia.org/wikipedia/commons/e/ee/.NET_Core_Logo.svg" alt="asp-dot-net core logo" height="250px" />

## dotnet new web

We're going to get started by running this command

```
dotnet new web --no-https -o HelloWorld
```

This will create a filestructure that looks like...

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

## Adding MVC

