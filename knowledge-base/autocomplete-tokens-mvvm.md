---
title: Manage the Tokens Collection in .NET MAUI AutoComplete
description: Learn how to add and delete items from the AutoComplete's tokens collection.
type: how-to
page_title: How to Manage the Tokens collection of the RadAutoComplete for .NET MAUI in MVVM approach
slug: autocomplete-tokens-collection-mvvm
tags: autocomplete, .net maui, tokens, collection, mvvm
res_type: kb
---

## Environment

| Version | Product | Author | 
| --- | --- | ---- | 
| 7.1.0 | Telerik UI for .NET MAUI AutoComplete | [Dobrinka Yordanova](https://www.telerik.com/blogs/author/dobrinka-yordanova)| 

## Description

This article explains how to manage the tokens collection of the AutoComplete in MVVM scenario.

## Solution

The `Tokens` collection of the `AutoComplete` is a read-only collection:

```C#
public ObservableCollection<object> Tokens { get; }
```

To add or remove tokens using an MVVM setup, create a custom behavior.

**1.** Create a `TokensBehavior` class that inherits from `Behavior<RadAutoComplete>`:

```C#
public class TokensBehavior : Behavior<RadAutoComplete>
{
    public static readonly BindableProperty TokensProperty =
        BindableProperty.Create(nameof(Tokens), typeof(ObservableCollection<object>), typeof(TokensBehavior), null, propertyChanged: OnTokensPropertyChanged);

    private RadAutoComplete acv;

    public ObservableCollection<object> Tokens
    {
        get
        {
            return (ObservableCollection<object>)this.GetValue(TokensProperty);
        }
        set
        {
            this.SetValue(TokensProperty, value);
        }
    }
    protected override void OnAttachedTo(BindableObject bindable)
    {
        base.OnAttachedTo(bindable);
        this.acv = (RadAutoComplete)bindable;
    }

    protected override void OnDetachingFrom(BindableObject bindable)
    {
        base.OnDetachingFrom(bindable);
    }

    private static void OnTokensPropertyChanged(BindableObject bindable, object oldValue, object newValue)
    {
        var oldCollection = oldValue as INotifyCollectionChanged;
        if (oldCollection != null)
        {
            oldCollection.CollectionChanged -= ((TokensBehavior)bindable).Tokens_CollectionChanged;
        }

        var collection = newValue as INotifyCollectionChanged;
        if (collection != null)
        {
            ((TokensBehavior)bindable).UpdateTransfer(newValue);
            collection.CollectionChanged += ((TokensBehavior)bindable).Tokens_CollectionChanged;
        }
    }

    private void UpdateTransfer(object tokens)
    {
        Transfer((ObservableCollection<object>)tokens, this.acv.Tokens);
        this.acv.Tokens.CollectionChanged += Tokens_CollectionChanged1;
    }

    private void Tokens_CollectionChanged(object sender, NotifyCollectionChangedEventArgs e)
    {
        this.UnsubscribeFromEvents();
        Transfer(this.Tokens, this.acv.Tokens);
        this.SubscribeToEvents();
    }

    private void Tokens_CollectionChanged1(object sender, NotifyCollectionChangedEventArgs e)
    {
        if (e.Action == NotifyCollectionChangedAction.Add)
        {
            this.UnsubscribeFromEvents();
            Transfer(this.acv.Tokens, this.Tokens);
            this.SubscribeToEvents();
        }
    }

    private void SubscribeToEvents()
    {
        this.acv.Tokens.CollectionChanged += this.Tokens_CollectionChanged1;
        if (this.Tokens != null)
        {
            this.Tokens.CollectionChanged += this.Tokens_CollectionChanged;
        }
    }

    private void UnsubscribeFromEvents()
    {
        this.acv.Tokens.CollectionChanged -= this.Tokens_CollectionChanged1;
        if (this.Tokens != null)
        {
            this.Tokens.CollectionChanged -= this.Tokens_CollectionChanged;
        }
    }

    public static void Transfer(ObservableCollection<object> source, ObservableCollection<object> target)
    {
        if (source == null || target == null)
            return;

        target.Clear();
        foreach (var o in source)
        {
            target.Add(o);
        }
    }
}
```

**2.** Set the behavior to the AutoComplete control:

```XAML
<VerticalStackLayout>
    <telerik:RadAutoComplete x:Name="autoCompleteView"
                                        ItemsSource="{Binding Source}"
                                        TextSearchPath="Name" 
                                        DisplayMode="Tokens">
        <telerik:RadAutoComplete.Behaviors>
            <local:TokensBehavior BindingContext="{Binding Source={x:Reference autoCompleteView}, Path=BindingContext}"
                                    Tokens="{Binding SelectedTokens}"/>
        </telerik:RadAutoComplete.Behaviors>
    </telerik:RadAutoComplete>
    <Button Text="Select Token" Command="{Binding SelectTokenCommand}"/>
    <Button Text="Remove Token" Command="{Binding RemoveTokenCommand}"/>
</VerticalStackLayout>
```

**3.** Add the `telerik` namespace:

```XAML
xmlns:telerik="http://schemas.telerik.com/2022/xaml/maui"
```

**4.** Add a sample model:

```C#
public class Customer
{
    public Customer(string name, string email)
    {
        this.Name = name;
        this.Email = email;
    }
    public string Name { get; set; }
    public string Email { get; set; }
}
```

**5.** Add the `ViewModel`:

```C#
public class ViewModel
{
    public ObservableCollection<Customer> Source { get; set; }
    public ViewModel()
    {
        this.Source = new ObservableCollection<Customer>()
            {
                new Customer("Freda Curtis", "fcurtis@mail.com"),
                new Customer("Jeffery Francis", "jfrancis@mail.com"),
                new Customer("Eva Lawson", "elawson@mail.com"),
                new Customer("Emmett Santos", "esantos@mail.com"),
                new Customer("Theresa Bryan", "tbryan@mail.com"),
                new Customer("Jenny Fuller", "jfuller@mail.com"),
                new Customer("Terrell Norris", "tnorris@mail.com"),
            };

        this.SelectTokenCommand = new Command(OnSelectTokenCommandExecuted);
        this.RemoveTokenCommand = new Command(OnRemoveTokenCommandExecuted);

        this.SelectedTokens = new ObservableCollection<object>();
    }

    public ICommand SelectTokenCommand { get; set; }
    public ICommand RemoveTokenCommand { get; set; }

    public ObservableCollection<object> SelectedTokens { get; set; }

    private void OnSelectTokenCommandExecuted(object obj)
    {
        this.SelectedTokens.Add(this.Source[0]);
    }

    private void OnRemoveTokenCommandExecuted(object obj)
    {
        var item = this.SelectedTokens.FirstOrDefault();
        if (item != null)
        {
            this.SelectedTokens.Remove(item);
        }
    }
}
```
