# Day 10 - LINQ & LoginReg

<img src="https://miro.medium.com/max/480/1*SnZqHENpIMiEKsg999Q0DQ.png" alt="ef-core" />

## LoginReg

In order to have a successfull Login & Registration we need to validate both a Register Form and a Login Form.<br>
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

