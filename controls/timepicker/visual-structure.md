---
title: Visual Structure
page_title: .NET MAUI TimePicker Documentation - Visual Structure
description: Learn what visual elements the Telerik TimePicker for .NET MAUI displays, and explore the visual structure of the control.
position: 0
previous_url: /controls/timepicker/timepicker-visual-structure
slug: timepicker-visual-structure
---

# .NET MAUI TimePicker Visual Structure

This article describes all visual elements that are used in the TimePicker for .NET MAUI.

## Before and After Time Value Selection

![TimePicker Visual Structure](images/time_picker_placeholder_display.png "Visual elements of Time Picker control")

## Popup Visual Structure

![TimePicker Popup Visual Structure](images/time_picker_structure.png "Visual elements of Time Picker Popup")

## Legend

- `Placeholder`&mdash;The text visualized before picking a time value. You can customize the placeholder through the [`PlaceholderTemplate`]({%slug timepicker-templates%}#placeholdertemplate) property.
- `DisplayStringFormat`&mdash;The text visualized after a time value is picked.
- `Header`&mdash;The text displayed in the popup header. You can set it to a direct text input through the [`HeaderLabelText`]({%slug timepicker-styling%}#popup-styling) property or customize the popup header by using the [`HeaderTemplate`]({%slug timepicker-templates%}#headertemplate) property.
- `SpinnerHeader`&mdash;The text visualized for the spinner header depending on the values that are picked. For example, if the `SpinnerFormatString` is `g` and `AreSpinnerHeadersVisible="True"`, the text visualized for the spinner header will be **Hour** **Minutes** **AM/PM**.
- `Spinner`&mdash;Displays items in a list.
- `SelectionHighlight`&mdash;Highlights the currently selected time when the popup is open.
- `Footer`&mdash;The footer of the popup. By default, it contains the **OK** and **Cancel** buttons. It can be customized through the [`FooterTemplate`]({%slug timepicker-templates%}#footertemplate) property.

## See Also

- [Getting Started]({%slug timepicker-getting-started%})
- [Time Format Strings]({%slug timepicker-formatting%})
