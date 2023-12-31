# Week 5 entry incuding clean code examples

## Meaningful Names:
Class names are easy to understand being meaningful and descriptive with what they are doing. 

An example of this in my code from last week is the class name "Character" and methon name "LevelUp" are descriptive and explain what the class and method are doing. The class is dealing whith the character and the method LevelUp is called when the character is moviing to their next level to add more abilities.


## Keep Functions Small and Focused:
Keep your functions small and with a clear focus, split up any classes that are trying to do too much at once making it confusing and difficult to give it a meaningful class name.

An example of this is the LevelUp class, this class has one clear purpose meaning it has been cept small and focused. 


## Consistent Formatting:
Keeping your code structure consistent - indentation and spacing consistent and readable 

My code indentation has been kept consistent through the class and methods making it readable and easier to understand. All my methods in the class and the code inside these methods are indented to the same level metting consistent formatting.

## Encapsulation:
Encasulation helps keep data private within the class or methods it is needed with no risk of accidental changes. 

Access to my level field is restricted by the property Level. There is also vaidation to make sure there are no non-negative values before setting the level.  

## Defensive Programming:
This is to add validation, error handling and other issues that are not planned but could happen. It is to try make sure the program is prepared for miss inputs and errors.

My exapmple of this is the negative number check before setting levels. This is a for of input validation as there should be no negative values in level. 


## Organised Code:
This is to just make sure your code is readable and understandable, this includes: Consistent Formatting, Meaningful Names, Logical and Intuitive Structure.

My code meets all of these, using consistent formatting in all methods, my class and method names make sense and are focused and descriptive, the stuructire of my code makes sense as the methods are in order. 


## Here is the doxygen output for my code: 

![Doxygen](/Images/Doxygen.png?raw=true)

This output quite nicely shows the class and constructor name along with any functions and properties in the class. My class is kept nice and simple having a class which changes the characters level up by 1. There is a quick negative chack as the level should never be a negative and then the level is increased.

## Where I have eliminated the need for comments

My naming of classes and functions is good, it explains what the class is controlling and what each functions inension is. Also the naming of Level is good for understanding that in the class Character the Level must be that the character is increasing in level. Specifically the method name LevelUp explains exactly what the method is doing and no commentary is needed to explain this. 



