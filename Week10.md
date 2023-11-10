# Week 10 New issue and review

For my issue this week I made an operational status page. I am able to create, view all and remove the entries. 

To save each entry I have used a list, here is the initial of the list:

```
List<(string Name, string Status, DateTime Date)> operationRecords = new List<(string Name, string Status, DateTime Date)>();
```

I have then used OnCLick functions to add and remove entries from this list. 

Here is the section of code creating the new entry: 

```
operationRecords.Add((operationName, $"{status} - {date.ToString("yyyy-MM-dd HH:mm:ss")}", date));
```
I have error checking for an entry with no name giving an error message to fill in name of entry before it will be created. 

The entries are shown with the name, time and date of creation and if the entry is updated the date and time will change to be the most recent edit of the entry. 


