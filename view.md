# View

## Xaml based
Simple binding, declare ItemSource which is ObservableCollection in the ViewModel and then we can bind on property inside DataTemplate :
```
<ListView ItemSource={"Binding Animals"}>
    <ListView.ItemTemplate>
        <DataTemplate>
            <TextBlock Text={"Binding Name"}>
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>
```
## Code Behind
Navigation : 
In Windows 8.1 and windows phone 8.1 (RT version) we implement navigation like this : 
```
//basic navigation to some Page
Frame.Navigate(typeof(Page);
//navigation to page from item in ListView or Gridiew
Frame.Navigate(typeof(Page), e.ClickedItem);
```
If we want to call methods of ViewModel inside View : 
```
//for events
var model = sender as ArtistViewModel;
//inside OnNavigatedo method
var model = e.Parameter as ArtistViewModel;
//for example our method private int GetId(FrameworkElement element)
var model = element.DataContext as ArtistViewModel; 
```

