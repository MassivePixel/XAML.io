# Binding overview

Binding simplifies presentation logic. Views are typically bound to view models, but can also be bound to any C# object.

## DataContext
Gets or sets the data context for a FrameworkElement when it participates in data binding.

### Bind DataContext in XAML
Declaring in Page attribute
```
DataContext="{Binding Source={StaticResource Locator}, Path=MyPath}"
```

### Bind DataContext in code behind
In constructor or OnNavigated method
```
DataContext = App.MyName; 
```
MyName is the name we choose for our ViewModel (in ViewModelLocator)

### Using d:DataContext - debug DataContext
We use this so we can get intellisence and check did we bind everything correctly in the View
```
d:DataContext="{d:DesignInstance viewModel:SomeViewModel}"
```

### Binding to StaticResource vs Binding to parent context

## How to bind to property
If you have property named PropertyName of type String in the associated data context, the following syntax is used to bind PropertyName to the Text property on TextBlock(the Text property is a dependency property of type string defined on the TextBlockcontrol)
```
<TextBlock Text="{Binding PropertyName}">
```

### Two-way binding
As default binding is One-way. Two-way we use when we want to change from UI something and save it to Data
````
<TextBox Text="{Binding ElementName, Mode=TwoWay}"/>
```

### StringFormat
String Format is not supported in WinRT, but you can use it if you make Converter
```
public class StringFormatConverter : IValueConverter
{
    public object Convert(object value, 
                          Type targetType, 
                          object parameter, 
                          string language)
    {
        return string.Format(parameter as string, value);
    }  
    public object ConvertBack(object value, 
                              Type targetType, 
                              object parameter, 
                              string language)
    {
        return null;
    }
}
```

Declare your converter so you can use it as Static Resource
```
<Page.Resources>
    <local:StringFormatConverter x:Name="StringFormat"/>
</Page.Resources>
```

Use it in binding
```
<TextBlock Text="{Binding Path=SomeText, 
		Converter={StaticResource ResourceKey=StringFormat}, 
                           ConverterParameter='Hello {0}'}"
		 />
```

### Converter
We use it when we want to bind to something but is not the same format.
https://github.com/MassivePixel/wp-guidelines/wiki/Converters

#### Advanced: converters as a dependency object

## How to bind to a list of objects
We declare ListView or GridView and then in ItemSource we bind it to our list that we wanna display. 
Example simple binding to List of Items and then displaying Name of each item in a list
```
<ListView ItemSource={Binding Items}
	/>
	<ListView.ItemTemplate>
		<DataTemplate>
			<Texblock Text={Binding Name}
			/>
		</DataTemplate>
	</ListView.ItemTemplate>
</ListView>
```

## How to bind to a command
We need to implement Command in our ViewModel. After that we can bind to it.
````
<AppBarButon Command={Binding SomeCommand}> //in xaml
```
In ViewModel we implement it either as ICommand or RelayCommand 
```
public Icommand SomeCommand{ get; set; }
//or
public RelayCommand SomeCommand{ get; set; }
```
Then in constructor of the ViewModel we initialize Command
Example
```
Public ViewModel()
{
	SomeCommand= new RelayCommand(Command)
}
```

### CommandParameter
CommandParameter calls mehtod that contains logic that we want our command to do

For more on commands follow this link :         

https://channel9.msdn.com/Series/Windows-Phone-8-1-Development-for-Absolute-Beginners/Part-24-Binding-to-Commands-and-CommandParameters

## Advanced: How to bind event to command
