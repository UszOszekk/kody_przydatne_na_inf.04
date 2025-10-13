# Obsługa plików w Windows Forms (C#)

Poniżej znajdziesz przykłady użycia plików w aplikacjach Windows Forms: zapisywanie, wczytywanie, odczyt oraz dodawanie plików multimedialnych (dźwięki, obrazy).

---

## 1. Jak dodać plik do projektu, żeby go odczytać?

- Dodaj plik (np. tekstowy, obraz, dźwięk) do projektu:
  1. W Solution Explorer kliknij prawym na projekt → "Add" → "Existing Item".
  2. Wybierz plik.
  3. Ustaw właściwość pliku:
     - `Copy to Output Directory` → `Copy always` lub `Copy if newer`
  4. Po kompilacji plik będzie w katalogu `bin\Debug` lub `bin\Release`.
- Odczyt pliku z projektu:  
  Użyj ścieżki np. `Application.StartupPath + "\\nazwa_pliku.txt"`

---

## 2. Zapisywanie tekstu do pliku

```csharp
using System.IO;

private void buttonZapisz_Click(object sender, EventArgs e)
{
    SaveFileDialog dlg = new SaveFileDialog();
    dlg.Filter = "Pliki tekstowe (*.txt)|*.txt|Wszystkie pliki (*.*)|*.*";
    if (dlg.ShowDialog() == DialogResult.OK)
    {
        File.WriteAllText(dlg.FileName, textBoxTekst.Text);
        MessageBox.Show("Zapisano!");
    }
}
```
- Zapisuje zawartość z `textBoxTekst` do wybranego pliku.

---

## 3. Wczytywanie pliku (wybór pliku + odczyt całości)

```csharp
private void buttonWczytaj_Click(object sender, EventArgs e)
{
    OpenFileDialog dlg = new OpenFileDialog();
    dlg.Filter = "Pliki tekstowe (*.txt)|*.txt|Wszystkie pliki (*.*)|*.*";
    if (dlg.ShowDialog() == DialogResult.OK)
    {
        string tekst = File.ReadAllText(dlg.FileName);
        textBoxTekst.Text = tekst;
        MessageBox.Show("Wczytano!");
    }
}
```
- Wczytuje cały plik do textBoxa.

---

## 4. Odczyt pliku linia po linii

```csharp
private void buttonOdczytajLinie_Click(object sender, EventArgs e)
{
    OpenFileDialog dlg = new OpenFileDialog();
    dlg.Filter = "Pliki tekstowe (*.txt)|*.txt|Wszystkie pliki (*.*)|*.*";
    if (dlg.ShowDialog() == DialogResult.OK)
    {
        string[] linie = File.ReadAllLines(dlg.FileName);
        listBoxLinie.Items.Clear();
        listBoxLinie.Items.AddRange(linie);
    }
}
```
- Wczytuje każdą linię do ListBoxa.

---

## 5. Dodawanie plików multimedialnych

### Obrazy

```csharp
using System.Drawing;

private void buttonObraz_Click(object sender, EventArgs e)
{
    OpenFileDialog dlg = new OpenFileDialog();
    dlg.Filter = "Pliki graficzne (*.jpg;*.png;*.bmp)|*.jpg;*.png;*.bmp";
    if (dlg.ShowDialog() == DialogResult.OK)
    {
        pictureBox1.Image = Image.FromFile(dlg.FileName);
    }
}
```
- Wyświetla obraz w PictureBox.

### Dźwięki (.wav)

```csharp
using System.Media;

private void buttonDzwiek_Click(object sender, EventArgs e)
{
    OpenFileDialog dlg = new OpenFileDialog();
    dlg.Filter = "Pliki dźwiękowe (*.wav)|*.wav";
    if (dlg.ShowDialog() == DialogResult.OK)
    {
        SoundPlayer player = new SoundPlayer(dlg.FileName);
        player.Play();
    }
}
```
- Odtwarza dźwięk .wav.

### Wideo

**Wideo (.avi, .wmv, .mp4) – bez dodatkowych bibliotek nie można bezpośrednio odtwarzać w Windows Forms.**
- Można otworzyć plik domyślnym programem systemu:
```csharp
System.Diagnostics.Process.Start("nazwa_pliku.mp4");
```

---

## 6. Przykładowe formaty plików

**Tekstowe:**  
- `.txt` – plik tekstowy
- `.csv` – dane tabelaryczne
- `.xml` – dane tekstowe w formacie XML

**Obrazy:**  
- `.jpg`, `.jpeg`, `.bmp`, `.png`, `.gif` – obsługiwane przez `Image.FromFile`

**Dźwięki:**  
- `.wav` – obsługiwane przez `SoundPlayer`
- `.mp3` – nieobsługiwane bez dodatkowej biblioteki

**Wideo:**  
- `.avi`, `.wmv`, `.mp4` – nieobsługiwane bez dodatkowej biblioteki

---

## 7. Odczyt pliku dodanego do projektu

```csharp
string path = Application.StartupPath + "\\nazwa_pliku.txt";
string tekst = File.ReadAllText(path);
```
- Odczyt pliku znajdującego się w katalogu projektu po kompilacji.

---

## 8. Obsługa plików binarnych (np. obraz, dowolny plik)

```csharp
// Odczyt binarny
byte[] dane = File.ReadAllBytes("plik.png");

// Zapis binarny
File.WriteAllBytes("kopiapliku.png", dane);
```

---

## 9. Wskazówki do projektu Windows Forms

- Dodaj kontrolki: Button, TextBox, ListBox, PictureBox
- Do kodu dodaj using(JAK NIE DZIAŁA POWINNO SAMO SIĘ DODAĆ):  
  `using System; using System.IO; using System.Drawing; using System.Media; using System.Windows.Forms;`