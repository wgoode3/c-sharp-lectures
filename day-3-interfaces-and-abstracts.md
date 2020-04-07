# Day 3 - C# Interfaces and Abstracts

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/C_Sharp_logo.svg/800px-C_Sharp_logo.svg.png" alt="c#" width="200px" />

## Abstract Class

what if we never want to make an instance of our base class?

## Interface

what if we want to guarantee unrelated classes can be used the same way?


## Abstracts vs Interfaces

<img src="https://raw.githubusercontent.com/wgoode3/c-sharp-lectures/master/assets/abstracts-interfaces.png" alt="diagram" />

```cs
// Drink.cs

namespace Beverage {

    public abstract class Drink
    {
    
        public string Color {get;set;}
        public bool IsCarbonated {get;set;}
        public double Temperature {get;set;}
    
    
        /// <summary>
        /// Drinks need to have color, isCarbonated, and a temperature
        /// </summary>
        public Drink (string color, bool isCarbonated, double temperature)
        {
            Color = color;
            IsCarbonated = isCarbonated;
            Temperature = temperature;
        }
        
        /// <summary>
        /// The way we consume the drink will vary based on temerature
        /// </summary>
        public virtual void Consume ()
        {
            // I'll assume we're using Celsius here
            temperature < 40 ? Console.WriteLine("Glug glug...") : Console.WriteLine("Sip sip...");
        }
    
    }
}

```
