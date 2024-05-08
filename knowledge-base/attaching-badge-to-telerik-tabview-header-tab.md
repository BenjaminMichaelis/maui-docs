---
title: Attaching a Badge to the TabView Header (Tab)
description: Learn how to attach a badge to each tab in the Telerik TabView control to display additional info.
type: how-to
page_title: How to Attach Badge to Telerik TabView Header/Tab
slug: attaching-badge-to-telerik-tabview-header-tab
tags: badge, tabview, header, tab, customization
res_type: kb
---

## Environment
| Property | Value |
| --- | --- |
| Product | BadgeView for .NET MAUI |
| Version | 6.7.0 |

## Description
I want to attach a badge to each tab in the Telerik TabView control. Each badge must display the number of new items in the corresponding tab.

## Solution
Follow these steps to attach a badge to each tab in the Telerik TabView control:

1. Customize the `TabItem` control template by using the `HeaderItemTemplate` property of the TabView control. In the custom control template, add a BadgeView control, attached to a Label or any other suitable control within the TabItem.

```XAML
<ControlTemplate x:Key="myHeaderItemTemplate">
    <telerik:RadBorder BackgroundColor="{TemplateBinding BackgroundColor}"
                    BorderColor="{TemplateBinding BorderColor}"
                    BorderThickness="{TemplateBinding BorderThickness}"
                    CornerRadius="{TemplateBinding CornerRadius}"
                    Padding="{TemplateBinding ContentPadding}">
        <telerik:RadBadgeView BadgeText="1"
                            HorizontalOptions="Center"
                            VerticalOptions="Center"
                            BadgeHorizontalAlignment="Start">
            <telerik:RadBadgeView.Content>
                <Label Text="{TemplateBinding Text}"/>
            </telerik:RadBadgeView.Content>
        </telerik:RadBadgeView>
    </telerik:RadBorder>
</ControlTemplate>
```

2. Set the created control template to the `HeaderItemTemplate` property of the TabView control:

```XAML
<telerik:RadTabView x:Name="tabView"
                    HeaderItemTemplate="{StaticResource myHeaderItemTemplate}">
    <telerik:TabViewItem HeaderText="Home">
        <Label Margin="10" Text="This is the content of the Home tab" />
    </telerik:TabViewItem>
    <telerik:TabViewItem HeaderText="Folder">
        <Label Margin="10" Text="This is the content of the Folder tab" />
    </telerik:TabViewItem>
    <telerik:TabViewItem HeaderText="View">
        <Label Margin="10" Text="This is the content of the View tab" />
    </telerik:TabViewItem>
</telerik:RadTabView>
```

This will display a badge on each tab, showing additional information about the tab content.

## Notes
You can customize the appearance of the BadgeView control by modifying its properties such as colors, size, and position.

## See Also
- [Telerik TabView Documentation](https://docs.telerik.com/devtools/maui/controls/tabview/overview)
- [Telerik BadgeView Documentation](https://docs.telerik.com/devtools/maui/controls/badgeview/overview)
