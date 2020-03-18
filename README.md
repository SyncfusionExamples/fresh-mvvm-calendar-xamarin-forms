# How to bind events in Xamarin.Forms Calendar (SfCalendar) using FreshMVVM framework
The [SfCalendar](https://help.syncfusion.com/xamarin/calendar/overview?) allows you to work with FreshMVVM framework. To achieve this, follow the below steps.

The following article explains about working with FreshMVVM framework 
https://www.syncfusion.com/kb/11228/how-to-bind-events-in-xamarin-forms-calendar-sfcalendar-using-freshmvvm-framework

**Step 1:** Install the [FreshMVVM](https://www.nuget.org/packages/FreshMvvm/) NuGet package in your shared code project.

**Step 2:** Create your XAML page (view) with name ending with “Page”.
``` c#
namespace CalendarXamarin
{
    public partial class CalendarPage : ContentPage
    {
         public CalendarPage ()
         {
            InitializeComponent ();
         }
    }
}
```
**Step 3:** Create a page model with the name ending with PageModel and inherit FreshBasePageModel. If your Page name is MainPage then the PageModel name should be MainPageModel and the namespace of Page and PageModel should be the same.
``` c#
namespace CalendarXamarin
{
     public class CalendarPageModel : FreshBasePageModel
     {
        
     }
}
```
To raise property changed notifier, use RaisePropertyChanged method of base class in your PageModel.
``` c#
public class CalendarPageModel : FreshBasePageModel
{
      private CalendarEventCollection appointments;
 
      public CalendarEventCollection Appointments
      {
           get
           {
                return this.appointments;
           }
           set
           {
                this.appointments = value;
                this.RaisePropertyChanged("Appointments");
           }
      }
 
      public CalendarPageModel()
      {
           this.Appointments = new CalendarEventCollection();
      }
}
```
**Step 4:** Set MainPage using PageModel in your App.xaml.cs file.
``` c#
public partial class App : Application
{
      public App()
      {
          InitializeComponent();
 
          var page = FreshPageModelResolver.ResolvePageModel<CalendarPageModel>();
          var basicNavContainer = new FreshNavigationContainer(page);
          MainPage = basicNavContainer;
      }
}
```
**Step 5:** Bind the event collection to the Calendar [DataSource](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfCalendar.XForms~Syncfusion.SfCalendar.XForms.SfCalendar~DataSource.html?) without mentioning the binding context.
``` xml
<syncfusion:SfCalendar x:Name="calendar" 
                               DataSource="{Binding Appointments}" 
                               ShowInlineEvents="True"/>
```
