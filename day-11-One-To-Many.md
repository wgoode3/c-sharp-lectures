# Day 11 - One To Many

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

## The Set Up

Remember that if we want to be able to relate one table to another we need to enable the use of Primary Keys and Foreign Keys.<br>
<br>
We have already been using PKs in the set up of our models, now we are going to start adding in FKs.

*For our site Trading Bronies*
A User can have many Bronies, but a Brony can only have one User(Owner).

#### User.cs
```cs
namespace TradingBronies
{
    public class User
    {
        [Key]
        public int UserId { get; set; }

        [Required]
        public string Name { get; set; }

        [Required]
        [EmailAddress]
        public string Email { get; set; }

        [Required]
        [DataType(DataType.Password)]
        public string Password { get; set; }

        public DateTime CreatedAt { get; set; }

        public DateTime UpdatedAt { get; set; }

        //NOT stored in Database
        public List<Brony> MyLittleBronies { get; set; }

    }
}
```
Notice that we have a list of brony that the user holds.  It's important to know that this list is not stored in the database.

```cs
namespace TradingBronies
{
    public class Brony
    {
        [Key]
        public int BronyId { get; set; }

        [Required]
        public string Name { get; set; }

        [Required]
        public string Color { get; set; }

        [Required]
        public string Condition { get; set; }

        [Required]
        public decimal Price {  get; set; }

        public DateTime CreatedAt { get; set; }

        public DateTime UpdatedAt { get; set; }

        public int UserId { get; set; }

        //NOT stored in database
        public User Owner {  get; set;}
    }
}
```
Since a Brony can have only one user, the foreign key must live in it's class.<br>
`public User Owner { get; set; }` && `public List<Brony> MyLittleBronies { get; set; }` are known as Navigational Properties.