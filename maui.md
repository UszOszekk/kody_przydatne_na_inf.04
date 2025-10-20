## 1. **Button** – przycisk

```xml
<Button Text="Kliknij mnie" Clicked="OnButtonClicked"/>
```
```csharp
void OnButtonClicked(object sender, EventArgs e)
{
    DisplayAlert("Info", "Kliknięto przycisk!", "OK");
}
```
**Co robi kod C#?**  
Pokazuje okienko z komunikatem po naciśnięciu przycisku.

---

## 2. **Entry** – pole tekstowe (jednolinijkowe)

```xml
<Entry Placeholder="Wpisz tekst" TextChanged="OnEntryChanged"/>
```
```csharp
void OnEntryChanged(object sender, TextChangedEventArgs e)
{
    string wpisanyTekst = e.NewTextValue;
}
```
**Co robi kod C#?**  
Pobiera wpisany tekst za każdym razem, gdy użytkownik coś zmieni w polu.

---

## 3. **Label** – etykieta, wyświetla tekst

```xml
<Label Text="Witaj, świecie!" FontSize="20" TextColor="Blue"/>
```

---

## 4. **Editor** – pole tekstowe (wielolinijkowe)

```xml
<Editor Placeholder="Wpisz dłuższą wiadomość" HeightRequest="100"/>
```
**Co robi kod?**  
Pozwala wpisać dłuższy tekst, np. komentarz. Obsługa w backendzie podobna jak w Entry (zdarzenie TextChanged).

---

## 5. **Image** – obrazek

```xml
<Image Source="logo.png" WidthRequest="100" HeightRequest="100"/>
```
**Co robi kod?**  
Wyświetla obrazek z pliku `logo.png`.

---

## 6. **CheckBox** – pole wyboru

```xml
<CheckBox IsChecked="false" CheckedChanged="OnCheckBoxChanged"/>
```
```csharp
void OnCheckBoxChanged(object sender, CheckedChangedEventArgs e)
{
    bool czyZaznaczone = e.Value;
}
```
**Co robi kod C#?**  
Sprawdza czy pole zostało zaznaczone/odznaczone przez użytkownika.

---

## 7. **RadioButton + GroupName** – wybór jednej z opcji

```xml
<StackLayout>
    <Label Text="Wybierz ulubiony kolor:" FontSize="18" Margin="0,20,0,10"/>
    <RadioButton Content="Czerwony" GroupName="Kolory" CheckedChanged="OnRadioButtonChecked"/>
    <RadioButton Content="Zielony" GroupName="Kolory" CheckedChanged="OnRadioButtonChecked"/>
    <RadioButton Content="Niebieski" GroupName="Kolory" CheckedChanged="OnRadioButtonChecked"/>
    <Label x:Name="WybranyKolorLabel" Text="Nie wybrano koloru." FontSize="16" Margin="0,20,0,0"/>
</StackLayout>
```
```csharp
private void OnRadioButtonChecked(object sender, CheckedChangedEventArgs e)
{
    var radio = sender as RadioButton;
    if (e.Value)
        WybranyKolorLabel.Text = $"Wybrano: {radio.Content}";
}
```
**Co robi kod C#?**  
Aktualizuje etykietę, pokazując wybraną opcję (kolor).

---

## 8. **Switch** – przełącznik

```xml
<Switch IsToggled="false" Toggled="OnSwitchToggled"/>
```
```csharp
void OnSwitchToggled(object sender, ToggledEventArgs e)
{
    bool czyWlaczone = e.Value;
}
```
**Co robi kod C#?**  
Sprawdza, czy przełącznik jest włączony/wyłączony.

---

## 9. **Slider** – suwak

```xml
<Slider Minimum="0" Maximum="100" ValueChanged="OnSliderChanged"/>
```
```csharp
void OnSliderChanged(object sender, ValueChangedEventArgs e)
{
    double wartosc = e.NewValue;
}
```
**Co robi kod C#?**  
Pobiera aktualną wartość wybraną przez użytkownika na suwaku.

---

## 10. **Picker** – lista rozwijana

```xml
<Picker Title="Wybierz kolor" SelectedIndexChanged="OnPickerChanged">
    <Picker.Items>
        <x:String>Czerwony</x:String>
        <x:String>Zielony</x:String>
        <x:String>Niebieski</x:String>
    </Picker.Items>
</Picker>
```
```csharp
void OnPickerChanged(object sender, EventArgs e)
{
    Picker picker = (Picker)sender;
    string wybranyKolor = picker.SelectedItem?.ToString();
}
```
**Co robi kod C#?**  
Pobiera wybraną wartość z listy rozwijanej.

---

## 11. **DatePicker / TimePicker**

**DatePicker:**
```xml
<DatePicker DateSelected="OnDateSelected"/>
```
```csharp
void OnDateSelected(object sender, DateChangedEventArgs e)
{
    DateTime wybranaData = e.NewDate;
}
```
**Co robi kod C#?**  
Pobiera wybraną przez użytkownika datę.

**TimePicker:**
```xml
<TimePicker TimeSelected="OnTimeSelected"/>
```
```csharp
void OnTimeSelected(object sender, EventArgs e)
{
    TimePicker picker = (TimePicker)sender;
    TimeSpan godzina = picker.Time;
}
```
**Co robi kod C#?**  
Pobiera wybraną przez użytkownika godzinę.

---

## 12. **Stepper** – zwiększanie/zmniejszanie wartości

```xml
<Stepper Minimum="1" Maximum="10" Increment="1" ValueChanged="OnStepperChanged"/>
```
```csharp
void OnStepperChanged(object sender, ValueChangedEventArgs e)
{
    double wybranaWartosc = e.NewValue;
}
```
**Co robi kod C#?**  
Pobiera aktualną wartość wybraną przez użytkownika na przyciskach plus/minus.

---

## 13. **ListView / CollectionView** – lista elementów

**ListView:**
```xml
<ListView ItemsSource="{Binding MojaLista}">
    <ListView.ItemTemplate>
        <DataTemplate>
            <TextCell Text="{Binding Nazwa}" Detail="{Binding Opis}"/>
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>
```
**Co robi kod?**  
Wyświetla listę obiektów – źródło danych jest najczęściej kolekcją w C# (np. List<string>).

---

## 14. **ProgressBar** – pasek postępu

```xml
<ProgressBar Progress="0.5"/>
```
**Co robi kod?**  
Pokazuje pasek postępu na 50%. W backendzie można zmieniać wartość właściwości `Progress`.

---

## 15. **ActivityIndicator** – animacja ładowania

```xml
<ActivityIndicator IsRunning="true" IsVisible="true"/>
```
**Co robi kod?**  
Pokazuje animację ładowania, gdy trwa jakaś operacja (np. pobieranie danych).

---

## 16. **StackLayout, Grid, FlexLayout** – układ kontrolek

**StackLayout:**
```xml
<StackLayout Orientation="Vertical">
    <Label Text="Nagłówek"/>
    <Button Text="Kliknij"/>
</StackLayout>
```
**Grid:**
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <Label Grid.Row="0" Text="Nagłówek"/>
    <Button Grid.Row="1" Text="Przycisk"/>
</Grid>
```
**Co robi kod?**  
Rozmieszcza kontrolki na ekranie w pionie (StackLayout) lub w siatce (Grid).

---

# Dodatkowe informacje

- Każda kontrolka może mieć własne zdarzenia (np. `Clicked`, `CheckedChanged`, `ValueChanged`) – obsługujemy je w pliku `.xaml.cs`.
- Jeśli chcesz dynamicznie tworzyć kontrolki w C#, możesz to zrobić również w kodzie C# zamiast w XAML.
- Jeśli potrzebujesz przykładu z backendu (np. obsługa listy, logika formularza), napisz!




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