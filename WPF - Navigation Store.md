## Navigation Store

Assume we have two views: Login and Home and we want to navigate between them by clicking on a button:
`Login.xaml`:
```
<StackPanel>
// Textbox for Username & Password
    <Button Command="{Binding LoginCommand}" Content="LOGIN"/>
</StackPanel>
```

`Home.xaml`:
```
<Button Command="{Binding LogoutCommand}" Content="LOGOUT"/>
```

First, we create `NavigationStore.cs`:
```
using System;

namespace ProjectName.folderName
{
    public class NavigationStore
    {
        public event Action CurrentVMChanged;

        private ViewModelBase _currentVM;

        public ViewModelBase CurrentVM
        {
            get { return _currentVM; }
            set { _currentVM = value; OnCurrentVMChanged(); }
        }

        private void OnCurrentVMChanged()
        {
            CurrentVMChanged?.Invoke();
        }
    }
}
```
The `NavigationStore` class provides a mechanism to store & notify changes to the current View Model. It allows other components in the application to subscribe to the `CurrentVMChanged` event and react accordingly when the current View Model is updated.

Next, we create the commands for Login and Logout
`LoginCommand`:
```
public class LoginCommand : CommandBase
    {
        private readonly NavigationStore _navigationStore;

        public LogoutCommand(NavigationStore navigationStore)
        {
            _navigationStore = navigationStore;
        }

        public override void Execute(object parameter)
        {
            _navigationStore.CurrentVM = new HomeVM(_navigationStore);
        }
    }
```
 the `Loginommand` class is responsible for executing the login operation in the application. When the Execute method is called, it updates the current view model in the provided NavigationStore instance to a new instance of the HomeVM view model, indicating a transition to the Home view.
 
 Similarly, we have `LogoutCommand.cs`:
 ```
 public class LogoutCommand : CommandBase
    {
        private readonly NavigationStore _navigationStore;

        public LogoutCommand(NavigationStore navigationStore)
        {
            _navigationStore = navigationStore;
        }

        public override void Execute(object parameter)
        {
            _navigationStore.CurrentVM = new LoginVM(_navigationStore);
        }
    }
    ```
    
    However, we might need to modify `LoginCommand` so that we can perform certain tasks before changing the view (for instance, validate input username & password, then call API to authenticate the user). Therefore, we can adjust `LoginCommand.cs` as follow:
```
public class LoginCommand : CommandBase
    {
        private readonly NavigationStore _navigationStore;
        public LoginVM VM { get; set; }

        public LoginCommand(NavigationStore navigationStore, LoginVM vM)
        {
            _navigationStore = navigationStore;
            VM = vM;
        }

        public override async void Execute(object parameter)
        {
            bool isSuccess = await VM.Login();

            // Only change the view if the authentication is successful.
            if (isSuccess)
            {
                _navigationStore.CurrentVM = new MainViewVM(_navigationStore);
            }
        }
    }
```

Since `LoginCommand` and `LogoutCommand` inherit from `CommandBase`, we have to create `CommandBase.cs` class. `CommandBase` class is a base class for implementing commands and provides a basic structure for defining commands.
```
public abstract class CommandBase : ICommand
    {
        public event EventHandler CanExecuteChanged;

        public virtual bool CanExecute(object parameter) => true;

        public abstract void Execute(object parameter);

        protected void OnCanExecuteChanged()
        {
            CanExecuteChanged?.Invoke(this, new EventArgs());
        }
    }:
```

Next, we implement the commands in View Model:
`LoginVM`:
```
 public class LoginVM : ViewModelBase
    {
				public ICommand LoginCommand { get; }
        
        // Constructor
        public LoginVM(NavigationStore navigationStore)
		{
			LoginCommand = new LoginCommand(navigationStore, this);
		}

        public async Task<bool> Login()
        {   
            bool isSuccess = true;
            // call API to login           
            return isSuccess;
        }
    }
```
    
Same code for `HomeVM`.

Then, we need to connect the view models to the views in MainWindow.xaml or any other components:
`MainWindow.xaml`:
```
  <ContentControl Content="{Binding CurrentVM}">
        <ContentControl.Resources>
            <DataTemplate DataType="{x:Type vm:HomeVM}">
                <view:Home />
            </DataTemplate>
            <DataTemplate DataType="{x:Type vm:LoginVM}">
                <view:Login />
            </DataTemplate>
        </ContentControl.Resources>
    </ContentControl>
```
`MainWindowVM.cs`:
```
public class MainWindowVM : ViewModelBase
    {
        private readonly NavigationStore _navigationStore;
        public ViewModelBase CurrentVM => _navigationStore.CurrentVM;

        public MainWindowVM(NavigationStore navigationStore)
        {
            _navigationStore = navigationStore;

            _navigationStore.CurrentVMChanged += OnCurrentVMChanged;
        }

        private void OnCurrentVMChanged()
        {
            OnPropertyChanged(nameof(CurrentVM));
        }
    }
```

Finally, we instantiate the login View Model in `App.xaml.cs`:
```
protected override void OnStartup(StartupEventArgs e)
        {
            NavigationStore navigationStore = new NavigationStore();

            navigationStore.CurrentVM = new LoginVM(navigationStore);

            MainWindow = new MainWindow()
            {
                DataContext = new MainWindowVM(navigationStore)
            };
            MainWindow.Show();
            base.OnStartup(e);
        }
```

    
