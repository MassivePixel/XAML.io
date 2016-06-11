# MVVM (Model - View -ViewModel)
Model-View-VewModel (MVVM) pattern helps you to cleanly separate the business and presentation logic of your application from its user interface(UI).   

On Windows RT platform (Windows 8.1, Windows phone 8.1) we use MVVM light toolkit that help us accelerate the creation and development of MVVM applications.   
The following illustration shows the three MVVM classes and their interaction.
<img src="http://www.deviantpics.com/images/2015/07/03/IC448690.png" alt="IC448690.png" border="0" />

## View
A visual element - windows page, user control, data template etc    
Reference ViewModel through DataContext    
ValueConverters - customize data being displayed    
Code behind mostly used for complex animations, trasitions, state changing, navigation etc   

## ViewModel
Presentation logic - properties & commands   
No knowledge of the View    
Notifies View of any changes    

## Model
Data and business logic   
No knowledge of the View or the ViewModel   
