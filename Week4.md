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
    private List<SpecialAbilities> Abilities { get; set; }

    public Char()
    {
        Abilities = new List<SpecialAbilities>();
    }

    public void NewAbility(SpecialAbilities ability)
    {
        Abilities.Add(ability);
    }

    public void LevelUp() 
    {
        Level++;
    }
}
```
````


The changes I have made are Initilizing Abilities which was not done at all with can lead to an error when attempting to edit the list. I also have changed the abilities property from having a private setter to having a seperate mathod for adding abilities meaning there is no chance you could accidentally change the list without realising

