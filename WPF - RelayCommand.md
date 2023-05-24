## Relay Command
In this example, we will create a UI that allows us to add, delete, and update an Item.
First, we need to create a class `RelayCommand`:
RelayCommand.cs
```
using System;
using System.Windows.Input;

namespace Project_Name
{
    internal class RelayCommand : ICommand
    {
        private readonly Action<object> _execute;
        private readonly Func<object, bool> _canExecute;

        public event EventHandler CanExecuteChanged
        {
            add { CommandManager.RequerySuggested += value; }
            remove { CommandManager.RequerySuggested -= value; }
        }

        public RelayCommand(Action<object> execute, Func<object, bool> canExecute = null)
        {
            _execute = execute;
            _canExecute = canExecute;
        }

        public bool CanExecute(object parameter) => _canExecute == null || _canExecute(parameter);

        public void Execute(object parameter) => _execute(parameter);
    }
}
```

Next, inside of the code behind, we create RelayCommand object for each action.
`canExecute => { return true; }` can be removed from the `AddCommand` if it's always true.
`canExecute => SelectedItem != null` is the condition for `DeleteCommand`. Specifically, if there is no SelectedItem, the command won't be executed
```
public RelayCommand AddCommand => new RelayCommand(execute => AddItem(), canExecute => { return true; });
public RelayCommand DeleteCommand => new RelayCommand(execute => DeleteItem(), canExecute => SelectedItem != null);
public RelayCommand SaveCommand => new RelayCommand(execute => SaveItem(), canExecute => CanSave());

private void AddItem()
{
    // Add item to the existing list
}

private void RemoveItem()
{
    // Remove item to the existing list
}

private void SaveItem()
{
    // Save item to the existing list
}


private void CanSave()
{
    return true; // or false based on some condition
}
```

Xaml file:
```
<Button Command={Binding AddCommand}>Add</Button>
<Button Command={Binding DeleteCommand}>Delete</Button>
<Button Command={Binding SaveCommand}>Save</Button>
```
