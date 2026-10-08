# Tydzień 1 – od pomysłu do responsywnej strony

W tym tygodniu poznasz potrzeby „klienta”, przygotujesz makiety i zbudujesz statyczną wersję strony. Statyczna oznacza, że treść znajduje się jeszcze bezpośrednio w plikach HTML i nie korzysta z bazy danych.

## Dzień 1 – analiza potrzeb i przygotowanie projektu

Gałąź: `day-01-analiza`

### Cel

Zrozumieć, dla kogo i po co powstaje strona. Dobra strona nie zaczyna się od kodowania, tylko od pytań i uporządkowania wymagań.

### Co warto wiedzieć

**Wymaganie funkcjonalne** mówi, co użytkownik może zrobić, np. „użytkownik może wysłać formularz kontaktowy”.

**Wymaganie niefunkcjonalne** opisuje jakość lub ograniczenie, np. „strona ma dobrze działać na telefonie” albo „czas ładowania powinien być krótki”.

### Instrukcja krok po kroku

1. Przeczytaj całe repozytorium, zwłaszcza `README.md` i `INSTRUKCJA_START.md`.
2. Skonfiguruj Git i utwórz gałąź `day-01-analiza`.
3. Ustal z opiekunem temat strony. Może to być np. firma remontowa, serwis rowerowy, restauracja albo fikcyjna firma usługowa.
4. Utwórz katalog `docs` i plik `docs/WYMAGANIA.md`.
5. Opisz krótko firmę oraz jej ofertę. Jeśli projekt jest fikcyjny, zaznacz to.
6. Określ przynajmniej dwie grupy odbiorców.
7. Zapisz główny cel strony oraz 3–5 celów pomocniczych.
8. Sporządź listę podstron i funkcji.
9. Podziel wymagania na `MUST` – obowiązkowe, `SHOULD` – ważne i `COULD` – dodatkowe.
10. Zapisz minimum pięć pytań do klienta.
11. Omów dokument z opiekunem i nanieś uwagi.

### Przykład – jak opisać wymaganie

Zamiast nieprecyzyjnego:

> Strona ma być ładna i nowoczesna.

napisz konkretniej:

> Strona korzysta z maksymalnie dwóch rodzin krojów pisma, ma spójną paletę 3–4 kolorów, czytelne odstępy i układ dostosowany do ekranu o szerokości 320 px.

Przykładowe pytania do klienta:

- Kto jest głównym odbiorcą strony?
- Jakie działanie użytkownik powinien wykonać najczęściej?
- Które elementy oferty są najważniejsze?
- Czy firma posiada logo, kolory, zdjęcia i prawa do ich publikacji?
- Jakie dane ma zbierać formularz kontaktowy?
- Kto będzie później aktualizować treści?

### Proponowana struktura pliku wymagań

```text
# Wymagania projektu
## Opis firmy
## Odbiorcy
## Cel strony
## Zakres MUST
## Zakres SHOULD
## Zakres COULD
## Lista podstron
## Pytania do klienta
## Ustalenia z opiekunem
```

### Typowe błędy

- Rozpoczynanie kodowania bez ustalenia zakresu.
- Wymagania typu „fajna strona”, których nie da się sprawdzić.
- Obiecanie zbyt wielu funkcji na 20 dni.
- Użycie prawdziwych danych osobowych w projekcie demonstracyjnym.
- Jeden commit wykonany dopiero na koniec dnia.

### Co oddajesz

- plik `docs/WYMAGANIA.md`;
- co najmniej trzy logiczne commity;
- Pull Request z krótkim podsumowaniem ustaleń.

### Gotowe, gdy

- [ ] Opisano temat i odbiorców strony.
- [ ] Cel strony jest konkretny.
- [ ] Zakres podzielono na MUST, SHOULD i COULD.
- [ ] Wymieniono podstrony i funkcje.
- [ ] Zapisano minimum pięć pytań do klienta.
- [ ] Opiekun zaakceptował zakres.

---

## Dzień 2 – mapa strony, makiety i identyfikacja wizualna

Gałąź: `day-02-makiety`

### Cel

Zaplanować strukturę i wygląd przed rozpoczęciem pisania HTML. Makieta nie musi być piękną grafiką – ma jasno pokazywać rozmieszczenie elementów.

### Co warto wiedzieć

**Mapa strony** pokazuje hierarchię podstron. **Wireframe**, czyli prosta makieta, przedstawia układ bez skupiania się na detalach graficznych.

Przykładowa mapa:

```text
Strona główna
├── Oferta
│   ├── Usługa A
│   └── Usługa B
├── O nas
├── Galeria
└── Kontakt
```

### Instrukcja krok po kroku

1. Utwórz gałąź `day-02-makiety` z aktualnej gałęzi `main`.
2. Na podstawie wymagań wykonaj mapę strony.
3. Dla każdej podstrony zapisz jej cel i najważniejszą akcję użytkownika.
4. Wykonaj makietę strony głównej w wersji desktopowej.
5. Wykonaj makietę tej samej strony dla telefonu.
6. Wykonaj makietę formularza kontaktowego albo oferty.
7. Wybierz paletę 3–4 kolorów. Sprawdź, czy tekst jest czytelny na tle.
8. Wybierz maksymalnie dwie rodziny kroju pisma lub użyj bezpiecznego zestawu systemowego.
9. Zapisz podstawowe zasady wyglądu w `docs/STYL.md`.
10. Wyeksportuj makiety do `docs/makiety/` jako PNG, SVG albo PDF.

### Elementy, które warto umieścić na makiecie strony głównej

- logo lub nazwa firmy;
- menu;
- główny nagłówek i przycisk działania, np. „Zobacz ofertę”;
- skrócona oferta;
- informacja budująca zaufanie;
- wybrane zdjęcia lub realizacje;
- dane kontaktowe i stopka.

### Przykład opisu decyzji

> Na telefonie karty oferty układają się w jednej kolumnie, aby tekst i przyciski nie były zbyt wąskie. Na ekranie komputera będą widoczne trzy karty w jednym rzędzie.

### Typowe błędy

- Projektowanie wyłącznie szerokiego widoku komputerowego.
- Zbyt dużo różnych kolorów i wielkości tekstu.
- Brak wyraźnego głównego działania.
- Tekst umieszczony na zdjęciu bez zapewnienia kontrastu.
- Kopiowanie wyglądu innej strony jeden do jednego.

### Co oddajesz

- mapę strony;
- minimum trzy makiety;
- plik `docs/STYL.md` z kolorami i typografią;
- Pull Request ze zrzutami makiet.

### Gotowe, gdy

- [ ] Każda planowana podstrona znajduje się na mapie.
- [ ] Makieta strony głównej ma wersję desktopową i mobilną.
- [ ] Widoczne są menu, treść główna i stopka.
- [ ] Paleta kolorów i typografia są opisane.
- [ ] Opiekun zaakceptował kierunek wizualny.

---

## Dzień 3 – struktura projektu i semantyczny HTML

Gałąź: `day-03-html`

### Cel

Zbudować wszystkie podstrony w HTML tak, aby treść miała logiczną strukturę nawet bez stylów CSS.

### Co warto wiedzieć

Semantyczny HTML używa elementów zgodnie z ich znaczeniem. `nav` oznacza nawigację, `main` główną treść, `article` samodzielny fragment, a `button` działanie. Element `div` jest pomocny, ale nie powinien zastępować wszystkich pozostałych elementów.

### Proponowana struktura katalogów

```text
projekt/
├── index.html
├── oferta.html
├── o-nas.html
├── galeria.html
├── kontakt.html
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
└── docs/
```

Nazwy plików zapisuj małymi literami, bez spacji i polskich znaków.

### Instrukcja krok po kroku

1. Utwórz strukturę katalogów.
2. Dodaj plik `index.html` oraz pozostałe podstrony wynikające z wymagań.
3. W każdym dokumencie dodaj `<!doctype html>`, język polski, kodowanie UTF-8 i ustawienie viewport.
4. Utwórz wspólny nagłówek z nazwą firmy i menu.
5. Utwórz jeden element `main` zawierający właściwą treść podstrony.
6. Dodaj wspólną stopkę.
7. Zbuduj poprawną hierarchię nagłówków. Zwykle każda podstrona ma jeden główny `h1`.
8. Dodaj link umożliwiający przejście do każdej podstrony.
9. Dodaj treści robocze. Nie używaj kilku stron przypadkowego tekstu `Lorem ipsum`, jeśli możesz opisać przykładową firmę.
10. Dodaj opisy alternatywne do obrazów niosących informację.
11. Sprawdź HTML w walidatorze wskazanym przez opiekuna.

### Minimalny przykład dokumentu

To tylko wzór struktury, a nie gotowa strona:

```html
<!doctype html>
<html lang="pl">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Oferta – Nazwa firmy</title>
  </head>
  <body>
    <header>
      <nav aria-label="Główna nawigacja">
        <!-- Tutaj dodaj listę odnośników -->
      </nav>
    </header>
    <main>
      <h1>Oferta</h1>
      <!-- Tutaj dodaj sekcje oferty -->
    </main>
    <footer><!-- Dane w stopce --></footer>
  </body>
</html>
```

### Wskazówki dotyczące obrazów

- Logo firmy: opis alternatywny może zawierać nazwę firmy.
- Zdjęcie realizacji: opisz krótko, co istotnego przedstawia.
- Dekoracyjny ornament: może mieć pusty `alt=""`.
- Nie rozpoczynaj każdego opisu od słów „zdjęcie przedstawia”. Czytnik ekranu i tak rozpoznaje obraz.

### Typowe błędy

- Kilka elementów `h1` bez uzasadnienia albo przeskok z `h1` do `h4`.
- Link bez treści, np. „kliknij tutaj”, który nie mówi dokąd prowadzi.
- Używanie elementu `button` do przejścia na inną stronę zamiast linku.
- Brak atrybutu `lang="pl"`.
- Ścieżki do obrazów działające tylko na komputerze autora.
- Wielokrotne identyczne wartości `id`.

### Co oddajesz

- kompletny szkielet wszystkich podstron;
- treści robocze i działające linki;
- wynik sprawdzenia walidatorem opisany w Pull Requeście.

### Gotowe, gdy

- [ ] Wszystkie podstrony istnieją i są połączone menu.
- [ ] Każda podstrona ma prawidłowy tytuł i jeden główny nagłówek.
- [ ] Użyto elementów semantycznych.
- [ ] Obrazy mają właściwe opisy alternatywne.
- [ ] Nie ma istotnych błędów walidacji HTML.

---

## Dzień 4 – CSS, układ i responsywność

Gałąź: `day-04-style`

### Cel

Zamienić poprawną strukturę HTML w czytelną, spójną i responsywną stronę.

### Co warto wiedzieć

Podejście **mobile first** oznacza, że najpierw przygotowujesz prosty układ dla małego ekranu, a później dodajesz reguły dla szerszych ekranów. Pomaga to uniknąć ściskania dużego projektu na telefonie.

### Instrukcja krok po kroku

1. Utwórz `assets/css/style.css` i podłącz go do każdej podstrony.
2. Na początku ustaw przewidywalny model pudełkowy dla elementów.
3. Zdefiniuj kolory, szerokość treści i podstawowe odstępy jako zmienne CSS.
4. Ustaw czytelny krój, wysokość linii i skalę nagłówków.
5. Ogranicz maksymalną szerokość głównej treści i wyśrodkuj ją.
6. Ostyluj nagłówek, menu, sekcje, karty, przyciski i stopkę.
7. Zbuduj układ kart za pomocą Grid lub Flexbox.
8. Dodaj co najmniej jeden breakpoint przez `@media`.
9. Sprawdź szerokości 320 px, 768 px i około 1440 px.
10. Dodaj widoczny styl `:focus-visible` dla linków i przycisków.
11. Sprawdź, czy tekst ma dobry kontrast i nic nie wychodzi poza ekran.

### Przykład zmiennych i kontenera

Nazwy i wartości dopasuj do własnego projektu:

```css
:root {
  --color-primary: #1f5f74;
  --color-text: #1d252c;
  --color-background: #ffffff;
  --space-sm: 0.5rem;
  --space-md: 1rem;
  --space-lg: 2rem;
  --content-width: 72rem;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

.container {
  width: min(100% - 2rem, var(--content-width));
  margin-inline: auto;
}
```

Przykład rozwinięcia układu na szerszym ekranie:

```css
.cards {
  display: grid;
  gap: 1rem;
}

@media (min-width: 48rem) {
  .cards {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

Nie przepisuj przykładu bezmyślnie. Sprawdź, czy nazwy klas pasują do Twojego HTML i czy trzy kolumny są właściwe dla treści.

### Typowe błędy

- Ustawianie stałej szerokości całej strony, np. `width: 1200px`.
- Dziesiątki przypadkowych wartości odstępów.
- Ukrywanie problemu za pomocą `overflow-x: hidden` zamiast znalezienia elementu wychodzącego poza ekran.
- Bardzo mała czcionka na telefonie.
- Usunięcie obramowania fokusu bez dodania własnego widocznego stylu.
- Rozciąganie obrazu przez ustawienie jednocześnie sztywnej szerokości i wysokości.

### Co oddajesz

- wspólny arkusz stylów;
- zrzuty ekranu dla 320 px, 768 px i widoku desktopowego;
- opis jednej decyzji dotyczącej responsywności w Pull Requeście.

### Gotowe, gdy

- [ ] Na ekranie 320 px nie ma poziomego przewijania.
- [ ] Treść nie jest nadmiernie rozciągnięta na dużym ekranie.
- [ ] Kolory i odstępy są spójne.
- [ ] Linki i przyciski mają widoczny fokus.
- [ ] Obrazy zachowują właściwe proporcje.

---

## Dzień 5 – dostępna nawigacja i pierwszy przegląd

Gałąź: `day-05-przeglad`

### Cel

Dokończyć statyczną wersję strony, poprawić nawigację i sprawdzić jakość całego pierwszego etapu.

### Instrukcja krok po kroku

1. Sprawdź, czy menu ma taką samą kolejność na każdej podstronie.
2. Wyróżnij bieżącą podstronę nie tylko kolorem, ale również np. podkreśleniem i atrybutem `aria-current="page"`.
3. Dodaj link „Przejdź do treści”, który pozwala użytkownikowi klawiatury ominąć menu.
4. Przejdź całą stronę używając wyłącznie klawisza `Tab`, `Shift+Tab` i `Enter`.
5. Sprawdź, czy kolejność fokusu jest logiczna.
6. Kliknij każdy link i usuń odnośniki prowadzące do błędu 404.
7. Sprawdź, czy każda podstrona ma unikalny tytuł w karcie przeglądarki.
8. Ponownie uruchom walidację HTML i CSS.
9. Sprawdź wygląd na telefonie i komputerze.
10. Poproś inną osobę o krótkie wykonanie zadania, np. „znajdź numer telefonu firmy”. Obserwuj, czy jest to łatwe.
11. Popraw wykryte problemy.
12. W Pull Requeście dodaj zrzuty ekranu i krótką listę wykonanych testów.

### Przykład oznaczenia bieżącej podstrony

```html
<a href="oferta.html" aria-current="page">Oferta</a>
```

Na pozostałych linkach nie dodawaj `aria-current`.

### Przykład linku pomijającego menu

```html
<a class="skip-link" href="#main-content">Przejdź do treści</a>
<main id="main-content">
```

Link może być niewidoczny bez fokusu, ale musi pojawić się po naciśnięciu `Tab`.

### Pytania do samokontroli

- Czy po wyłączeniu CSS treść nadal ma logiczną kolejność?
- Czy użytkownik wie, na której podstronie się znajduje?
- Czy przyciski wyglądają jak przyciski, a linki jak elementy możliwe do kliknięcia?
- Czy ważne informacje są łatwe do znalezienia?
- Czy strona nadaje się do użycia bez myszy?

### Typowe błędy

- Wyróżnienie aktywnej strony tylko delikatną zmianą koloru.
- Fokus niewidoczny na ciemnym tle.
- Menu działa tylko po najechaniu myszą.
- Tekst alternatywny powtarza podpis widoczny obok zdjęcia.
- Naprawienie jednego widoku kosztem innego.

### Co oddajesz

- kompletną statyczną wersję strony;
- informację o wykonanych testach;
- zrzuty widoku mobilnego i desktopowego;
- Pull Request do pierwszego punktu kontrolnego.

### Gotowe, gdy

- [ ] Wszystkie linki działają.
- [ ] Całą stronę można obsłużyć klawiaturą.
- [ ] Aktywna podstrona jest właściwie oznaczona.
- [ ] HTML i CSS nie mają istotnych błędów walidacji.
- [ ] Opiekun zaakceptował pierwszy tydzień.

Po akceptacji opiekun może oznaczyć wersję tagiem `v0.1`.

