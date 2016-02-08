# XAML Notes
#### Personal Note For Learning Purpose only [source].


## App.XAML
###App.xaml
App.xaml is the declarative starting point of your application.App.xaml.cs extends the Application class, which is a central class in a WPF Windows application. .NET will go to this class for starting instructions and then start the desired Window or Page from there. This is also the place to subscribe to important application events, like application start, unhandled exceptions and so on.
### App.xaml.cs
This class extends the Application class, allowing us to do stuff on the application level. For instance, you can subscribe to the Startup event, where you can manually create your starting window. Command-line parameters are passed to your WPF application through the **Startup event**.
##### Here's an example:
```xml
<Application x:Class="WpfTutorialSamples.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                         Startup="Application_Startup">
    <Application.Resources></Application.Resources>
</Application>
```
And the code behind:
```csharp
namespace WpfTutorialSamples
{
        public partial class App : Application
        {
                private void Application_Startup(object sender, StartupEventArgs e)
                {
                        MainWindow wnd = new MainWindow();
                        wnd.Title = "Something else";
                        if(e.Args.Length == 1)
                                MessageBox.Show("Now opening file: \n\n" + e.Args[0]);
                        wnd.Show();
                }
        }
}
```

## Resources:
Resources are given a key, using the **x:Key** attribute, which allows you to reference it from other parts of the application by using this key, in combination with the StaticResource markup extension.
```xml
<Window x:Class="WpfTutorialSamples.WPF_Application.ExtendedResourceSample"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:sys="clr-namespace:System;assembly=mscorlib"
        Title="ExtendedResourceSample" Height="160" Width="300"
        Background="{DynamicResource WindowBackgroundBrush}">
    <Window.Resources>
        <sys:String x:Key="ComboBoxTitle">Items:</sys:String>

        <x:Array x:Key="ComboBoxItems" Type="sys:String">
            <sys:String>Item #1</sys:String>
            <sys:String>Item #2</sys:String>
            <sys:String>Item #3</sys:String>
        </x:Array>

        <LinearGradientBrush x:Key="WindowBackgroundBrush">
            <GradientStop Offset="0" Color="Silver"/>
            <GradientStop Offset="1" Color="Gray"/>
        </LinearGradientBrush>
    </Window.Resources>
    <StackPanel Margin="10">
        <Label Content="{StaticResource ComboBoxTitle}" />
        <ComboBox ItemsSource="{StaticResource ComboBoxItems}" />
    </StackPanel>
</Window>
```
### StaticResource vs. DynamicResource:
The main difference is that a static resource is resolved only once, which is at the point where the XAML is loaded. If the resource is then changed later on, this change will not be reflected where you have used the StaticResource.
A DynamicResource on the other hand, is resolved once it's actually needed, and then again if the resource changes.
### Local and application wide resources:
If you only need a given resource for a specific control, you can make it more local by adding it to this specific control, instead of the window. It works exactly the same way, the only difference being that you can now only access from inside the scope of the control where you put it.
The App.xaml file can contain resources just like the window and any kind of WPF control, and when you store them in App.xaml, they are globally accessible in all of windows and user controls of the project. It works exactly the same way as when storing and using from a Window.















[source]: http://www.wpf-tutorial.com/
