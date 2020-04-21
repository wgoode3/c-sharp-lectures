# Day 11 - One To Many

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

Setting up Many to Many relationships in MySQL requires that we use a `3rd` table to hold the foreign keys.<br>
Likewise we will need to create a `3rd` class and put it in our context file so that EntityFramework can make that connection.

#### Crab.cs

```cs
namespace SpaceCrabs
{
    public class Crab
    {
        [Key]
        public int CrabId { get; set; }

        [Required]
        public string Name { get; set; }

        [Required]
        public string Weapon { get; set; }

        [Required]
        public string SpaceCraft { get; set; }

        public DateTime CreatedAt { get; set; }

        public DateTime UpdatedAt { get; set; }

        //NOT stored in Database
        public List<Association> VisitedPlanets { get; set; }

    }
}
```

#### Planet.cs

```cs
namespace SpaceCrabs
{
    public class Planet
    {
        [Key]
        public int PlanetId { get; set; }

        [Required]
        public string Name { get; set; }

        [Required]
        public string System { get; set; }

        [Required]
        public string Galaxy { get; set; }

        //NOT stored in Database
        public List<Association> Vistors { get; set; }
    }
}

```

#### Association.cs

```cs
namespace SpaceCrabs
{
    public class Association
    {
        [Key]
        public int AssociationId { get; set; }

        public int CrabId { get; set; }

        public int PlantId { get; set; }

        //NOT stored in Database
        public Crab SpaceCrab { get; set; }

        //NOT stored in Database
        public Planet Planet { get; set; }
    }
}
```

#### MyContext.cs

```cs
namespace TradingBronies
{
    public class MyContext : DbContext
    {
        public MyContext(DbContextOptions options) : base(options){}

        public DbSet<Crab> Crabs { get; set; }

        public DbSet<Planet> Planets { get; set; }

        public DbSet<Association> Associations { get; set; }
    }
}
```

### Enter `.ThenInclude()` 

#### HomeController.cs

```cs
namespace SpaceCrabs
{
    public class HomeController : Controller
    {
        private MyContext _context;
        public HomeController(MyContext context)
        {
            _context = context;
        } 

        [HttpGet("")]
        public IActionResult Index()
        {
            // This will give us a list of all the crabs with the list of associated planets 
            List<Planet> Planets = _context.Planets.Include( p => p.Visitors )
                                            .ThenInclude( a => a.SpaceCrab )
                                            .ToList();
            return View(Planets);
        }

        [HttpGet("crabs")]
        public IActionResult Profile(int userId)
        {
            List<Crab> Crabs = _context.Crabs.Include( c => c.VisitedPlanets )
                                            .ThenInclude( a => a.Planet )
                                            .ToList();

            return View(profile);
        }

    }
}
```