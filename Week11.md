# My issue and review week 11

My Issue this week was creating a page for requests, e.g. food, fuel and other resources needed, these requests are dated and timed and able to be removed when complete and created automatically being set with a date/time

Using these two classes I create the request adding a date and time, this then gives the name, date and time to a function which adds it to the current requests.

Using good naming conventions makes this code very simple to understand, OnAddRequest click already describes that this is called when the button to add a request is clicked, OnFilterTextChanged again explains that the filtering system for the requests has been changed and this very simply updates tyhe list view to show the correct filtered requests and lastly, UpdateListView is to update the list checking the filter asked by the user and displaying any requests under this category. 

```
private void OnAddRequestClicked(object sender, EventArgs e)
    {
        var request = new Request
        {
            Description = DescriptionEntry.Text,
            Category = CategoryEntry.Text
        };

        _requests.Add(request);
        DescriptionEntry.Text = string.Empty;
        CategoryEntry.Text = string.Empty; // Clear the input field
        UpdateListView();
    }

    private void OnFilterTextChanged(object sender, TextChangedEventArgs e)
    {
        UpdateListView();
    }

    private void UpdateListView()
    {
        string filter = FilterEntry.Text ?? string.Empty;
        ListViewRequests.ItemsSource = _requests
            .Where(r => string.IsNullOrEmpty(filter) || r.Category.Contains(filter, StringComparison.OrdinalIgnoreCase))
            .ToList();
    }

}
```

Using the XAML I have made a filtering system as every request is put into a category which is set at the creation of the request, this means the requests can be filtered by category. here is the XAML: 
```
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Undac.LocalMediaAgencies"
             Title="Resource Requests">

    <VerticalStackLayout Spacing="15" Padding="10">

        <!-- Input Fields for Creating a Request -->
        <Entry x:Name="DescriptionEntry" Placeholder="Enter description"/>
        <Entry x:Name="CategoryEntry" Placeholder="Enter category (e.g., Food)"/>
        <Button Text="Add Request" Clicked="OnAddRequestClicked"/>

        <!-- Entry for Filtering -->
        <Entry x:Name="FilterEntry" Placeholder="Filter by category" TextChanged="OnFilterTextChanged"/>

        <!-- List of Requests -->
        <ListView x:Name="ListViewRequests">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Description}" Detail="{Binding Category}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>

    </VerticalStackLayout>
</ContentPage>
```

# Improvements after review

I was suggested to add error handling to my code so it doesnt just do nothing when the user does not fill in necissary boxes, here is my edited code to inprove error handling including comments on the new lines:

```
private void OnAddRequestClicked(object sender, EventArgs e)
{
    // Check if either Description or Category is empty
    if (string.IsNullOrWhiteSpace(DescriptionEntry.Text) || string.IsNullOrWhiteSpace(CategoryEntry.Text))
    {
        // Show an error message
        // Notify User of error made
        DisplayAlert("Error", "Please fill in both description and category.", "OK");
        return; // Return early to prevent adding the request
    }

    var request = new Request
    {
        Description = DescriptionEntry.Text,
        Category = CategoryEntry.Text
    };

    _requests.Add(request);
    DescriptionEntry.Text = string.Empty;
    CategoryEntry.Text = string.Empty;
    UpdateListView();
}
```



