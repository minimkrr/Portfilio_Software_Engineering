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

# My testing

I decided the best testing for this code is to check a new test is added with the correct values and the text boxes clear after the button is pressed, here is my test I used:

```
[Fact]
    public void OnAddRequestClicked_AddsNewRequestAndClearsEntries()
    {
        // Arrange
        var viewModel = new RequestTest(); // Assuming your methods are in a ViewModel
        viewModel.DescriptionEntryText = "Test Description";
        viewModel.CategoryEntryText = "Test Category";
        viewModel._requests = new List<Request>(); // Initialize the requests list

        // Act
        viewModel.OnAddRequestClicked(null, null); // Calling the method

        // Assert
        Assert.Single(viewModel._requests); // Check if exactly one request is added
        var addedRequest = viewModel._requests.First();
        Assert.Equal("Test Description", addedRequest.Description);
        Assert.Equal("Test Category", addedRequest.Category);

        // Check if the text entries are cleared
        Assert.Empty(viewModel.DescriptionEntryText);
        Assert.Empty(viewModel.CategoryEntryText);
    }
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

I was also suggestsed to add Doxygen comments so here is a nicely commented version of my code using doxygen comments:

```
    /// \brief Holds the list of media requests.
    private List<Request> _requests = new List<Request>();

    /// \brief Initializes a new instance of the LocalMediaAgencies class.
    public LocalMediaAgencies()
    {
        InitializeComponent();
    }

    /// \brief Handles the Add Request button click event.
    /// \details Checks if the description and category fields are filled. If so, adds a new request to the list.
    /// \param sender The source of the event.
    /// \param e Contains the event data.
    private void OnAddRequestClicked(object sender, EventArgs e)
    {
        // Check if either Description or Category is empty
        if (string.IsNullOrWhiteSpace(DescriptionEntry.Text) || string.IsNullOrWhiteSpace(CategoryEntry.Text))
        {
            // Show an error message
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

    /// \brief Handles the Text Changed event of the filter entry.
    /// \param sender The source of the event.
    /// \param e Contains the event data.
    private void OnFilterTextChanged(object sender, TextChangedEventArgs e)
    {
        UpdateListView();
    }

    /// \brief Updates the list view based on the current filter.
    /// \details Filters the requests list based on the user's input in the filter entry and updates the UI.
    private void UpdateListView()
    {
        string filter = FilterEntry.Text ?? string.Empty;
        ListViewRequests.ItemsSource = _requests
            .Where(r => string.IsNullOrEmpty(filter) || r.Category.Contains(filter, StringComparison.OrdinalIgnoreCase))
            .ToList();
    }
}

/// \class Request
/// \brief Represents a request with a description and category.
public class Request
{
    /// \brief Gets or sets the description of the request.
    public string Description { get; set; }

    /// \brief Gets or sets the category of the request.
    public string Category { get; set; }
}
```

# Reviewing Code

The code i reviewed had good naming conventions, all was easy to read. There were no comments to help with understanding what was going on without having to read the full file. There was no validation ot error handling on their inputs. These were the pnly main issues as coding conventions were all nicely done and the code worked as intended.

My suggestions where to add some error handling and validation along with comments. 


