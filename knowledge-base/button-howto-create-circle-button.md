---
title: Creating Circular Buttons
page_title: Rendering Circular Buttons - .NET MAUI Knowledge Base
description: Learn how to create, implement, and develop a circular button when using the Telerik UI for .NET MAUI Button control.
type: how-to
slug: button-create-circle-button
previous_url: /controls/button/howto/button-howto-create-circle-button
res_type: kb
---

## Environment

<table>
	<tbody>
    <tr>
      <td>Product</td>
      <td>Telerik UI for .NET MAUI Button</td>
    </tr>
  	<tr>
  		<td>Product Version</td>
  		<td>0.2.0</td>
  	</tr>
	</tbody>
</table>

## Description

How can I create a circular Button based on the Button control for my Telerik UI for .NET MAUI project?

## Solution

To create a circular button with the Telerik UI for .NET MAUI Button, adjust its `Width`, `Height`, and `CornerRadius` properties in the following way:

1. Set `Width` as equal to `Height`.
1. Set `CornerRadius` as half of the `Width`/`Height` value.

The following example demonstrates how to implement the suggested approach.

 ```XAML
<telerik:RadButton WidthRequest="120"
				   HeightRequest="120"                                
				   Text="Circle Button"
				   FontSize="Micro"
				   TextColor="White"
				   BackgroundColor="DarkBlue"
				   CornerRadius="60"  />
 ```

1. Add the namespace:

 ```XAML
xmlns:telerik="http://schemas.telerik.com/2022/xaml/maui"
 ```

The following image shows the end result.

![A Telerik UI for .NET MAUI Circular Button in iOS, Android, and WinUI desktop environment](images/button-howto-circlebutton.png)
