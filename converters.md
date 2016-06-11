# Converters

Converters allow us to shape the data items of our View Model into the format need to correctly bind to our View.   
For example we have property that should be either visible to users or hidden from them depending on some flag
First we need to create helper class that for converting values from bool to visibility
```
public class BoolToVisibilityConverter : IValueConverter
{
    public object Convert(object value, 
                          Type targetType, 
                          object parameter, 
                          string language)
    {
        bool isVisible = (bool)value;
        return isVisible ? Visibility.Visible : Visibility.Collapsed;
    }
    public object ConvertBack(object value, 
                              Type targetType, 
                              object parameter, 
                              string language)
    {
        return (Visibility)value == Visibility.Visible;
    }
}
```
Then in ViewModel that we have property created it so we can bind on it
```
private bool isVisible;
public bool IsVisible
{
    get { return isVisible; }
    set 
    { 
        isVisible= value;
        RaisePropertyChanged("IsVisible");
    }
}
```
Before we bind on this property in View we need to register Converter in app.xaml so we can use it as Static Resource
```
<Application.Resources>
    <!-- other resources -->
    <local:BooleanToVisibilityConverter x:Key="BooleanToVisibilityConverter"/>
    <!-- other resources -->
</Application.Resources>
```
And now we can finally tell the binding to use converter
```
<TextBox x:Name="text" 
  Visibility="{Binding IsVisible, 
               Converter={StaticResource BooleanToVisibilityConverter}}" />
```

For more on converters check this page
http://www.codeproject.com/Articles/758656/Use-Converters-in-your-Windows-Phone-Apps
