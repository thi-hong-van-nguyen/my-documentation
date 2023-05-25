## Create Global Variables

### 1. Create a class to hold your global variable and implement the INotifyPropertyChanged interface to enable dynamic UI updates when the variable changes. For example:
```
public class GlobalData : INotifyPropertyChanged
{
    private string _myVariable;

    public string MyVariable
    {
        get { return _myVariable; }
        set
        {
            _myVariable = value;
            OnPropertyChanged(nameof(MyVariable));
        }
    }

    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
```

### 2. Instantiate the GlobalData class in your App.xaml.cs file so that it becomes globally accessible. Add a property to retrieve the instance of the GlobalData class. For example:
```
public partial class App : Application
{
    public static GlobalData GlobalData { get; } = new GlobalData();
}
```

### 3. In your view models or code-behind files, you can access and update the global variable using App.GlobalData.MyVariable. For example:
```
// Get the value
string variableValue = App.GlobalData.MyVariable;

// Set the value
App.GlobalData.MyVariable = "New value";
```

### 4. In your XAML, you can bind the UI elements to the global variable using the Binding markup extension. For example:
```
<Window x:Class="YourNamespace.YourWindow"        
        xmlns:local="clr-namespace:YourNamespace">
    <TextBlock Text="{Binding Source={x:Static local:App.GlobalData}, Path=MyVariable}" />
</Window>
```
