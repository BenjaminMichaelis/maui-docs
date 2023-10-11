---
title: Programmatic Scrolling
page_title: .NET MAUI Scheduler Documentation - Programmatic Scrolling
description: Learn more about the programmatic scrolling feature in the Telerik UI for .NET MAUI Scheduler control.
position: 10
slug: scheduler-programmating-scrolling 
---

# Programmatic Scrolling

The Telerik UI for .NET MAUI Scheduler provides an option for programmatic scrolling. The option allows you to set up the `RadScheduler`, so that the view is scrolled to specific time, for example directly to the working hours. This can be achieved with the `ScrollIntoView` method. 

## Scroll Into Time

`ScrollIntoView` method scrolls the current View to the specified time. It accept a single parameter of type `TimeOnly`. The snippet below shows how the method can be used - in short, it scrolls the view to "10AM":

 <snippet id='scheduler-scrolltotime-code' />

 ## See Also

 - [Views]({% slug scheduler-views-overview %})