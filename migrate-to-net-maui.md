---
title: Migration
page_title: Migrating from Telerik UI for Xamarin to .NET MAUI
description: "Convert your Telerik UI for Xamarin application to Telerik UI for .NET MAUI by updating the namespaces and the necessary NuGet packages. "
tags: maui, dotnet maui, telerik maui, migration, xamarin.forms
slug: migrate-to-net-maui
previous_url: /get-started/migrate-to-net-maui
position: 5
---

# Migrating from Telerik UI for Xamarin to Telerik UI for .NET MAUI

This guide provides the information you need to convert your application, which was built with [Telerik UI for Xamarin controls](https://www.telerik.com/maui-ui#Controls), to a .NET MAUI one, which uses the Telerik UI for .NET MAUI components. By migrating to .NET MAUI, you will be able to receive the latest features and mobile operating system support for your project.

## Step 1: Migrate the Xamarin Application to .NET MAUI

While you don't need to fully rewrite your existing Xamarin project, you will still need to make changes to ensure its smooth transition to .NET 6.0 and, thus, update to .NET MAUI.

The following list summarizes the required steps. For the detailed guide, go to the official Microsoft documentation on [how to migrate your Xamarin.Forms application to the .NET SDK style](https://docs.microsoft.com/en-us/dotnet/maui/get-started/migrate).

1. Convert the projects from the .NET framework to the .NET SDK style.
1. Update the namespaces.
1. Update any incompatible NuGet packages.
1. Address any breaking API changes.
1. Run the converted application and verify that it functions correctly.

## Step 2: Replace the Telerik References

Once your Xamarin.Forms app has been migrated to .NET MAUI, you’re ready to replace the Telerik UI for Xamarin references with the Telerik UI for .NET MAUI ones and, then, register the controls.

To reference the .NET MAUI controls, use wither of the following approaches:

* Manually add the required Telerik packages to the solution.
* Reference the Telerik NuGet packages.

### Manually Adding the Assemblies

replace the Telerik Xamaron assemblies with the Telerik UI for .NET MAUI package, using the local NuGet feeds. To get the Telerik UI for .NET MAUI `.nupkg` file, download any of the following:

* An `automatic installation` for Windows or Mac.
* The `.zip` file that contains the `.nupkg` file.
* The `Telerik.UI.for.Maui.[Version].nupkg` file from your Telerik account. For the detailed guide, go to the article on [downloading the Telerik UI for .NET MAUI product files]({%slug download-product-files%}).

When the `.nupkg` file is available on your machine, you are ready to set up the local NuGet feed. For the detailed guide on setting up the local NuGet package, go to the [Local feeds](https://docs.microsoft.com/en-us/nuget/hosting-packages/local-feeds) official Microsoft topic.

### Referencing the Telerik .NET MAUI NuGet Packages using the Telerik NuGet Server

When using the Telerik NuGet server, you can install the `Telerik.UI.for.MAUI` NuGet package in the .NET MAUI Application.

For the detailed guide on configuring the Telerik NuGet Server and installing the Telerik UI for .NET MAUI NuGet package, go to the article about [installing Telerik UI for .NET MAUI with NuGet]({%slug telerik-nuget-server%}).

## Step 2: Register the .NET MAUI Controls

Now, you will register the Telerik controls through the `Telerik.Maui.Controls.Compatibility.UseTelerik` extension method that will be called inside the `CreateMauiApp` method of the `MauiProgram.cs` file of your project:

**1.** Go to the `MauiProgram.cs` file and add the needed namespace:

```C#
using Telerik.Maui.Controls.Compatibility;
```

**2.** Call the `UseTelerik()` method inside the `CreateMauiApp` method:

```C#
public static class MauiProgram
{
	public static MauiApp CreateMauiApp()
	{
		var builder = MauiApp.CreateBuilder();
		builder
			.UseTelerik()
			.UseMauiApp<App>()
			.ConfigureFonts(fonts =>
			{
				fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
			});

		return builder.Build();
	}
}
```

## Step 3: Replace the Xamarin Components with Their .NET MAUI Counterparts

Now, you can replace the Telerik UI for Xamarin components with their Telerik UI for .NET MAUI counterparts.

### Notes on Component Migration

Before you start, note the following:

* You can directly replace some components, such as the DataGrid, ListView, Barcode, Button, and more, by changing their respective namespace. All Telerik UI for .NET MAUI controls use a common `xmlns:telerik="http://schemas.telerik.com/2022/xaml/maui"` `telerik` namespace.

* Some components, such as the MaskedEntries, Entry, Pickers, and TabView, require API changes. For the detailed guide, go to their corresponding article on converting the Xamarin control to .NET MAUI, for example, the topic about [migrating the Entry from Xamarin.Forms]({%slug entry-migrate-from-xamarin%}).

If you use components that are not yet available in Telerik UI for .NET MAUI, note that the team is constantly working on enriching the suite by adding more controls to it. To get more information about what is expected, refer to the following resources:

* For more information on the planned releases, go to the [Telerik UI for .NET MAUI Roadmap](https://www.telerik.com/support/whats-new/maui-ui/roadmap).
* For logged issues and feature requests for new components, go to the [Telerik UI for .NET MAUI Feedback Portal](https://feedback.telerik.com/maui).
* Alternatively, directly contact the team through the [support ticketing system](https://www.telerik.com/account/support-center/contact-us/technical-support?pid=2338), the [forums](https://www.telerik.com/forums/maui), or the [Feedback Portal](https://feedback.telerik.com/maui).

### Migration Guides for .NET MAUI Components

The following list includes the links to the available Xamarin-to-MAUI migration guides for Telerik UI controls:

* [Accordion]({% slug accordion-migrate-from-xamarin %})
* [AutoComplete]({% slug autocomplete-migrate-from-xamarin %})
* [CheckBox]({% slug checkbox-migrate-from-xamarin %})
* [ComboBox]({% slug combobox-migrate-from-xamarin %})
* [DataForm]({% slug dataform-migrate-from-xamarin %})
* [DatePicker]({% slug migrate-xamarin-datepicker-to-maui %})
* [DateTimePicker]({% slug migrate-xamarin-datetimepicker-to-maui %})
* [Entry]({% slug entry-migrate-from-xamarin %})
* [ImageEditor]({% slug imageeditor-migrate-from-xamarin %})
* [ListPicker]({% slug migrate-xamarin-listpicker-to-maui %})
* [ListView]({% slug migrate-xamarin-listview-to-maui %})
* [MaskedEntry]({% slug maskedentry-migrate-from-xamarin %})
* [ProgressBar]({% slug progressbar-migrate-from-xamarin %})
* [SignaturePad]({% slug signaturepad-migrate-from-xamarin %})
* [TemplatedPicker]({% slug  migrate-xamarin-templatedpicker-to-maui %})
* [TimePicker]({% slug  migrate-xamarin-timepicker-to-maui %})
* [TimeSpanPicker]({% slug migrate-xamarin-timespanpicker-to-maui %})

## Step 4: Port Custom Renderers to Handlers

To customize the appearance and behavior of the native controls on each platform, Xamarin.Forms widely uses custom renderers and platform effects. In .NET MAUI, these renderers are replaced with handlers and, when migrating to .NET MAUI, you will need port the custom renderers to handlers.

For the detailed guide, go to the official Microsoft documentation on GitHub about [how to migrate custom renderers to handlers](https://github.com/dotnet/maui/wiki/Porting-Custom-Renderers-to-Handlers).

## See Also

* [Telerik UI for .NET MAUI Sample Applications]({% slug controls-samples-app %})