#Week 12 issue and changes after review

##Issue: 

I chose to create the rota issue, I have created this relatively simply, it can create a rota name, location, assign people to each specific rota entry and then view each one seeing name, location and people assigned to the particular event. 

```
using System;
using Microsoft.Maui.Controls;

namespace Undac

{
    public partial class LocalMediaAgencies : ContentPage
    {
        // Assume _rotaManager is a service to manage rotas
        private List<Rota> _rotas = new List<Rota>();

        public LocalMediaAgencies()
        {
            InitializeComponent();
            RotaPicker.ItemsSource = GetRotaNames();
        }

        private void OnCreateRotaClicked(object sender, EventArgs e)
        {
            string rotaName = RotaNameEntry.Text;
            string rotaLocation = RotaLocationEntry.Text;

            if (string.IsNullOrWhiteSpace(rotaName) || string.IsNullOrWhiteSpace(rotaLocation))
            {
                DisplayAlert("Error", "Rota name and location are required.", "OK");
                return;
            }

            _rotas.Add(new Rota { Name = rotaName, Location = rotaLocation });
            RotaNameEntry.Text = string.Empty;
            RotaLocationEntry.Text = string.Empty;
            RotaPicker.ItemsSource = GetRotaNames(); // Refresh the picker
        }

        private void OnDiscontinueRotaClicked(object sender, EventArgs e)
        {
            string selectedRota = (string)RotaPicker.SelectedItem;
            if (selectedRota != null)
            {
                _rotas.RemoveAll(r => r.Name == selectedRota);
                RotaPicker.ItemsSource = GetRotaNames(); // Refresh the picker
            }
        }

        private async void OnManageAttendeesClicked(object sender, EventArgs e)
        {
            string selectedRotaName = (string)RotaPicker.SelectedItem;
            var selectedRota = _rotas.FirstOrDefault(r => r.Name == selectedRotaName);

            if (selectedRota != null)
            {
                string attendees = await DisplayPromptAsync("Manage Attendees",
                    $"Enter attendees for {selectedRota.Name} (comma-separated):",
                    initialValue: string.Join(", ", selectedRota.PeopleAttending),
                    maxLength: 500, keyboard: Keyboard.Text);

                if (!string.IsNullOrWhiteSpace(attendees))
                {
                    selectedRota.PeopleAttending = attendees.Split(',').Select(a => a.Trim()).ToList();
                }
            }
            else
            {
                await DisplayAlert("Error", "Please select a rota first.", "OK");
            }
        }

        
        private async void OnViewCalendarClicked(object sender, EventArgs e)
        {
            string rotaInfo = string.Join("\n", _rotas.Select(r =>
                $"Name: {r.Name}\nLocation: {r.Location}\nAttendees: {r.GetFormattedAttendees()}\n"));

            await DisplayAlert("Rota Details", rotaInfo, "OK");
        }

        private List<string> GetRotaNames()
        {
            return _rotas.Select(r => r.Name).ToList();
        }
    }

    public class Rota
    {
        public string Name { get; set; }
        public string Location { get; set; }
        public List<string> PeopleAttending { get; set; } = new List<string>();
    }

}

```

This code does as described having button click methods for viewing the created rotas and removing the created rota. To add members to cach rota you select it on the UI and then you can add poeple to that specific rota. 

The nameand location are added to each rota by the text boxes on the UI.

To remove each entry the removal is just done by selecting the name of the rota and using the remove button.

##Review


Naming conventions: The naming of variables and functions is good, they are easily understandable and explain what the variable is holding or function is doing.

Error handling: Errors handling is a little limited, it wont allow nothing to be in an inout box however rotas can be named the same and removing only one of these would not work, this could be fixed in creation of the rota or in the removal of rota. 

Input Validation: This is lacking as rota can be named the same, asignees names are just written in so spelling and grammar mistakes will happen with no checks on worng chatacters etc.








