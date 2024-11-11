---
title: Customize AutoComplete Cursor Color
description: How to access the native entry element inside the RadAutoComplete to customize the cursor
type: how-to
page_title: Customize AutoComplete Cursor
slug: autocomplete-cursor-customization
position: 
tags: maui, autocomplete, radautocomplete, cursor, caret, color, styling
ticketid: 1612671
res_type: kb
---

## Environment
<table>
	<tbody>
		<tr>
			<td>Product Version</td>
			<td>5.2.0</td>
		</tr>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® UI for .NET MAUI</td>
		</tr>
	</tbody>
</table>


## Description

This article shows you how to access the native element through the .NET MAUI handler for RadAutoComplete.

### Step 1.

Subscribe to the HandlerChanged event of the RadAutoComplete you want to customize.

```csharp
MyRadAutoComplete.HandlerChanged += AutoComplete1_HandlerChanged;
```

### Step 2.

In the event handler, access the RadAutoComplete Handler's PlatformView property. From there, you can access all the native platform's features.

```csharp
private void AutoComplete1_HandlerChanged(object sender, EventArgs e)
{
    var platformView = sender as RadAutoComplete;

#if ANDROID
    if (platformView?.Handler?.PlatformView is Telerik.Maui.Border.BorderViewGroup borderViewGroup)
    {
        var textInputs = borderViewGroup.GetChildrenOfType<Google.Android.Material.TextField.TextInputLayout>();
        var textInput = textInputs.FirstOrDefault();

        if (textInput is { EditText.TextCursorDrawable: not null })
        {
            textInput.EditText.TextCursorDrawable?.SetColorFilter(new Android.Graphics.PorterDuffColorFilter(Android.Graphics.Color.Red, Android.Graphics.PorterDuff.Mode.Darken));
        }
    }
#elif __IOS__
    if (platformView?.Handler?.PlatformView is Telerik.Maui.Border.TKBorderView borderView)
    {
        var textField = borderView.FindDescendantView<UIKit.UITextField>();
        
        if(textField != null)
            textField.TintColor = UIKit.UIColor.Red;
    }
#endif
}
```

## Alternate Approach

If you have many instances of the control on a single view, or throughout your app, you may want to consider creating your own custom class and subclassing the RadAutoComplete. In the custom control's class you can override the OnHandlerChanged instead of subscribing to an event handler.

```csharp
public class MyCustomTelerikAutoComplete : Telerik.Maui.Controls.RadAutoComplete
{
    protected override void OnHandlerChanged()
    {
        // 1. Run the default handler logic first
        base.OnHandlerChanged();

        // 2. Find the inner text edit control, then change the cursor
#if ANDROID
        if (this.Handler?.PlatformView is Telerik.Maui.Border.BorderViewGroup borderViewGroup)
        {
            var textInputs = borderViewGroup.GetChildrenOfType<Google.Android.Material.TextField.TextInputLayout>();
            var textInput = textInputs.FirstOrDefault();

            if (textInput is { EditText.TextCursorDrawable: not null })
            {
                textInput.EditText.TextCursorDrawable?.SetColorFilter(new Android.Graphics.PorterDuffColorFilter(Android.Graphics.Color.Red, Android.Graphics.PorterDuff.Mode.Darken));
            }
        }
#elif __IOS__
        if (this.Handler?.PlatformView is Telerik.Maui.Border.TKBorderView borderView)
        {
            // Find the UITextField inside the AutoComplete's layout
            var textField = borderView.FindDescendantView<UIKit.UITextField>();
            
            // Do your customizations
            if(textField != null)
                textField.TintColor = UIKit.UIColor.Red;
        }
#endif
    }
}
```

### Known Limitations

It is not possible to apply caret customization on the following platforms:

- Windows - WinUI3, and WinApp SDK, just does not have any access the caret of the native TextBox.
- MacCatalyst - Due to a .NET MAUI issue, changes to TextField.HintColor is not respected on MacCatalyst.

If either of those situations change, then these limitations may be outdated and you can attempt the customization again.

## See Also

-[Entry Styling]({%slug entry-styling%})

