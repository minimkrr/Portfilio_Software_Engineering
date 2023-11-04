# Week 9 continuing creating next issue

## Team Workflow

Again this week i chose a task from te task board and moved to In Development assinged to myself

My task is to create security alerts that can be created and when completed can be marked as resolved. 

## My Task

I have created a page which a security alert can be created and these are saved when the app is stopped running so they dont disapear between runs of the progran. Also there is a resolve button next to each security issue which when pressed removes the issue from the list.

To do this I have made the button for create entry to add the text in the input box to a string called "savedEntries" and when the resolved button is clicked this entry is searched for in the list and removed.

```
 ObservableCollection<string> entries;

    public Security()
    {
        InitializeComponent();

        string savedEntries = Preferences.Get("Entries", string.Empty);

        if (!string.IsNullOrEmpty(savedEntries))
        {
            var savedEntriesList = savedEntries.Split(';').ToList();
            entries = new ObservableCollection<string>(savedEntriesList);
        }
        else
        {
            entries = new ObservableCollection<string>();
        }

        entryList.ItemsSource = entries;
    }

    private void OnAddEntryClicked(object sender, EventArgs e)
    {
        if (!string.IsNullOrWhiteSpace(entry.Text))
        {
            entries.Add(entry.Text);
            entry.Text = string.Empty;

            SaveEntries();
        }
    }

    private void OnDeleteClicked(object sender, EventArgs e)
    {
        if (sender is Button button && button.CommandParameter is string entryToDelete)
        {
            entries.Remove(entryToDelete);
            SaveEntries();
        }
    }

    private void SaveEntries()
    {
        var entriesToSave = string.Join(";", entries);
        Preferences.Set("Entries", entriesToSave);
    }
```
 As you can see from the code above, I have used a list to save each entry, My onAddEntryClick has a quick error check of the button does not work with the text box being blank. If the box it not blank the entry will be added to the string and the SaveEntries method will add this to the string. To delete an issue I have another on click command called OnDeleteClicked, this will delete the specific entry that the button is for and not the other entries. 

 ```
<StackLayout>
        <Entry x:Name="entry" Placeholder="Enter Security Risk" />
        <Button Text="Add Entry" Clicked="OnAddEntryClicked" />
        <ListView x:Name="entryList">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <ViewCell>
                        <StackLayout Orientation="Horizontal">
                            <Label Text="{Binding}" VerticalOptions="Center" />
                            <Button Text="Reolved" CommandParameter="{Binding .}" Clicked="OnDeleteClicked" />
                        </StackLayout>
                    </ViewCell>
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </StackLayout>
```

For my XAML I have used an entry bix and button for creating the Secutity Risk and another button by each label for deleting. The lables are used to show each Security Risk.

## Screenshots

![blankSecurity](/Images/blankSecurity.png?raw=true)

![filledSecurity](/Images/filledSecurity.png?raw=true)
