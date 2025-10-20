
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

    // Etap 1: znajdź kandydata
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

    // Etap 2: sprawdź, czy kandydat rzeczywiście jest liderem
    int wystapienia = 0;
    for (int i = 0; i < tablica.Length; i++)
        if (tablica[i] == kandydat)
            wystapienia++;

    if (wystapienia > tablica.Length / 2)
        return kandydat;  
    else
        return -1;         
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
## 16. Badanie czy liczba jest pierwsza (Is Prime)
Sprawdza, czy liczba jest pierwsza.

```csharp
bool CzyPierwsza(int liczba)
{
    if (liczba < 2) return false;
    for (int i = 2; i * i <= liczba; i++)
        if (liczba % i == 0)
            return false;
    return true;
}
```

## 17. Silnia (Factorial)
Rekurencyjna i iteracyjna funkcja silni.

```csharp
long SilniaIteracyjnie(int n)
{
    long wynik = 1;
    for (int i = 2; i <= n; i++)
        wynik *= i;
    return wynik;
}

long SilniaRekurencyjnie(int n)
{
    if (n <= 1) return 1;
    return n * SilniaRekurencyjnie(n - 1);
}
```

## 18. Fibonacci – rekurencyjnie i iteracyjnie
Generuje n-ty wyraz ciągu Fibonacciego.

```csharp
int FibonacciRekurencyjnie(int n)
{
    if (n <= 1) return n;
    return FibonacciRekurencyjnie(n - 1) + FibonacciRekurencyjnie(n - 2);
}

int FibonacciIteracyjnie(int n)
{
    if (n <= 1) return n;
    int a = 0, b = 1;
    for (int i = 2; i <= n; i++)
    {
        int temp = a + b;
        a = b;
        b = temp;
    }
    return b;
}
```

## 19. Suma elementów tablicy / ciągu (Sum of Array)
Oblicza sumę wszystkich elementów tablicy.

```csharp
int SumaTablicy(int[] tablica)
{
    int suma = 0;
    foreach (int el in tablica)
        suma += el;
    return suma;
}
```

## 20. Schemat Hornera (Horner's Scheme)
Oblicza wartość wielomianu przy użyciu schematu Hornera.

```csharp
double Horner(double[] wspolczynniki, double x)
{
    double wynik = wspolczynniki[0];
    for (int i = 1; i < wspolczynniki.Length; i++)
        wynik = wynik * x + wspolczynniki[i];
    return wynik;
}
```

## 21. NWD, NWW oraz operacje na ułamkach
Największy wspólny dzielnik (NWD) i najmniejsza wspólna wielokrotność (NWW):

```csharp
int NWD(int a, int b)
{
    while (b != 0)
    {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int NWW(int a, int b)
{
    return a / NWD(a, b) * b;
}
```
Operacje na ułamkach (dodawanie, odejmowanie, mnożenie):

```csharp
(int licznik, int mianownik) DodajUlamki(int l1, int m1, int l2, int m2)
{
    int mianownik = NWW(m1, m2);
    int licznik = l1 * (mianownik / m1) + l2 * (mianownik / m2);
    int dzielnik = NWD(Math.Abs(licznik), mianownik);
    return (licznik / dzielnik, mianownik / dzielnik);
}

(int licznik, int mianownik) OdejmijUlamki(int l1, int m1, int l2, int m2)
{
    int mianownik = NWW(m1, m2);
    int licznik = l1 * (mianownik / m1) - l2 * (mianownik / m2);
    int dzielnik = NWD(Math.Abs(licznik), mianownik);
    return (licznik / dzielnik, mianownik / dzielnik);
}

(int licznik, int mianownik) PomnozUlamki(int l1, int m1, int l2, int m2)
{
    int licznik = l1 * l2;
    int mianownik = m1 * m2;
    int dzielnik = NWD(Math.Abs(licznik), mianownik);
    return (licznik / dzielnik, mianownik / dzielnik);
}
```

## 22. Potęgowanie szybkie (Fast Exponentiation)
Oblicza a^n w czasie logarytmicznym.

```csharp
long PotegowanieSzybkie(long a, int n)
{
    long wynik = 1;
    while (n > 0)
    {
        if ((n & 1) == 1)
            wynik *= a;
        a *= a;
        n >>= 1;
    }
    return wynik;
}
```

## 23. Połowienie przedziałów (Bisection Method)
Znajduje pierwiastek funkcji w przedziale [a, b] metodą bisekcji.

```csharp
double Bisekcja(Func<double, double> f, double a, double b, double epsilon = 1e-10)
{
    double fa = f(a), fb = f(b);
    if (fa * fb > 0) throw new ArgumentException("Funkcja musi mieć różne znaki na końcach przedziału.");
    while (Math.Abs(b - a) > epsilon)
    {
        double c = (a + b) / 2;
        double fc = f(c);
        if (fc == 0.0) return c;
        if (fa * fc < 0)
        {
            b = c;
            fb = fc;
        }
        else
        {
            a = c;
            fa = fc;
        }
    }
    return (a + b) / 2;
}
```

## 24. Metoda trapezów (Trapezoid Method)
Numeryczne całkowanie funkcji metodą trapezów.

```csharp
double CałkujTrapezy(Func<double, double> f, double a, double b, int n)
{
    double h = (b - a) / n;
    double suma = (f(a) + f(b)) / 2.0;
    for (int i = 1; i < n; i++)
        suma += f(a + i * h);
    return suma * h;
}
```

## 25. Metoda prostokątów (Rectangle Method)
Numeryczne całkowanie funkcji metodą prostokątów.

```csharp
double CałkujProstokaty(Func<double, double> f, double a, double b, int n)
{
    double h = (b - a) / n;
    double suma = 0.0;
    for (int i = 0; i < n; i++)
        suma += f(a + i * h);
    return suma * h;
}
```

## 26. Nierówność trójkąta (Triangle Inequality)
Sprawdza czy z trzech boków można zbudować trójkąt.

```csharp
bool CzyMoznaZbudowacTrojkat(double a, double b, double c)
{
    return a + b > c && a + c > b && b + c > a;
}
```

## 27. Dwa odcinki – czy się przecinają (Do Segments Intersect)
Sprawdza czy dwa odcinki się przecinają.

```csharp
bool CzyOdcinkiPrzecinaja(
    (double x, double y) p1, (double x, double y) p2,
    (double x, double y) q1, (double x, double y) q2)
{
    double Cross((double x, double y) a, (double x, double y) b, (double x, double y) c)
        => (b.x - a.x) * (c.y - a.y) - (b.y - a.y) * (c.x - a.x);

    return
        Math.Sign(Cross(p1, p2, q1)) != Math.Sign(Cross(p1, p2, q2)) &&
        Math.Sign(Cross(q1, q2, p1)) != Math.Sign(Cross(q1, q2, p2));
}
```

## 28. Odwrotna notacja polska (Reverse Polish Notation)
Oblicza wyrażenie zapisane w odwrotnej notacji polskiej.

```csharp
double OdwrotnaNotacjaPolska(string[] tokens)
{
    Stack<double> stos = new Stack<double>();
    foreach (var token in tokens)
    {
        if (double.TryParse(token, out double liczba))
            stos.Push(liczba);
        else
        {
            double b = stos.Pop();
            double a = stos.Pop();
            switch (token)
            {
                case "+": stos.Push(a + b); break;
                case "-": stos.Push(a - b); break;
                case "*": stos.Push(a * b); break;
                case "/": stos.Push(a / b); break;
            }
        }
    }
    return stos.Pop();
}
```
## 29. Rozkład liczby na czynniki pierwsze (Prime Factorization)
Zwraca tablicę czynników pierwszych liczby.

```csharp
int[] CzynnikiPierwsze(int liczba)
{
    int[] czynniki = new int[32]; // max 32 czynników dla typowych liczb
    int licznik = 0;
    int n = liczba;
    for (int i = 2; i * i <= n; i++)
    {
        while (n % i == 0)
        {
            czynniki[licznik++] = i;
            n /= i;
        }
    }
    if (n > 1)
        czynniki[licznik++] = n;
    int[] wynik = new int[licznik];
    for (int i = 0; i < licznik; i++)
        wynik[i] = czynniki[i];
    return wynik;
}
```

## 30. Sito Eratostenesa (Sieve of Eratosthenes)
Znajduje wszystkie liczby pierwsze do n, wynik jako tablica.

```csharp
int[] SitoEratostenesa(int n)
{
    bool[] pierwsze = new bool[n + 1];
    for (int i = 2; i <= n; i++)
        pierwsze[i] = true;
    for (int i = 2; i * i <= n; i++)
        if (pierwsze[i])
            for (int j = i * i; j <= n; j += i)
                pierwsze[j] = false;
    // policz ile liczb pierwszych
    int liczbaPierwszych = 0;
    for (int i = 2; i <= n; i++)
        if (pierwsze[i])
            liczbaPierwszych++;
    int[] wynik = new int[liczbaPierwszych];
    int indeks = 0;
    for (int i = 2; i <= n; i++)
        if (pierwsze[i])
            wynik[indeks++] = i;
    return wynik;
}
```

## 31. Pozycyjne reprezentacje liczb (Positional Number Systems)
Konwersja liczby z systemu dziesiętnego na inny system pozycyjny (np. binarny, ósemkowy, szesnastkowy).

```csharp
string NaSystemPozycyjny(int liczba, int podstawa)
{
    if (liczba == 0) return "0";
    string cyfry = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    char[] wynik = new char[32]; // max 32 cyfr
    int indeks = 0;
    int abs = liczba < 0 ? -liczba : liczba;
    while (abs > 0)
    {
        int reszta = abs % podstawa;
        wynik[indeks++] = cyfry[reszta];
        abs /= podstawa;
    }
    string s = "";
    for (int i = indeks - 1; i >= 0; i--)
        s += wynik[i];
    if (liczba < 0)
        s = "-" + s;
    return s;
}
```

### Przeliczanie liczby z dziesiętnego na binarny (Decimal to Binary Conversion)
Przeliczanie liczby dziesiętnej na binarną polega na dzieleniu liczby przez 2, zapisywaniu reszt i odczytaniu ich od końca.

```csharp
string DziesietnyNaBinarny(int liczba)
{
    return NaSystemPozycyjny(liczba, 2);
}
```

### Instrukcja: Jak przeliczać liczby na inne systemy pozycyjne

**Z dziesiętnego na inny system (np. binarny, ósemkowy, szesnastkowy):**
1. Wybierz podstawę docelową (np. binarny – 2, ósemkowy – 8, szesnastkowy – 16).
2. Dziel liczbę przez podstawę, zapisując reszty z kolejnych dzieleń.
3. Odczytaj reszty od końca – to wynik w wybranym systemie.
4. Możesz użyć funkcji NaSystemPozycyjny(liczba, podstawa) w C#.

**Przykład ręczny:**
- Liczba 13 na binarny:
    - 13 / 2 = 6, reszta 1
    - 6 / 2 = 3, reszta 0
    - 3 / 2 = 1, reszta 1
    - 1 / 2 = 0, reszta 1
    - Czytamy reszty od końca: 1101

**Z innego systemu na dziesiętny:**
- Pomnóż każdą cyfrę przez odpowiednią potęgę podstawy i zsumuj.
- Np. 1101₂ = 1×2³ + 1×2² + 0×2¹ + 1×2⁰ = 8 + 4 + 0 + 1 = 13

### Funkcja konwersji z binarnego na dziesiętny:
W teorii może działać funkcja wbudowana np: 
```csharp 
Convert.ToInt32(liczbaBin, 2);
```
```csharp
int BinarnyNaDziesietny(string liczbaBin)
{
    int wynik = 0;
    int potega = 1;
    for (int i = liczbaBin.Length - 1; i >= 0; i--)
    {
        if (liczbaBin[i] == '1')
            wynik += potega;
        potega *= 2;
    }
    return wynik;
}
```
## 32. Sprawdzenie palindromu (Palindrome Check)
Sprawdza, czy podany tekst jest palindromem (taki sam czytany od przodu i od tyłu).

```csharp
bool CzyPalindrom(string tekst)
{
    int lewy = 0;
    int prawy = tekst.Length - 1;
    while (lewy < prawy)
    {
        if (tekst[lewy] != tekst[prawy])
            return false;
        lewy++;
        prawy--;
    }
    return true;
}
```

## 33. Zliczanie liter (Count Letters)
Zlicza liczbę liter w stringu (ignoruje inne znaki).

```csharp
int ZliczLitery(string tekst)
{
    int licznik = 0;
    for (int i = 0; i < tekst.Length; i++)
        if ((tekst[i] >= 'A' && tekst[i] <= 'Z') || (tekst[i] >= 'a' && tekst[i] <= 'z'))
            licznik++;
    return licznik;
}
```

## 34. Zliczanie wystąpień znaków (Count Character Occurrences)
Policzy, ile razy każdy znak występuje w tekście.

```csharp
int[] ZliczWystapieniaZnakow(string tekst)
{
    int[] licznik = new int[256]; // dla ASCII
    for (int i = 0; i < tekst.Length; i++)
        licznik[(byte)tekst[i]]++;
    return licznik;
}
```

## 35. Porównywanie stringów (Compare Strings)
Porównuje dwa stringi – zwraca true, jeśli są identyczne.

```csharp
bool PorownajStringi(string a, string b)
{
    if (a.Length != b.Length)
        return false;
    for (int i = 0; i < a.Length; i++)
        if (a[i] != b[i])
            return false;
    return true;
}
```

## 36. Wyszukiwanie wzorca w tekście (Pattern Search in Text)
Znajduje indeks pierwszego wystąpienia wzorca w tekście (algorytm naiwny).

```csharp
int WyszukajWzorzec(string tekst, string wzorzec)
{
    int n = tekst.Length;
    int m = wzorzec.Length;
    for (int i = 0; i <= n - m; i++)
    {
        int j = 0;
        while (j < m && tekst[i + j] == wzorzec[j])
            j++;
        if (j == m)
            return i;
    }
    return -1;
}
```

## 37. Anagramy (Anagrams)
Sprawdza, czy dwa teksty są anagramami (zawierają te same znaki z tą samą liczbą wystąpień).

```csharp
bool CzyAnagram(string a, string b)
{
    if (a.Length != b.Length)
        return false;
    int[] licznikA = new int[256];
    int[] licznikB = new int[256];
    for (int i = 0; i < a.Length; i++)
    {
        licznikA[(byte)a[i]]++;
        licznikB[(byte)b[i]]++;
    }
    for (int i = 0; i < 256; i++)
        if (licznikA[i] != licznikB[i])
            return false;
    return true;
}
```
## 38. Stos (Stack) – operacje push/pop

```csharp
class Stack
{
    private int[] dane;
    private int szczyt;
    public Stack(int rozmiar)
    {
        dane = new int[rozmiar];
        szczyt = -1;
    }
    public void Push(int wartosc)
    {
        if (szczyt < dane.Length - 1)
            dane[++szczyt] = wartosc;
    }
    public int Pop()
    {
        if (szczyt >= 0)
            return dane[szczyt--];
        return -1; // lub wyjątek
    }
    public bool IsEmpty()
    {
        return szczyt == -1;
    }
}
```

## 39. Kolejka (Queue) – operacje enqueue/dequeue

```csharp
class Queue
{
    private int[] dane;
    private int poczatek, koniec, liczba;
    public Queue(int rozmiar)
    {
        dane = new int[rozmiar];
        poczatek = 0;
        koniec = 0;
        liczba = 0;
    }
    public void Enqueue(int wartosc)
    {
        if (liczba < dane.Length)
        {
            dane[koniec] = wartosc;
            koniec = (koniec + 1) % dane.Length;
            liczba++;
        }
    }
    public int Dequeue()
    {
        if (liczba > 0)
        {
            int wynik = dane[poczatek];
            poczatek = (poczatek + 1) % dane.Length;
            liczba--;
            return wynik;
        }
        return -1; // lub wyjątek
    }
    public bool IsEmpty()
    {
        return liczba == 0;
    }
}
```

## 40. Kolejka dwukierunkowa (Deque) – operacje z obu stron

```csharp
class Deque
{
    private int[] dane;
    private int poczatek, koniec, liczba;
    public Deque(int rozmiar)
    {
        dane = new int[rozmiar];
        poczatek = 0;
        koniec = 0;
        liczba = 0;
    }
    public void PushFront(int wartosc)
    {
        if (liczba < dane.Length)
        {
            poczatek = (poczatek - 1 + dane.Length) % dane.Length;
            dane[poczatek] = wartosc;
            liczba++;
        }
    }
    public void PushBack(int wartosc)
    {
        if (liczba < dane.Length)
        {
            dane[koniec] = wartosc;
            koniec = (koniec + 1) % dane.Length;
            liczba++;
        }
    }
    public int PopFront()
    {
        if (liczba > 0)
        {
            int wynik = dane[poczatek];
            poczatek = (poczatek + 1) % dane.Length;
            liczba--;
            return wynik;
        }
        return -1;
    }
    public int PopBack()
    {
        if (liczba > 0)
        {
            koniec = (koniec - 1 + dane.Length) % dane.Length;
            int wynik = dane[koniec];
            liczba--;
            return wynik;
        }
        return -1;
    }
    public bool IsEmpty()
    {
        return liczba == 0;
    }
}
```

## 41. Lista jednokierunkowa – wstawianie, usuwanie, odczyt

```csharp
class Node
{
    public int wartosc;
    public Node next;
    public Node(int wartosc)
    {
        this.wartosc = wartosc;
        next = null;
    }
}

class ListaJednokierunkowa
{
    private Node head;
    public void WstawNaPoczatku(int wartosc)
    {
        Node nowy = new Node(wartosc);
        nowy.next = head;
        head = nowy;
    }
    public void Usun(int wartosc)
    {
        Node poprzedni = null;
        Node aktualny = head;
        while (aktualny != null && aktualny.wartosc != wartosc)
        {
            poprzedni = aktualny;
            aktualny = aktualny.next;
        }
        if (aktualny != null)
        {
            if (poprzedni == null)
                head = aktualny.next;
            else
                poprzedni.next = aktualny.next;
        }
    }
    public Node Odczytaj(int indeks)
    {
        Node aktualny = head;
        int licznik = 0;
        while (aktualny != null)
        {
            if (licznik == indeks)
                return aktualny;
            licznik++;
            aktualny = aktualny.next;
        }
        return null;
    }
}
```

## 42. Lista dwukierunkowa – wstawianie, usuwanie, odczyt

```csharp
class DNode
{
    public int wartosc;
    public DNode prev, next;
    public DNode(int wartosc)
    {
        this.wartosc = wartosc;
        prev = next = null;
    }
}

class ListaDwukierunkowa
{
    private DNode head, tail;
    public void WstawNaPoczatku(int wartosc)
    {
        DNode nowy = new DNode(wartosc);
        nowy.next = head;
        if (head != null)
            head.prev = nowy;
        head = nowy;
        if (tail == null)
            tail = nowy;
    }
    public void Usun(int wartosc)
    {
        DNode aktualny = head;
        while (aktualny != null && aktualny.wartosc != wartosc)
            aktualny = aktualny.next;
        if (aktualny != null)
        {
            if (aktualny.prev != null)
                aktualny.prev.next = aktualny.next;
            else
                head = aktualny.next;
            if (aktualny.next != null)
                aktualny.next.prev = aktualny.prev;
            else
                tail = aktualny.prev;
        }
    }
    public DNode Odczytaj(int indeks)
    {
        DNode aktualny = head;
        int licznik = 0;
        while (aktualny != null)
        {
            if (licznik == indeks)
                return aktualny;
            licznik++;
            aktualny = aktualny.next;
        }
        return null;
    }
}
```
## 43. Szyfr przestawieniowy (Transposition Cipher)
Zamienia kolejność liter według określonego klucza (tutaj prosty przykład: odwracanie tekstu).
Szyfr przestawieniowy (ang. transposition cipher) to rodzaj szyfru klasycznego, w którym bezpieczeństwo opiera się na zmianie kolejności liter w wiadomości, a nie na ich zamianie na inne znaki. Oznacza to, że szyfruje się tekst, przemieszczając jego znaki według określonego klucza – nie zamienia się liter na inne, tylko zmienia ich pozycję.



```csharp
string SzyfrPrzestawieniowy(string tekst)
{
    char[] szyfr = new char[tekst.Length];
    for (int i = 0; i < tekst.Length; i++)
        szyfr[i] = tekst[tekst.Length - 1 - i];
    return new string(szyfr);
}
```

*Możesz użyć własnego klucza permutacji, np. tablicy int[] klucz gdzie klucz[i] to nowa pozycja znaku tekst[i].*

---

## 44. Szyfr Cezara (Caesar Cipher)
Przesuwa każdą literę o ustaloną liczbę pozycji w alfabecie (domyślnie 3).

```csharp
string SzyfrCezara(string tekst, int przesuniecie)
{
    char[] szyfr = new char[tekst.Length];
    for (int i = 0; i < tekst.Length; i++)
    {
        char c = tekst[i];
        if (c >= 'A' && c <= 'Z')
            szyfr[i] = (char)('A' + (c - 'A' + przesuniecie + 26) % 26);
        else if (c >= 'a' && c <= 'z')
            szyfr[i] = (char)('a' + (c - 'a' + przesuniecie + 26) % 26);
        else
            szyfr[i] = c;
    }
    return new string(szyfr);
}
```
*Do odszyfrowania podaj przesunięcie ujemne.*

## 45. Tworzenie klas i obiektów

**Klasa** to szablon (model) opisujący strukturę i zachowanie obiektów. Klasa określa jakie dane (pola, właściwości) i funkcje (metody) będą miały jej obiekty.

**Obiekt** to instancja klasy, czyli konkretny „egzemplarz” posiadający własne wartości pól.

Przykład:
```csharp
class Osoba
{
    public string Imie;
    public int Wiek;
}

void PrzykladObiektu()
{
    Osoba osoba = new Osoba(); // tworzenie obiektu
    osoba.Imie = "Jan";
    osoba.Wiek = 30;
}
```
- `Osoba` to klasa.
- `osoba` to obiekt klasy `Osoba`.

---

## 46. Pola prywatne i publiczne, enkapsulacja

**Pole** to zmienna zdefiniowana w klasie. Może być:
- **publiczne** – dostępne z zewnątrz,
- **prywatne** – dostępne tylko wewnątrz klasy.

**Enkapsulacja** (hermetyzacja) polega na ukrywaniu implementacji klasy przed użytkownikiem, udostępniając tylko niezbędne informacje i metody.

Przykład:
```csharp
class KontoBankowe
{
    private double saldo;     // pole prywatne
    public string Wlasciciel; // pole publiczne

    public void Wplac(double kwota)
    {
        saldo += kwota;
    }

    public double PobierzSaldo()
    {
        return saldo;
    }
}
```
- `saldo` jest polem prywatnym – nie można go zmienić bezpośrednio, tylko przez metody klasy.
- `Wlasciciel` jest polem publicznym – można go odczytać i zmienić z zewnątrz.

---

## 47. Konstruktor i destruktor

**Konstruktor** – specjalna metoda wywoływana automatycznie przy tworzeniu obiektu. Służy do inicjalizacji pól.

**Destruktor** – metoda wywoływana przy usuwaniu obiektu z pamięci („sprzątanie” zasobów, np. zamykanie plików).

Przykład:
```csharp
class Samochod
{
    public string Marka;

    public Samochod(string marka) // konstruktor
    {
        Marka = marka;
    }

    ~Samochod() // destruktor
    {
        // Tutaj można np. zamykać pliki, zwalniać zasoby
    }
}
```

**Uwaga:**  
- W C# destruktory są wywoływane przez „garbage collector” (GC), nie masz nad nimi pełnej kontroli.
- Używaj destruktora tylko do zwalniania niezarządzanych zasobów (np. uchwyty do plików, połączenia z bazą).
- Konstruktor możesz przeciążać – możesz mieć kilka wersji o różnych parametrach.

---

## 48. Dziedziczenie proste

**Dziedziczenie** pozwala tworzyć nową klasę na podstawie istniejącej, przejmując jej pola i metody.

Przykład:
```csharp
class Zwierze
{
    public string Gatunek;
    public void WydajDzwiek() { }
}

class Pies : Zwierze // Pies dziedziczy po Zwierze
{
    public void Szczekaj()
    {
        WydajDzwiek(); // metoda odziedziczona
    }
}
```
- `Pies` dziedziczy wszystko z `Zwierze` i może mieć swoje dodatkowe metody.

---

## 49. Polimorfizm i metody wirtualne

**Polimorfizm** pozwala używać różnych klas w ten sam sposób, jeśli dziedziczą po tej samej klasie bazowej.

**Metoda wirtualna** (`virtual`) – daje możliwość nadpisania zachowania w klasie pochodnej przez słowo kluczowe `override`.

Przykład:
```csharp
class Zwierze
{
    public virtual void WydajDzwiek()
    {
        Console.WriteLine("Nieznany dźwięk");
    }
}

class Kot : Zwierze
{
    public override void WydajDzwiek()
    {
        Console.WriteLine("Miau");
    }
}

class Pies : Zwierze
{
    public override void WydajDzwiek()
    {
        Console.WriteLine("Hau");
    }
}

void PolimorfizmPrzyklad()
{
    Zwierze z1 = new Kot();
    Zwierze z2 = new Pies();
    z1.WydajDzwiek(); // Miau
    z2.WydajDzwiek(); // Hau
}
```
- `virtual` oznacza, że metoda może być zmieniona w klasie dziedziczącej (`override`).
- Polimorfizm działa, gdy używasz typów bazowych do przechowywania obiektów klas pochodnych.

---

## 50. Statyczne pola/metody

**Statyczne pole/metoda** należy do klasy, a nie do konkretnego obiektu.  
Możesz je wywołać bez tworzenia obiektu.

Przykład:
```csharp
class Licznik
{
    public static int IleObiektow = 0; // statyczne pole

    public Licznik()
    {
        IleObiektow++;
    }

    public static void PokazLiczbeObiektow() // statyczna metoda
    {
        Console.WriteLine(IleObiektow);
    }
}
```
- `Licznik.IleObiektow` oraz `Licznik.PokazLiczbeObiektow()` możesz wywoływać bez tworzenia obiektu.
- Statyczne pola/metody służą do przechowywania lub operowania na danych wspólnych dla wszystkich obiektów danej klasy (np. licznik utworzonych obiektów).

---

### Podsumowanie pojęć:

- **Klasa:** szablon opisujący strukturę i zachowanie obiektów.
- **Obiekt:** instancja klasy.
- **Pole:** zmienna w klasie.
- **Metoda:** funkcja w klasie.
- **Konstruktor:** inicjalizuje obiekt.
- **Destruktor:** sprząta po obiekcie (rzadko używany w C#).
- **Pola publiczne/prywatne:** dostępność z zewnątrz.
- **Enkapsulacja:** ukrywanie szczegółów implementacji.
- **Dziedziczenie:** tworzenie klasy na bazie innej.
- **Polimorfizm:** różne klasy mogą być traktowane jak jedna (typ bazowy).
- **Metody wirtualne:** mogą być nadpisane w klasie pochodnej.
- **Pola/metody statyczne:** należą do klasy, nie do obiektu.


## 51. Odczytywanie i zapisywanie pliku (File Read/Write)

### Odczyt wszystkich linii z pliku tekstowego

```csharp
string[] OdczytajPlik(string sciezka)
{
    return File.ReadAllLines(sciezka);
}
```

### Zapis tablicy stringów do pliku (każdy element jako osobna linia)

```csharp
void ZapiszDoPliku(string sciezka, string[] linie)
{
    File.WriteAllLines(sciezka, linie);
}
```

**Jak to działa?**
- `File.ReadAllLines("dane.txt")` zwraca tablicę wszystkich linii z pliku.
- `File.WriteAllLines("wynik.txt", linie)` zapisuje każdą linię do pliku, nadpisując plik o podanej nazwie.

**Przykładowe użycie:**
```csharp
string[] tekst = OdczytajPlik("dane.txt");
ZapiszDoPliku("wynik.txt", tekst);
```

**Dodatkowe informacje:**
- Obie funkcje są w klasie `System.IO.File` (dodaj `using System.IO;` na początku pliku).
- Jeśli plik nie istnieje, `ReadAllLines` zgłosi wyjątek – obsłuż to przez `try-catch` jeśli chcesz zabezpieczyć program.
- `WriteAllLines` utworzy plik jeśli go nie ma, albo nadpisze, jeśli jest.

---
## UNIT TESTY W C#

1) Jak dodać projekt testowy (GUI) (Projekt testowy dodajemy do gotowego projektu)
- Otwórz solution w Visual Studio.
- Prawy klik na Solution → Add → New Project...
- Wyszukaj "mstest" → wybierz "MSTest Test Project" → Next → nazwij np. MyApp.Tests → Create. !!PAMIETAJ ŻE WERSJA NET TESTU I PROJEKTU MUSI SIĘ ZGADZAĆ!!
- W projekcie testowym prawy klik Dependencies/References → Add Project Reference → zaznacz projekt aplikacji → OK.

2) Co musi być w projekcie testowym (nuget)(powinno być automatycznie w vs code czyli można pominąć)
Szablon zwykle dodaje:
- Microsoft.NET.Test.Sdk
- MSTest.TestAdapter
- MSTest.TestFramework

Jeśli brak — prawy klik na projekt → Manage NuGet Packages → Browse → zainstaluj powyższe.


Przykłady kodu:

```csharp
// MyApp/Calculator.cs
namespace MyApp;
public class Calculator
{
    public int Add(int a, int b){
       return a + b;
    }

    public int Divide(int a, int b)
    {
        if (b == 0) throw new System.DivideByZeroException();
        return a / b;
    }
}
```

```csharp
// MyApp.Tests/CalculatorTests.cs
using Microsoft.VisualStudio.TestTools.UnitTesting;
using MyApp;
using System;

namespace MyApp.Tests;

[TestClass]
public class CalculatorTests
{
    [TestMethod]
    public void Add_TwoNumbers_ReturnsSum()
    {
        // Arrange
        var calc = new Calculator();
        // Act
        var result = calc.Add(2, 3);
        // Assert
        Assert.AreEqual(5, result);
    }

    [TestMethod]
    public void Divide_ByZero_Throws()
    {
        var calc = new Calculator();
        Assert.ThrowsException<DivideByZeroException>(() => calc.Divide(5, 0));
    }
}
```

4) Uruchamianie i debug (Visual Studio)
- Otwórz Test → Test Explorer.
- Kliknij Run All albo kliknij prawym na pojedynczy test → Run/Debug Selected Tests.
- Aby debugować: ustaw breakpoint i wybierz Debug Selected Tests.

5) Najczęstsze błędy i szybkie naprawy
-
- Testy nie są wykrywane w Test Explorer
  - Sprawdź, że w projekcie testowym są pakiety: Microsoft.NET.Test.Sdk, MSTest.TestAdapter, MSTest.TestFramework.
  - Sprawdź TargetFramework (niektóre kombinacje mogą być nieobsługiwane). Ustaw taki sam lub kompatybilny framework jak projekt aplikacji.
  - Rebuild Solution, odśwież Test Explorer, zrestartuj Visual Studio jeśli trzeba.

- Błąd: nie widzi klas/metod z projektu aplikacji
  - Upewnij się, że dodałeś Project Reference (Add → Reference → Projects). Nie dodawaj ręcznie plików DLL z bin\.

- Błędy kompilacji w teście
  - Sprawdź komunikaty kompilatora (Error List). Często brak importu namespace lub niezgodność wersji pakietów.
  - Upewnij się, że testowy csproj targetuje zgodny framework i że ProjectReference ścieżka jest poprawna.

- Test rzuca wyjątkiem zamiast asercji
  - Sprawdź stack trace w Test Explorer → kliknij wynik testu → zobacz output.
  - Użyj Assert.ThrowsException<T>() do testowania wyjątków.

- Problem z debugowaniem (breakpointy nie łapią)
  - Upewnij się, że konfiguracja jest Debug (nie Release).
  - Rebuild, usuń pliki bin/obj jeśli podejrzane.
  - Czasami Visual Studio wymaga restartu.
  
- Test nie działa i nie wiadomo dlaczego
  - Upewnij się, że wersja .NET testu oraz projektu jest taka sama.

6) Przydatne krótkie wskazówki (pigułka)
- Struktura testu: Arrange — Act — Assert.
- Jeden scenariusz = jeden test.


(jak by coś nie działało totalnie to tutaj jeszcze xml dla csproj jak wygląda i co musi być)
```xml
<!-- MyApp.Tests/MyApp.Tests.csproj -->
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net7.0</TargetFramework> <!-- dopasuj do projektu -->
    <IsPackable>false</IsPackable>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="17.*" />
    <PackageReference Include="MSTest.TestAdapter" Version="2.*" />
    <PackageReference Include="MSTest.TestFramework" Version="2.*" />
  </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="..\MyApp\MyApp.csproj" />
  </ItemGroup>
</Project>
```
