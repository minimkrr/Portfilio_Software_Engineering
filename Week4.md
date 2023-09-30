#Week 4 Portfolio


Here is the original code:

````
```
public class Character 
{
    public int Level { get; private set; }
    public List<SpecialAbilities> Abilities { get; private set; }

    public void LevelUp() 
    {
        Level++;
    }
}

```
````

And here is my changes i would make to the class

````
```
public class Character 
{
    public int Level { get; private set; }
    public List<SpecialAbilities> Abilities { get; private set; }

    public Character()
    {
        Abilities = new List<SpecialAbilities>();
    }

    public void LevelUp() 
    {
        Level++;
    }
}
```
````
