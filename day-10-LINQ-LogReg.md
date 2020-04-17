# Day 10 - LINQ & LoginReg

<img src="https://miro.medium.com/max/480/1*SnZqHENpIMiEKsg999Q0DQ.png" alt="ef-core" />

## LoginReg

In order to have a successful Login & Registration we need to validate both a Register Form and a Login Form.<br>
<br>
We do so by creating two different models: `User.cs` && `LoginUser.cs`

#### User.cs
This model will get put into our database.

```cs
    namespace LoginReg.Models
    {
        public class User
        {
            [Key]
            public int UserId { get; set; }

            [Required]
            public string FirstName {get;set;}

            [Required]
            public string LastName {get;set;}

            [EmailAddress]
            [Required]
            public string Email {get;set;}

            [DataType(DataType.Password)]
            [Required]
            [MinLength(8, ErrorMessage="Password must be 8 characters or longer!")]
            public string Password {get;set;}

            public DateTime CreatedAt {get;set;} = DateTime.Now;
            public DateTime UpdatedAt {get;set;} = DateTime.Now;

            // We us the NotMapped Annotation so that this variable doesn't end up in our database.
            [NotMapped]
            [Compare("Password")]
            [DataType(DataType.Password)]
            public string Confirm {get;set;}
        }
    }
```
#### LoginUser.cs
This model will not get put into our database.

```cs

    namespace LoginReg.Models
    {
        public class LoginUser
        {
            [Required]
            [EmailAddress]
            public string LoginEmail { get; set; }

            [DataType(DataType.Password)]
            [Required]
            public string LoginPassword {get;set;}
        }
    }
```

### Hashing Passwords

In order to hash a password we must import Identity from AspNetCore.
`using Microsoft.AspNetCore.Identity;`

Then we can hash passwords like so:

#### Somewhere in your HomeController.cs

```cs
    [HttpPost("register")]
    public IActionResult Register(User reg)
    {
        //These two lines will hash our password for us.
        PasswordHasher<User> Hasher = new PasswordHasher<User>();
        reg.Password = Hasher.HashPassword(reg, reg.Password);
    }

    [HttpPost("login")]
    publc IActionResult Login(LoginUser log)
    {

        //These two lines will compare our hashed passwords.
        var hash = new PasswordHasher<LoginUser>();
        var result = hash.VerifyHashedPassword(log, userInDb.Password, log.LoginPassword);
        //Result will either be 0 or 1.
        if(result == 0)
        {
            //Handle rejection and send them back to the form.
        } 

    }
```

## LINQ

<img src="https://www.zelda.com/links-awakening/assets/img/home/hero-char.png" alt="Link" width="400px">

<em>The Hero of (saving) Time</em>

LINQ is an acronym for Language Integrated Query

We can use LINQ with any type of dataset or SQL database.<br>
There are two notations of LINQ `Method` and `Query`<br>
<br>
We will be focusing on the Method Notation.

#### Lambda Expressions

<img src="https://res.cloudinary.com/teepublic/image/private/s--QH6eyKSY--/c_fit,g_north_west,h_840,w_837/co_000000,e_outline:40/co_000000,e_outline:inner_fill:1/co_ffffff,e_outline:40/co_ffffff,e_outline:inner_fill:1/co_bbbbbb,e_outline:3:1000/c_mpad,g_center,h_1260,w_1260/b_rgb:eeeeee/c_limit,f_jpg,h_630,q_90,w_630/v1582915404/production/designs/8222015_0.jpg" alt="Lambda" width="400px">

Lambda Expressions are a way we can simplify a function into one line.<br>
We use the `=>` to express a function returning something.<br>
<br>
Now we can use these expressions to query our database for the things we want to display on our page.

`_context.Users.FirstOrDefault( u => u.UserId == userId);` will return the first user that it finds in the database.<br>

There are methods for filtering, sorting, and general purpose.

#### Filtering
<ol>
    <li>FirstOrDefault</li>
    <li>Where</li>
    <li>Select</li>
</ol>

#### Sorting
<ol>
    <li>OrderBy</li>
    <li>OrderByDescending</li>
    <li>ThenBy</li>
    <li>ThenByDescending</li>
</ol>

#### General Purpose
<ol>
    <li>Min</li>
    <li>Max</li>
    <li>Take</li>
    <li>ToList</li>
</ol>
