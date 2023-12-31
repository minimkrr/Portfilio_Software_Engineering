# Week 8 using team workflow and implementing a task

## Team Work Flow

Using the task board I chose to implement the list of media agencies. I have assigned to the task and moved to in development which allows the other group members to see I am currently working on this task.

## How I chose to implement this.

I have decided to use radio buttons with the options of "All, TV, Radio, Press".

This all works well currently just using a hard coded list. 

Using the label and filtering by the type of media I am able to display only these options. I chose to make my radio buttons in C# rather than XAML this time just due to wanting to do something different however doing it in XAML does make the C# page look at little neater. 

The task is now in review and will act on feedback once reviewed. 

Here is a part of my code for filtering the options


```
// Radio Buttons
var AllButton = new RadioButton { Content = "All" };
        var TVButton = new RadioButton { Content = "TV" };
        var PressButton = new RadioButton { Content = "Press" };
        var RadioButton = new RadioButton { Content = "Radio" };

```

```

        TVButton.CheckedChanged += (sender, e) =>
        {
            if (TVButton.IsChecked)
                resultLabel.Text = "Selected option: Show TV";
                resultLabel.Text = string.Join(Environment.NewLine, items.Where(item => item.Contains("TV")));
        };

        PressButton.CheckedChanged += (sender, e) =>
        {
            if (PressButton.IsChecked)
                resultLabel.Text = "Selected option: Show Press";
                resultLabel.Text = string.Join(Environment.NewLine, items.Where(item => item.Contains("Press")));
        };

        RadioButton.CheckedChanged += (sender, e) =>
        {
            if (RadioButton.IsChecked)
                resultLabel.Text = "Selected option: Show Radio";
            resultLabel.Text = string.Join(Environment.NewLine, items.Where(item => item.Contains("Radio")));
        };

        var stackLayout = new StackLayout
        {
            Children = { AllButton, TVButton, PressButton, RadioButton, resultLabel }
        };

        Content = stackLayout; 

    }
```

# Screenshots of filtering

![AllMedia](/Images/AllMedia.png?raw=true)

![TVMedia](/Images/TVMedia.png?raw=true)

![PressMedia](/Images/PressMedia.png?raw=true)

![RadioMedia](/Images/RadioMedia.png?raw=true)


