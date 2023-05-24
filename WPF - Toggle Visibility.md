## Toggle Visibility of two components
We can toggle between two components in the same Window or User Control (which use the same ViewModel) by ultilizing property Visibility

```
<Grid x:Name="Grid-1" Visibility="{Binding IsLoggedIn,Converter={StaticResource BooleanToVisibilityConverter}}">
<Grid x:Name="Grid-2" Visibility="{Binding IsLoggedIn,Converter={StaticResource InverseBooleanToVisibilityConverter}}">
```

In this case, Grid-1 and Grid-2 are opposite. If Grid-1 shows up, Grid-2 will be hidden and vice versa.
The visibility of two components are based on boolean `IsLoggedIn`. We can toggle between them by changing the value of `IsLoggedIn`.
