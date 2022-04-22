---
title: Styling
page_title: .NET MAUI Barcode Documentation | Styling
description: "Learn how to customize the colors of the Telerik UI for .NET MAUI Barcode."
position: 8
previous_url: /controls/barcode/barcode-styling
slug: barcode-styling
---

# Styling

The Barcode enables you to change the visual appearance of your barcodes so they match your application theme.

To change the colors of the control, set the `ForegroundColor` and `BackgroundColor` properties.

```XAML
<telerikBarcode:RadBarcode WidthRequest="200" HeightRequest="100"
		HorizontalOptions="Center" VerticalOptions="Center"
		ForegroundColor="DarkBlue"
		BackgroundColor="Beige"
		Value="58000106">
	<telerikBarcode:RadBarcode.Symbology>
		<telerikBarcode:Code39 SizingMode="Stretch" />
	</telerikBarcode:RadBarcode.Symbology>
</telerikBarcode:RadBarcode>
```

Add the following namespace.

```XAML
xmlns:telerikBarcode="clr-namespace:Telerik.XamarinForms.Barcode;assembly=Telerik.Maui.Controls.Compatibility"
```

The following image shows a barcode with custom colors.

![Barcode Colors](images/barcode_colors.png)

## See Also

- [1D Supported Barcodes]({% slug 1dbarcode-overview %})
- [2D Supported Barcodes]({% slug 2dbarcode-overview %})