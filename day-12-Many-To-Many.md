# Day 11 - One To Many

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

Setting up Many to Many relationships in MySQL requires that we use a `3rd` table to hold the foreign keys.<br>
Likewise we will need to create a `3rd` class and put it in our context file so that EntityFramework can make that connection.

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