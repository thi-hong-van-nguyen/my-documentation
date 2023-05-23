## Toggle between several `User Control` using the same VM
When we toggle between views, we usually will create a new instance of the view model associated with that views. However, in some cases, we want to use the same data for all of the views. So, here is the approach:

### `Home.xaml` user control:
```
<UserControl>    
    <UserControl.DataContext>
        <vm:HomeVM />
    </UserControl.DataContext>

    <Grid>
            <Frame x:Name="HomeFrame" NavigationUIVisibility="Hidden"
                   DataContext="{Binding}"
                   LoadCompleted="HomeFrame_OnLoadCompleted"/>
    </Grid>
</UserControl>
```

### `Home` userControl CS:
```
 public partial class Home : UserControl
    {
        public Home()
        {
            InitializeComponent();
            HomeFrame.Navigate(new FirstView());
        }

        private void HomeFrame_OnLoadCompleted(object sender, System.Windows.Navigation.NavigationEventArgs e)
        {
            if(HomeFrame.Content is FrameworkElement content)
            {
                content.DataContext = HomeFrame.DataContext;
            }
        }
    }
```

With the code above, when the program runs, the first view is displayed is FirstView userControl. 
Then, let say in FirstView, we have a button which allows us to navigate to SecondView, we then have this code:
### `FirstView.xaml`
```
<Button on_Click="NavigateToSecondView">Go to next view</Button>
```

### `FirstView.cs`
```
private void NavigateToSecondView(object sender, System.Windows.Input.MouseButtonEventArgs e)
        {
            parentControl = TreeHelpers.FindParent<UserControl>(this);
            homeFrame = TreeHelpers.FindChild<Frame>(parentControl, "HomeFrame");
            homeFrame.Navigate(new SecondView());
        }
```

In order to achieve the above code, we need two helpers to find the parent user control and child user control so we can get the Frame element:
```
public static T FindParent<T>(DependencyObject child) where T : DependencyObject
        {
            DependencyObject parent = VisualTreeHelper.GetParent(child);

            if (parent == null)
            {
                return null;
            }

            if (parent is T)
            {
                return parent as T;
            }

            return FindParent<T>(parent);
        }

        // Helper method to find a child control with a specified name
        public static T FindChild<T>(DependencyObject parent, string childName) where T : FrameworkElement
        {
            int childCount = VisualTreeHelper.GetChildrenCount(parent);

            for (int i = 0; i < childCount; i++)
            {
                DependencyObject child = VisualTreeHelper.GetChild(parent, i);

                if (child is T && ((T)child).Name == childName)
                {
                    return (T)child;
                }

                T result = FindChild<T>(child, childName);

                if (result != null)
                {
                    return result;
                }
            }

            return null;
        }
```

