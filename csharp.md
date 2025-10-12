
# Algorytmy w C# - Sortowanie, Wyszukiwanie i Inne

## 1. Sortowanie bąbelkowe (Bubble Sort)
Porównuje sąsiednie elementy i zamienia je miejscami, jeśli są w złej kolejności.

```csharp
void SortowanieBabelkowe(int[] tablica)
{
    for (int i = 0; i < tablica.Length - 1; i++)
        for (int j = 0; j < tablica.Length - i - 1; j++)
            if (tablica[j] > tablica[j + 1])
            {
                int temp = tablica[j];
                tablica[j] = tablica[j + 1];
                tablica[j + 1] = temp;
            }
}
```

## 2. Sortowanie przez wstawianie (Insertion Sort)
Wstawia każdy element w odpowiednie miejsce w już posortowanej części tablicy.  

```csharp
void SortowaniePrzezWstawianie(int[] tablica)
{
    for (int i = 1; i < tablica.Length; i++)
    {
        int klucz = tablica[i];
        int j = i - 1;
        while (j >= 0 && tablica[j] > klucz)
        {
            tablica[j + 1] = tablica[j];
            j--;
        }
        tablica[j + 1] = klucz;
    }
}
```

## 3. Sortowanie przez wybór (Selection Sort)
Znajduje najmniejszy element i umieszcza go na początku, powtarzając dla reszty tablicy.

```csharp
void SortowaniePrzezWybor(int[] tablica)
{
    for (int i = 0; i < tablica.Length - 1; i++)
    {
        int minIndeks = i;
        for (int j = i + 1; j < tablica.Length; j++)
            if (tablica[j] < tablica[minIndeks]) 
                minIndeks = j;
        
        int temp = tablica[i];
        tablica[i] = tablica[minIndeks];
        tablica[minIndeks] = temp;
    }
}
```

## 4. Sortowanie kubełkowe (Bucket Sort)
Sortuje elementy rozmieszczając je w kubełkach według wartości.

```csharp
void SortowanieKubelkowe(int[] tablica, int maxWartosc)
{
    int[] kubelek = new int[maxWartosc + 1];
    foreach (int element in tablica) 
        kubelek[element]++;
    
    int indeks = 0;
    for (int i = 0; i <= maxWartosc; i++)
        while (kubelek[i] > 0)
        {
            tablica[indeks] = i;
            indeks++;
            kubelek[i]--;
        }
}
```

## 5. Szybkie sortowanie (Quick Sort)
Dzieli tablicę względem elementu pivot i rekurencyjnie sortuje części.

```csharp
void SzybkieSortowanie(int[] tablica, int lewy, int prawy)
{
    if (lewy < prawy)
    {
        int podzial = Podziel(tablica, lewy, prawy);
        SzybkieSortowanie(tablica, lewy, podzial - 1);
        SzybkieSortowanie(tablica, podzial + 1, prawy);
    }
}

int Podziel(int[] tablica, int lewy, int prawy)
{
    int pivot = tablica[prawy];
    int i = lewy - 1;
    for (int j = lewy; j < prawy; j++)
        if (tablica[j] < pivot)
        {
            i++;
            int temp = tablica[i];
            tablica[i] = tablica[j];
            tablica[j] = temp;
        }
    
    int temp2 = tablica[i + 1];
    tablica[i + 1] = tablica[prawy];
    tablica[prawy] = temp2;
    return i + 1;
}
```

## 6. Sortowanie przez scalanie (Merge Sort)
Dzieli tablicę na połowy, sortuje je rekurencyjnie i scala wyniki.

```csharp
void SortowaniePrzezScalanie(int[] tablica, int lewy, int prawy)
{
    if (lewy < prawy)
    {
        int srodek = (lewy + prawy) / 2;
        SortowaniePrzezScalanie(tablica, lewy, srodek);
        SortowaniePrzezScalanie(tablica, srodek + 1, prawy);
        Scal(tablica, lewy, srodek, prawy);
    }
}

void Scal(int[] tablica, int lewy, int srodek, int prawy)
{
    int[] tymczasowa = new int[prawy - lewy + 1];
    int i = lewy;
    int j = srodek + 1;
    int k = 0;
    
    while (i <= srodek && j <= prawy)
    {
        if (tablica[i] <= tablica[j])
        {
            tymczasowa[k] = tablica[i];
            i++;
        }
        else
        {
            tymczasowa[k] = tablica[j];
            j++;
        }
        k++;
    }
    
    while (i <= srodek)
    {
        tymczasowa[k] = tablica[i];
        i++;
        k++;
    }
    while (j <= prawy)
    {
        tymczasowa[k] = tablica[j];
        j++;
        k++;
    }
    
    for (int indeks = 0; indeks < tymczasowa.Length; indeks++)
        tablica[lewy + indeks] = tymczasowa[indeks];
}
```

## 7. Wyszukiwanie liniowe (Linear Search)
Przeszukuje tablicę element po elemencie od początku do końca.

```csharp
int WyszukiwanieLiniowe(int[] tablica, int szukana)
{
    for (int i = 0; i < tablica.Length; i++)
        if (tablica[i] == szukana) 
            return i;
    return -1;
}
```

## 8. Wyszukiwanie binarne (Binary Search)
Przeszukuje posortowaną tablicę dzieląc ją na połowy.

```csharp
int WyszukiwanieBinarne(int[] tablica, int szukana)
{
    int lewy = 0;
    int prawy = tablica.Length - 1;
    while (lewy <= prawy)
    {
        int srodek = (lewy + prawy) / 2;
        if (tablica[srodek] == szukana) 
            return srodek;
        if (tablica[srodek] < szukana) 
            lewy = srodek + 1;
        else 
            prawy = srodek - 1;
    }
    return -1;
}
```

## 9. Zliczanie wystąpień elementów (Count Occurrences)
Liczy ile razy każdy element występuje w tablicy.

```csharp
Dictionary<int, int> ZliczWystapienia(int[] tablica)
{
    var licznik = new Dictionary<int, int>();
    foreach (int element in tablica)
    {
        if (licznik.ContainsKey(element))
            licznik[element]++;
        else
            licznik[element] = 1;
    }
    return licznik;
}
```

## 10. Znajdowanie minimum i maksimum (Find Min and Max)
Znajduje najmniejszą i największą wartość w tablicy jednocześnie.

```csharp
(int minimum, int maksimum) ZnajdzMinMax(int[] tablica)
{
    int minimum = tablica[0];
    int maksimum = tablica[0];
    for (int i = 1; i < tablica.Length; i++)
    {
        if (tablica[i] < minimum) 
            minimum = tablica[i];
        if (tablica[i] > maksimum) 
            maksimum = tablica[i];
    }
    return (minimum, maksimum);
}
```

## 11. Odwracanie tablicy (Array Reversal)
Zmienia kolejność elementów w tablicy na odwrotną.

```csharp
void OdwrocTablice(int[] tablica)
{
    for (int i = 0; i < tablica.Length / 2; i++)
    {
        int temp = tablica[i];
        tablica[i] = tablica[tablica.Length - 1 - i];
        tablica[tablica.Length - 1 - i] = temp;
    }
}
```

## 12. Przeszukiwanie z wartownikiem (Sentinel Search)
Wyszukiwanie liniowe z wartownikiem na końcu tablicy dla optymalizacji.

```csharp
int PrzeszukiwanieZWartownikiem(int[] tablica, int szukana)
{
    int ostatni = tablica[tablica.Length - 1];
    tablica[tablica.Length - 1] = szukana;
    
    int i = 0;
    while (tablica[i] != szukana) 
        i++;
    
    tablica[tablica.Length - 1] = ostatni;
    
    if (i < tablica.Length - 1 || ostatni == szukana)
        return i;
    return -1;
}
```

## 13. Lider w zbiorze (Majority Element)
Znajduje element występujący w więcej niż połowie elementów tablicy.

```csharp
int ZnajdzLidera(int[] tablica)
{
    int kandydat = tablica[0];
    int licznik = 1;
    for (int i = 1; i < tablica.Length; i++)
    {
        if (tablica[i] == kandydat)
            licznik++;
        else
        {
            licznik--;
            if (licznik == 0)
            {
                kandydat = tablica[i];
                licznik = 1;
            }
        }
    }
    return kandydat;
}
```

## 14. Metoda Newton-Raphson (Newton-Raphson Method)
Numeryczna metoda znajdowania pierwiastka kwadratowego liczby.

```csharp
double NewtonRaphson(double liczba, double precyzja = 1e-10)
{
    double x = liczba / 2;
    double roznica = x * x - liczba;
    
    while (roznica > precyzja || roznica < -precyzja)
    {
        x = (x + liczba / x) / 2;
        roznica = x * x - liczba;
    }
    return x;
}
```

## 15. Liczby doskonałe (Perfect Numbers)
Sprawdza czy liczba jest doskonała (suma dzielników równa liczbie).

```csharp
bool CzyLiczbaDoskonala(int liczba)
{
    if (liczba <= 1) 
        return false;
    
    int suma = 1;
    for (int i = 2; i * i <= liczba; i++)
    {
        if (liczba % i == 0)
        {
            suma += i;
            if (i * i != liczba)
                suma += liczba / i;
        }
    }
    return suma == liczba;
}
```
