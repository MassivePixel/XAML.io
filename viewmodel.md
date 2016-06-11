# ViewModel
## Overview

> Use private setters whenever possible.

### MVVMLight and ViewModelBase

## Observable Property
Represents property that notify UI when it changes
```
//implementation
class Sample : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
    public int ID { get; set; }
    private string name = String.Empty;
    public string Name
    {
        get
        {
            return this.name;
        }
        set
        {
            if (value != this.name)
            {
                this.name = value;
                NotifyPropertyChanged(”Name”);
            }
        }
    }
    private void NotifyPropertyChanged([CallerMemberName] String propertyName = "")
    {
        if (PropertyChanged != null)
        {
           PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}

//shorter implementation
private string _folderName;
public string FolderName
{
    get { return _folderName; }
    set { Set(ref _folderName, value); }
}
```

## ObservableCollection<T> and binding to list items

Represents a dynamic data collection that provides notifications when items get added, removed, or when the whole list is refreshed.
```
public ObservableCollection<ItemViewModel> Items { get; private set;}
//initialize in constructor
public ArtistViewModel
{
    Items = new ObservableCollection<ItemViewModel>();
}
```
Now we can bind on Items in View.

## Advanced: ObservableProperty

## Advanced: ReactiveProperty

## Commands

### MVVMLight and RelayCommand

> Since most commands do not notify when changed, prefer to initialize them in constructor and use `RelayCommand` which can be disabled.

