---
title: Item Template
page_title: .NET MAUI TreeView Documentation - Item Template
description: Learn how to customize the default text displayed in the Telerik .NET MAUI TreeView control by using the item template. 
position: 7
slug: treeview-item-template
---

# .NET MAUI TreeView Item Template

The TreeView `ItemTemplate` property enables you to customize the text displayed in the TreeView items. Using this property allows you to apply text styles to all TreeView items.

In addition to the item's text, TreeView allows you to customize the checkbox, image, and expand/collapse indicator. For this purpose, use the [Control Template]({%slug treeview-control-template%}).

The following example shows how to define custom `ItemTemplate` by using the `ItemTemplate` property: 

**1.** Define the `RadTreeView` control and the `ItemTemplate`: 

```XAML
<telerik:RadTreeView x:Name="treeView" 
                        ItemsSource="{Binding Items}">
    <telerik:TreeViewDescriptor ItemsSourcePath="Children"
                                DisplayMemberPath="Name"
                                TargetType="{x:Type local:Item}" />
    <!-- modify the label and add additional elements in the label area.
ItemTemplate does not include expand indicator, image, checkbox, only the text, you can add additional elements to it.
    For example, I have added a button-->
    <telerik:RadTreeView.ItemTemplate>
        <DataTemplate>
            <Grid ColumnDefinitions="*,auto">
                <Label Text="{Binding Name}" BackgroundColor="Yellow"/>
                <telerik:TreeViewItemButton Text="Button" Grid.Column="1" WidthRequest="100" BackgroundColor="Green" HorizontalOptions="End"/>
            </Grid>
        </DataTemplate>
    </telerik:RadTreeView.ItemTemplate>
</telerik:RadTreeView>
```

**2.** Add the `telerik` namespaces:

```XAML
xmlns:telerik="http://schemas.telerik.com/2022/xaml/maui"
```

**3.** Create a sample `Item` class:

<snippet id='treeview-getting-started-item' />

**4.** Add the `ViewModel` class:

<snippet id='treeview-getting-started-viewmodel' />


## See Also

* [Expand and Collapse TreeView Items]({%slug treeview-expand-collapse%})
* [CheckBoxes in TreeView]({%slug treeview-checkboxes%})
* [Styling the TreeView Item]({%slug treeview-item-style%})
* [Scrolling options]({%slug treeview-scrolling%})
* [Multiple and Single Selection]({%slug treeview-selection%})
* [Available Commands in .NET MAUI TreeView]({%slug treeview-commands%})