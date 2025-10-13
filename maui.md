# CollectionView z ObservableCollection w .NET MAUI

W .NET MAUI najwygodniej używać **CollectionView** z **ObservableCollection** jako źródła danych.  
ObservableCollection automatycznie aktualizuje widok, gdy dodajesz/usuwasz elementy.

---

## Przykład pliku XAML (MainPage.xaml)

```xml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="TwojaAplikacja.MainPage">

    <CollectionView ItemsSource="{Binding Items}">
        <CollectionView.ItemTemplate>
            <DataTemplate>
                <StackLayout Padding="10">
                    <Label Text="{Binding Nazwa}" FontSize="18" />
                </StackLayout>
            </DataTemplate>
        </CollectionView.ItemTemplate>
    </CollectionView>

    <Button Text="Dodaj nowy" Clicked="Button_Clicked" />
</ContentPage>
```

---

## Przykład kodu C# (MainPage.xaml.cs)

```csharp
using System.Collections.ObjectModel;

public partial class MainPage : ContentPage
{
    public ObservableCollection<ItemModel> Items { get; set; }

    public MainPage()
    {
        InitializeComponent();
        Items = new ObservableCollection<ItemModel>
        {
            new ItemModel { Nazwa = "Pierwszy" },
            new ItemModel { Nazwa = "Drugi" },
            new ItemModel { Nazwa = "Trzeci" }
        };
        BindingContext = this;
    }

    private void Button_Clicked(object sender, EventArgs e)
    {
        Items.Add(new ItemModel { Nazwa = "Dodano: " + DateTime.Now.ToString("HH:mm:ss") });
    }
}

public class ItemModel
{
    public string Nazwa { get; set; }
}
```

---

## Wyjaśnienie

- **ObservableCollection** – kolekcja, która automatycznie odświeża CollectionView po każdej zmianie.
- **CollectionView i ItemsSource** – automatycznie wyświetla wszystkie obiekty z kolekcji.
- **Dodawanie elementów:**  
  Przycisk na dole dodaje nowy element do ObservableCollection, a CollectionView natychmiast pokazuje nowy wpis.
- **BindingContext = this** – ustawia źródło danych na bieżącą stronę.

---

## Dodatkowe wskazówki

- Możesz dodawać, usuwać, modyfikować elementy w ObservableCollection – CollectionView zawsze pokaże aktualny stan.
- Jeśli chcesz edytować/usunąć element, możesz dodać przycisk w szablonie DataTemplate.

```xml
<Button Text="Usuń" Command="{Binding BindingContext.UsunCommand, Source={x:Reference Name=CollectionView}}" CommandParameter="{Binding .}" />
```
W ViewModelu możesz utworzyć odpowiednią komendę.

---

**Podsumowanie:**  
ObservableCollection to najwygodniejsza kolekcja do dynamicznych list w MAUI. CollectionView automatycznie reaguje na jej zmiany.