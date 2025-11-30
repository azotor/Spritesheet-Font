# Spritesheet Font
Generowanie tekstu na podstawie czicionki w pliku z duszkami.
![Aplikacja](screen.png)

## Technologie
- Python
- PyGame

## Duszki
Znaki wchodzące w skład czcionki należy zapisać w pliku w formacie `*.png` w katalogu `Assets/Fonts`. Znaki w pliku znajdują się w siatce, gdzie w każdym pojedynczym polu siatki znajduje się jeden znak.

<figure>
  <figcaption>fontmain.png</figcaption>
  <img src="Assets/Fonts/fontmain.png" alt="fontmain.png">
</figure>

<figure>
  <figcaption>fontlight.png</figcaption>
  <img src="Assets/Fonts/fontlight.png" alt="fontlight.png">
</figure>

## Klasa `Font`

### Konstruktor

```python
__init__(
    self,
    font: str = "fontlight",
    width: int = 7,
    height: int = 8,
    scale: int = 1,
    alphabet: str = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ!?",.+-=:;$%&'
):
```

argumenty":
- `font` - nazwa pliku z czcionką ( bez formatu pliku ), domyślna czcionka `fontlight`
- `width` - szerokość znaku w pliku z czionką, domyślnie `7`
- `height` - wysokość znaku w pliku z czionką, domyślnie `8`
- `scale` - przeskalowanie czionki, domyślnie `1` - oryginalny rozmiar
- `alphabet` - ciąg znakowy z domyślnym alfabetem, kolejność znakó musi odpowiadać kolejnośći znaków w pliku graficznym od lewej do prawej, wiersz po wierszu, domyślny alfabet `0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ!?",.+-=:;$%&`

### Pobranie Surface'a z napisem

```python
getByWidth(
    self,
    message: str,
    width: int = 0
):
```

argumenty:
- `message` - tekst do wygenerowania,
- `width` - opcjonalny argument, szerokość Surface'a wynikowego z tekstem, domyślnie `0` rozmiar Surface'a tekstu nie będzie ograniczony

wynik:
- `Surface` - zwrócona powierzchnia z wygenerowanym tekstem, powierzchnia nie jest domyślnie umieszczona w głównym oknie aplikacji

### Wygenerowanie tesktu z opcjonalną szerokością powierzchni i umieszczenie na głównym ekranie

```python
render(
    self,
    message: str,
    pos,
    align = ( -1, -1 ),
    width:int = 0
):
```

argumenty:
- `message` - tekst do wygenerowania,
- `pos` - tuple dwóch elementów typu `int` określających położenie powierzchni z tekstem,
- `align` - tuple dwóch elementów typu `int` określających położenie powierzchni względem argumentu `pos`, domyślnie `( -1, -1 )` gdzie pierwszy element określa wyrównanie w pionie, a drugi w poziomie, wartości dopuszczalne: `-1`, `0`, `1`,
- `width` - opcjonalny argument, szerokość Surface'a wynikowego z tekstem, domyślnie `0` rozmiar Surface'a tekstu nie będzie ograniczony

<img src="align.png" alt="Położenie powierzhcni" width="300">

wynik:
umieszczenie na ekranie głównym powierzchni z wygenerowanym tekstem na współrzędnych określonych w argumencie `pos`

### Wygenerowanie tekstu z opcjonalną ilością znaków w linii i umieszczenie na głównym ekranie

```python
renderByGridsX(
    self,
    message: str,
    pos,
    align = ( -1, -1 ),
    gridsX:int = 0
):
```

argumenty:
jak wyżej z tym że zamiast `width` jest `gridsX`, który określa ilość znaków w linii powierzchni, domyślnie `0` cały tekst będzie wygenerowany w jednej linii

wynik:
umieszczenie na ekranie głównym powierzchni z wygenerowanym tekstem na współrzędnych określonych w argumencie `pos`

## Jak użyć
Skrypt korzysta z klas `Asset` oraz `Sprites`. Klasa `Asset` wczytuje pliki z katalogu `Assets`, klasa `Sprites` tnie plik graficzny na pojedyczne duszki i umieszcza je w tablicy.

### Import klasy `Font`
```python
from App.Font import Font
```

### Utworzenie obiektu `Font`
```python
myDefaultFont = Font()

myDefaultFontScale = Font( scale = 3 )

myOwnFont = Font(
    font = 'fontmain',
    width = 10,
    height = 10,
    scale = 3,
    alphabet = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
)
```

### Generowanie tekstu

```python
myDefaultFont.render(
    message = "ACCEPT CANCEL EXIT",
    pos = ( 20, 20 )
)

myDefaultFontScale.render(
    message = "HELLO WORLD",
    pos = ( 100, 100 )
)

myOwnFont.render(
    message = "HAPPY NEW YEAR 2024",
    pos = ( 100, 150 )
)

myDefaultFontScale.render(
    message = "MY NAME IS...",
    pos = ( 200, 250 ),
    align = ( 0, 0 ),
    width = 200
)

myOwnFont.renderByGridsX(
    message = "ABCDEFGHIJKL",
    pos = ( 400, 300 ),
    align = ( 0, -1 ),
    gridsX = 3
)

myDefaultFontScale.renderByGridsX(
    message = "ABCDEFGHIJKL",
    pos = ( 500, 300 ),
    align = ( 0, -1 ),
    gridsX = 4
)
```

![Aplikacja](screen2.png)
