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

The main methods i used were: 

```
private void OnRecordOperationStatusClicked(object sender, EventArgs e)
    {
        string operationName = OperationNameEntry.Text;

        if (string.IsNullOrWhiteSpace(operationName))
        {
            DisplayAlert("Error", "Please enter an operation name.", "OK");
            return;
        }

        string status = "Operation completed";
        DateTime date = DateTime.Now;

        var existingRecord = operationRecords.FirstOrDefault(record => record.Name == operationName);

        if (existingRecord.Name == operationName)
        {
            // If the record already exists, update it
            operationRecords.Remove(existingRecord);
        }

        operationRecords.Add((operationName, $"{status} - {date.ToString("yyyy-MM-dd HH:mm:ss")}", date));

        OperationNameEntry.Text = string.Empty;
        DisplayAlert("Operation Status Recorded", "Operation status recorded and saved.", "OK");
    }
```

This method is activated when the button to create record is clicked and finds the currect date and time along with the taking the name out of the name text box. It then saves the record and displayes a completed message. Also there is an error handle insuring the name box is filled.


The other main method is the remove, 

```
private void OnRemoveOperationRecordClicked(object sender, EventArgs e)
    {
        string operationName = OperationNameEntry.Text;

        if (string.IsNullOrWhiteSpace(operationName))
        {
            DisplayAlert("Error", "Please enter an operation name to remove.", "OK");
            return;
        }

        var existingRecord = operationRecords.FirstOrDefault(record => record.Name == operationName);
        if (existingRecord.Name == operationName)
        {
            operationRecords.Remove(existingRecord);
            OperationNameEntry.Text = string.Empty;
            DisplayAlert("Record Removed", $"Record for '{operationName}' has been removed.", "OK");
        }
        else
        {
            DisplayAlert("Error", $"Record with name '{operationName}' not found.", "OK");
        }
```

This again has an error handle making sure the box is filled as you can not delete nothing, It will check current records with the same name as you have specified to delete. If this is found then it will be removed and a message will come up confirming this has worked, again the error handle for this is to say that the record was not found. 

# Review by member of team

Main thing i forgot was to add comments, adding doxygen comments would helo to understand what is going on much faster, here are the same two classes after including some comments:

```
/// <summary>
        /// Event handler for the "Record Operation Status" button click.
        /// Records the status of an operation and saves it to the list of operation records.
        /// </summary>
        /// <param name="sender">The event sender.</param>
        /// <param name="e">The event arguments.</param>
        private void OnRecordOperationStatusClicked(object sender, EventArgs e)
        {
            string operationName = OperationNameEntry.Text;

            if (string.IsNullOrWhiteSpace(operationName))
            {
                DisplayAlert("Error", "Please enter an operation name.", "OK");
                return;
            }

            string status = "Operation completed";
            DateTime date = DateTime.Now;

            var existingRecord = operationRecords.FirstOrDefault(record => record.Name == operationName);

            if (existingRecord.Name == operationName)
            {
                // If the record already exists, update it
                operationRecords.Remove(existingRecord);
            }

            operationRecords.Add((operationName, $"{status} - {date.ToString("yyyy-MM-dd HH:mm:ss")}", date));

            OperationNameEntry.Text = string.Empty;
            DisplayAlert("Operation Status Recorded", "Operation status recorded and saved.", "OK");
        }

```


```
/// <summary>
        /// Event handler for the "Remove Operation Record" button click.
        /// Removes an operation record based on the provided operation name.
        /// </summary>
        /// <param name="sender">The event sender.</param>
        /// <param name="e">The event arguments.</param>
        private void OnRemoveOperationRecordClicked(object sender, EventArgs e)
        {
            string operationName = OperationNameEntry.Text;

            if (string.IsNullOrWhiteSpace(operationName))
            {
                DisplayAlert("Error", "Please enter an operation name to remove.", "OK");
                return;
            }

            var existingRecord = operationRecords.FirstOrDefault(record => record.Name == operationName);
            if (existingRecord.Name == operationName)
            {
                operationRecords.Remove(existingRecord);
                OperationNameEntry.Text = string.Empty;
                DisplayAlert("Record Removed", $"Record for '{operationName}' has been removed.", "OK");
            }
            else
            {
                DisplayAlert("Error", $"Record with name '{operationName}' not found.", "OK");
            }
        }
```


