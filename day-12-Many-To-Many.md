# Day 11 - One To Many

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

Setting up Many to Many relationships in MySQL requires that we use a `3rd` table to hold the foreign keys.<br>
Likewise we will need to create a `3rd` class and put it in our context file so that EntityFramework can make that connection.

#### User.cs
```cs
namespace NinjaVillage
{
    public class Ninja
    {
        [Key]
        public int NinjaId { get; set; }

        [Required]
        public string Name { get; set; }

        [Required]
        public string Weapon { get; set; }

        [Required]
        public string BeltColor { get; set; }

        public DateTime CreatedAt { get; set; }

        public DateTime UpdatedAt { get; set; }

        //NOT stored in Database
        public List<Association> Visited { get; set; }

    }
}
```

#### Dojo.cs

```cs
namespace NinjaVillage
{
    public class Village
    {
        [Key]
        public int VillageId { get; set; }

        public string Name { get; set; }

        public string Location { get; set; }

        public List<Association> Vistors { get; set; }
    }
}

```

```cs
namespace NinjaVillage
{
    public class Association
    {
        [Key]
        public int AssociationId { get; set; }

        public int NinjaId { get; set; }
        
        public int Village { get; set; }
    }
}
```