---
title: ".NET MAUI Display Toast Message"
datePublished: Tue Jan 18 2022 11:54:28 GMT+0000 (Coordinated Universal Time)
cuid: ckyk26jaa06bc7js1hya3fc6u
slug: dot-net-maui-display-toast-message
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/Lks7vei-eAg/upload/v1642339245208/Qf6D2qYno.jpeg
tags: xamarin, android, dotnet

---

While developing a mobile application, do you sometimes need to send feedback to the user after his actions? Even without disturbing the functioning of the application. It is possible to do this with Toast messages. However, you do not directly use Toast messages in .NET MAUI.

Now, I will show you how to show Toast messages like the native android apps in .NET MAUI applications.

So let's start with the definition of Toast messages. and follow the steps below
## What are Toast Messages?
Toast message provides the user with feedback on the process applied. The displayed message remains on the screen for a short time and disappears by itself. By default, it appears horizontally centered at the bottom of the screen. There are two types defined as long and short time duration.
## .NET MAUI Community Toolkit

### What is .NET MAUI Community Toolkit.
The .NET MAUI Community Toolkit is a collection of reusable elements for application development with .NET MAUI, including animations, behaviors, converters, effects, and helpers. It simplifies and demonstrates everyday developer tasks when building iOS, Android, macOS, and WinUI applications using .NET MAUI.

The MAUI Community Toolkit is available as a set of NuGet Packages for new or existing .NET MAUI projects.

### Setup
.NET MAUI Community Toolkit needs to install and register on your MAUI app to install the .NET MAUI Community Toolkit NuGet package 
```
dotnet add package CommunityToolkit.Maui --version 1.1.0
```
after installation is complete you should register the package that the `UseMauiCommunityToolkit()` method adds to MauiPrograms.cs like 
```
using CommunityToolkit.Maui;
namespace MauiApp6;

public static class MauiProgram
{
	public static MauiApp CreateMauiApp()
	{
		var builder = MauiApp.CreateBuilder();
		builder
			.UseMauiApp<App>()
			.UseMauiCommunityToolkit() //this line you should add
			.ConfigureFonts(fonts =>
			{
				fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
				fonts.AddFont("OpenSans-Semibold.ttf", "OpenSansSemibold");
			});

		return builder.Build();
	}
}
```
### See Result 🤩🤩
To display `Toast`, first, use the static method `Toast.Make()` to create the message, then display it with the `Show() ` method.
```
using CommunityToolkit.Maui.Alerts;

CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();

string text = "This is a Toast";
ToastDuration duration = ToastDuration.Short;

var toast = Toast.Make(text, duration);

await toast.Show(cancellationTokenSource.Token);
```
 to see the complete details of this method visit the technical documentation on [this link](https://docs.microsoft.com/en-us/dotnet/communitytoolkit/maui/alerts/toast).

## Without library or packages 
It is possible to use toast messages directly in native applications. But, we have no such option on cross platforms. likely, it is possible to access local features by defining Dependency Services in .NET MAUI.
 

### 1. Add `IToastMessage` Interface
We need an interface that has methods showing short and long period time messages. Because we will implement DependencyServices that we will define on local platforms from this interface.

To create new interface, follow path **right click project > add > new item > interface** called `IToastMessage`.
```
public interface IToastMessage
{
        void ShortToast(string message);
        void LongToast(string message);
}
```
Here we had defined two methods that take a string message as a parameter. We going to override these methods in the Dependency class on the native side.
### 2. Create a Dependency Service
 Create a class called `ToastMessage` on **Platform-specific > Android**.that inherits the `IToastMessage` and implement the interface members. Then implement methods of interface as follow.
```
using Android.Widget;
using ToastMessageSimple.Platforms.Android.Service;
using ToastMessageSimple.Services;
using Application = Android.App.Application;

[assembly:Dependency(typeof(ToastNotification))]

namespace ToastMessageSimple.Platforms.Android.Service;

public class ToastMessage : IToastMessage
{

    public void LongToast(string message)
    {
        Toast.MakeText(Application.Context, message, ToastLength.Short).Show();
    }

    public void ShortToast(string message)
    {
        Toast.MakeText(Application.Context, message, ToastLength.Long).Show();
    }
}
```
You can see `MakeText()`  [here](https://docs.microsoft.com/en-us/dotnet/api/android.widget.toast.maketext) is a native method for android.
When you call `Show()` can view the message.
### 3. Register`IToastMessage` to DependencyService
For this, Open `App.xaml.cs` file add this 
```
DependencyService.Register<IToastMessage>();
```
In constructor method between `InitializeComponent()` and  `MainPage = new MainPage()` like 
```
	public App()
	{
		InitializeComponent();
		DependencyService.Register<IToastMessage>();
		MainPage = new MainPage();
	}
```

### 4. See result 🤩

Open `MainPage.xaml` and remove preset content, add code as follows 
```
    <ScrollView>
        <Grid RowSpacing="25" RowDefinitions="Auto,Auto,*"
              Padding="{OnPlatform iOS='30,60,30,30', Default='30'}">


            <Button 
                Text="Short Time Toast"
                Grid.Row="0"
                SemanticProperties.Hint="See short period toast message"
                Clicked="OnShortToast"
                HorizontalOptions="Center" /> 
			<Button 
                Text="Long Time Toast"
                Grid.Row="1"
                SemanticProperties.Hint="See long period toast message"
                Clicked="OnLongToast"
                HorizontalOptions="Center" />
        </Grid>
    </ScrollView>
```
After this open `MainPage.xaml.cs` add follows  
```
    public MainPage()
	{
		InitializeComponent();
		_toastMessage = DependencyService.Get<IToastMessage>();
	}

	private void OnShortToast(object sender, EventArgs e)
	{
		_toastMessage.ShortToast("Welcome to .Net MAUI");
	}
	private void OnLongToast(object sender, EventArgs e)
	{
		_toastMessage.LongToast("Welcome to .Net MAUI");
	}
```

![Screenshot_20220117-222204.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1642445625959/wZnZC1H4T.jpeg)

![Screenshot_20220117-222211.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1642445635769/HMidy9NCb.jpeg)
** The end **

In this post, We see how can use Toast message in .Net MAUI applications. I hope it was useful. you can see the full code on  [Github](https://github.com/behroozbc/ToastMessageSimple) 
