#Week 4 Portfolio

This portfolio entry is taking a badly structured class and improving it to a better coding standard. 

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

The errors with the code here is that Abilities is not initilised which may cause a NULL error as the class does not know what this is assigned to. Also the list has a private setter however it is still changeble outside of the class which could cause confusion and incorrect results if it is changes somewhere else in the program by mistake. 

And here is my changes i would make to the class

````
```
public class Character 
{
    private int level;
    public int Level 
    { 
        get { return level; }
        private set 
        {
            if (value >= 0)
                level = value;
        }
    }

    public Character()
    {
        Level = 1;
    }

    public void LevelUp() 
    {
        Level++;
    }
}
```
````


The changes I have made are Initilizing Abilities which was not done at all with can lead to an error when attempting to edit the list. I also have changed the abilities property from having a private setter to having a seperate mathod for adding abilities meaning there is no chance you could accidentally change the list without realising. As well as all the changes to make sure this run properly with less rsk if errors it is also much more easy and understandable with what is going on. It is much more redable and the class names are named in a way you can understand the purpose of it. 

