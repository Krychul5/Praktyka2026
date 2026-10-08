# Tydzień 2 – interakcje, formularz, galeria i framework

W tym tygodniu dodasz zachowanie w JavaScript, przygotujesz formularz kontaktowy, zoptymalizujesz zdjęcia i świadomie wykorzystasz Bootstrap. Na koniec wykonasz audyt frontendu.

## Dzień 6 – pierwsze interakcje w JavaScript

Gałąź: `day-06-javascript`

### Cel

Nauczyć się wybierać elementy strony, reagować na zdarzenia i zmieniać interfejs bez przeładowania dokumentu.

### Co warto wiedzieć

JavaScript w przeglądarce może korzystać z DOM, czyli obiektowej reprezentacji dokumentu HTML. Zdarzenie `click` występuje po kliknięciu, `input` po zmianie wartości pola, a `submit` przy próbie wysłania formularza.

### Instrukcja krok po kroku

1. Utwórz `assets/js/main.js`.
2. Podłącz skrypt do każdej potrzebnej podstrony z atrybutem `defer`.
3. Otwórz konsolę przeglądarki i upewnij się, że plik jest ładowany bez błędu 404.
4. Wybierz element za pomocą `querySelector`.
5. Dodaj pierwszą użyteczną interakcję, np. przycisk „wróć na górę” pojawiający się po przewinięciu.
6. Dodaj drugą interakcję, np. rozwijanie odpowiedzi FAQ.
7. Podziel kod na niewielkie funkcje o nazwach opisujących działanie.
8. Sprawdź zachowanie, gdy oczekiwanego elementu nie ma na danej podstronie.
9. Sprawdź obsługę klawiaturą.
10. Usuń pomocnicze `console.log`, które nie są już potrzebne.

### Krótki przykład obsługi kliknięcia

```js
const exampleButton = document.querySelector('[data-example-button]');

if (exampleButton) {
  exampleButton.addEventListener('click', () => {
    // W tym miejscu wykonaj potrzebną zmianę.
  });
}
```

Warunek `if` zapobiega błędowi na podstronie, na której nie ma wskazanego przycisku. Użyj własnych nazw i dodaj rzeczywiste zachowanie.

### Przykład dobrego podziału pracy

Zamiast jednej funkcji `doEverything()` wykonującej kilkadziesiąt czynności użyj nazw wskazujących zamiar, np.:

- `setupBackToTopButton()`;
- `toggleFaqItem()`;
- `updateMenuState()`.

### Typowe błędy

- Skrypt jest wykonywany przed utworzeniem elementów HTML.
- `querySelector` zwraca `null`, a kod próbuje od razu wywołać metodę.
- Kod polega wyłącznie na zmianach stylu zapisanych bezpośrednio w JavaScript; zwykle lepiej przełączać klasę CSS.
- Element wyglądający jak przycisk jest zwykłym `div` i nie działa klawiaturą.
- Konsola zawiera błędy, które są ignorowane.

### Co oddajesz

- plik `main.js`;
- co najmniej dwie sensowne interakcje;
- opis sposobu sprawdzenia każdej interakcji.

### Gotowe, gdy

- [ ] Konsola nie pokazuje błędów JavaScript.
- [ ] Interakcje działają myszą i klawiaturą.
- [ ] Kod jest podzielony na czytelne funkcje.
- [ ] Brak elementu na podstronie nie powoduje awarii całego skryptu.
- [ ] Interakcje mają wartość dla użytkownika, a nie są tylko ozdobą.

---

## Dzień 7 – formularz i walidacja po stronie przeglądarki

Gałąź: `day-07-formularz`

### Cel

Zbudować dostępny formularz oraz wyświetlać zrozumiałe komunikaty przed wysłaniem niepoprawnych danych.

### Co warto wiedzieć

Walidacja w JavaScript poprawia wygodę użytkownika, ale nie zapewnia bezpieczeństwa. W trzecim tygodniu te same dane sprawdzisz ponownie w PHP, ponieważ kod w przeglądarce można wyłączyć lub ominąć.

### Pola obowiązkowe

- imię;
- adres e-mail;
- temat wiadomości;
- wiadomość;
- zgoda wymagana do wysłania danych.

Nie zbieraj danych, których projekt nie potrzebuje.

### Instrukcja krok po kroku

1. Utwórz formularz na stronie kontaktowej.
2. Dla każdego pola dodaj widoczną etykietę `label` połączoną z polem przez `for` oraz `id`.
3. Użyj odpowiednich typów, np. `type="email"` dla adresu e-mail.
4. Dodaj atrybuty `required`, `minlength` i `maxlength` tam, gdzie mają sens.
5. Dodaj miejsce na komunikat błędu bezpośrednio obok pola.
6. W JavaScript przechwyć zdarzenie `submit`.
7. Odczytaj wartości i usuń zbędne spacje z początku i końca.
8. Sprawdź każde pole osobno.
9. Jeśli występują błędy, zatrzymaj wysłanie i ustaw fokus na pierwszym niepoprawnym polu.
10. Po poprawnej walidacji pokaż komunikat demonstracyjny. Na tym etapie dane nie są jeszcze zapisywane.
11. Przetestuj formularz klawiaturą.

### Przykład dostępnej pary etykieta–pole–błąd

```html
<label for="email">Adres e-mail</label>
<input
  id="email"
  name="email"
  type="email"
  required
  aria-describedby="email-error"
>
<p id="email-error" class="field-error" aria-live="polite"></p>
```

Komunikat powinien mówić, co poprawić:

> Wpisz adres e-mail w formacie nazwa@domena.pl.

Zbyt ogólny komunikat:

> Błąd formularza.

### Przypadki do sprawdzenia

- wszystkie pola puste;
- e-mail bez znaku `@`;
- wiadomość zawierająca tylko spacje;
- bardzo długa wiadomość;
- brak zaznaczonej zgody;
- wszystkie dane poprawne;
- polskie znaki i apostrof w treści.

### Typowe błędy

- Etykieta istnieje tylko jako placeholder, który znika po rozpoczęciu pisania.
- Wszystkie błędy są pokazane daleko od pól.
- Czerwone obramowanie jest jedyną informacją o błędzie.
- Formularz czyści poprawne wartości po jednym błędzie.
- Wyrażenie regularne do e-maila jest przesadnie skomplikowane.
- Przycisk wysłania nie ma czytelnej treści.

### Co oddajesz

- dostępny formularz;
- walidację JavaScript;
- listę sprawdzonych przypadków w opisie Pull Requesta.

### Gotowe, gdy

- [ ] Każde pole ma widoczną etykietę.
- [ ] Komunikaty wskazują konkretne rozwiązanie.
- [ ] Fokus trafia na pierwsze błędne pole.
- [ ] Formularz można obsłużyć bez myszy.
- [ ] Poprawne dane przechodzą walidację.

---

## Dzień 8 – przygotowanie zdjęć i interaktywna galeria

Gałąź: `day-08-galeria`

### Cel

Przygotować obrazy do internetu oraz stworzyć galerię, którą można filtrować według kategorii.

### Co warto wiedzieć

Zdjęcie prosto z aparatu może mieć kilka tysięcy pikseli i wiele megabajtów. Wyświetlanie go jako małej miniatury nadal wymaga pobrania całego dużego pliku. Dlatego obrazy należy zmniejszyć i skompresować przed publikacją.

### Instrukcja krok po kroku

1. Ustal, czy masz prawo opublikować każde zdjęcie. Gdy używasz zdjęć testowych, zapisz źródło i licencję.
2. Utwórz `docs/MATERIALY.md` i zapisz źródła obrazów, ikon oraz fontów.
3. Wybierz 8–12 zdjęć pasujących do projektu.
4. Usuń niepotrzebne dane lokalizacyjne z fotografii, jeśli takie występują.
5. Przytnij zdjęcia do spójnych proporcji miniaturek.
6. Zmniejsz wymiary do realnej wielkości używanej na stronie. Duży obraz prezentacyjny zwykle nie potrzebuje szerokości zdjęcia z aparatu.
7. Zapisz obrazy jako WebP albo dobrze skompresowany JPEG/PNG, zależnie od zawartości.
8. Nadaj nazwy opisowe, np. `montaz-kuchni-01.webp`, a nie `IMG_8452.JPG`.
9. Zbuduj galerię w HTML. Każdy element powinien mieć kategorię w atrybucie `data-category`.
10. Dodaj przyciski: „Wszystkie” i przynajmniej dwie kategorie.
11. W JavaScript pokaż lub ukryj elementy zależnie od wybranej kategorii.
12. Oznacz aktywny filtr również w sposób dostępny dla technologii asystujących.
13. Dodaj `loading="lazy"` do obrazów znajdujących się poza pierwszym widokiem.

### Przykład elementu galerii

```html
<article class="gallery-item" data-category="wnetrza">
  <img
    src="assets/images/realizacja-wnetrze-01.webp"
    alt="Jasna kuchnia po zakończonym remoncie"
    width="640"
    height="480"
    loading="lazy"
  >
  <h2>Remont kuchni</h2>
</article>
```

Wartości `width` i `height` pomagają przeglądarce zarezerwować miejsce przed pobraniem obrazu. Wstaw rzeczywiste proporcje swojego pliku.

### Przykładowy algorytm filtrowania

1. Po kliknięciu przycisku odczytaj jego wybraną kategorię.
2. Przejdź po wszystkich elementach galerii.
3. Jeśli wybrano „wszystkie” albo kategoria elementu pasuje, pokaż element.
4. W przeciwnym przypadku ukryj element.
5. Zaktualizuj stan aktywnego przycisku.

Najpierw spróbuj zapisać ten algorytm samodzielnie. Dopiero później przełóż go na JavaScript.

### Typowe błędy

- Zdjęcia ważą kilka megabajtów każde.
- Miniatury mają różne proporcje i powodują skakanie układu.
- Obrazy nie mają wymiarów ani opisów alternatywnych.
- Filtr działa tylko raz albo po każdym kliknięciu duplikuje elementy.
- Ukryty element pozostaje dostępny dla fokusu klawiatury.
- Użyte zdjęcia nie mają znanego źródła lub prawa publikacji.

### Co oddajesz

- zoptymalizowane obrazy;
- plik `docs/MATERIALY.md`;
- responsywną galerię z filtrowaniem;
- porównanie rozmiaru co najmniej jednego obrazu przed i po optymalizacji.

### Gotowe, gdy

- [ ] Każdy obraz ma znane źródło i prawo użycia.
- [ ] Pliki mają opisowe nazwy i odpowiednie rozmiary.
- [ ] Galeria dobrze wygląda na telefonie i komputerze.
- [ ] Wszystkie filtry działają wielokrotnie.
- [ ] Aktywny filtr jest wyraźnie oznaczony.

---

## Dzień 9 – świadome wykorzystanie Bootstrap

Gałąź: `day-09-bootstrap`

### Cel

Poznać framework CSS i wykorzystać jego gotowe rozwiązania bez utraty własnego projektu wizualnego.

### Co warto wiedzieć

Framework dostarcza sprawdzone klasy i komponenty. Nie zwalnia jednak z rozumienia HTML, CSS ani dostępności. Przed dodaniem komponentu przeczytaj jego dokumentację i sprawdź przykład w używanej wersji Bootstrap.

### Instrukcja krok po kroku

1. Ustal z opiekunem wersję Bootstrap i sposób dołączenia.
2. Jeśli używasz CDN, zapisz źródło oraz upewnij się, że projekt może wymagać połączenia z internetem. Jeśli zasoby mają być lokalne, umieść je w odpowiednim katalogu.
3. Przeczytaj dokumentację siatki, breakpointów i wybranych komponentów.
4. Wybierz miejsca, w których framework naprawdę pomoże. Przykładowo: układ kart, nawigacja, formularz, modal lub komunikat.
5. Zastosuj siatkę Bootstrap przynajmniej w jednej sekcji.
6. Użyj co najmniej dwóch komponentów.
7. Dostosuj kolory, odstępy i wygląd do `docs/STYL.md`.
8. Nie dodawaj klasy wyłącznie dlatego, że istnieje. Każda powinna mieć cel.
9. Sprawdź obsługę klawiaturą, mały ekran i konsolę.
10. W `docs/TECHNOLOGIE.md` opisz, jaką wersję i które elementy wykorzystano.

### Przykład decyzji

> Do listy usług użyłem siatki Bootstrap, ponieważ automatycznie zmienia liczbę kolumn zależnie od szerokości. Własny CSS odpowiada za kolory i wygląd kart zgodny z makietą.

### Pytania przed użyciem komponentu

- Czy komponent pasuje do celu strony?
- Czy działa bez myszy?
- Czy wymaga dodatkowego JavaScript Bootstrap?
- Czy własny CSS nie nadpisuje go w przypadkowy sposób?
- Czy komponent nie zastępuje prostszego elementu HTML bez potrzeby?

### Typowe błędy

- Skopiowanie całego szablonu Bootstrap bez zrozumienia.
- Ładowanie dwóch różnych wersji frameworka.
- Użycie klas z dokumentacji innej wersji.
- Nadpisywanie stylów przez liczne `!important`.
- Dodanie ciężkiego komponentu dla drobnej ozdoby.
- Brak własnego wyglądu – strona wygląda jak przykład z dokumentacji.

### Co oddajesz

- Bootstrap podłączony w uzgodniony sposób;
- siatkę i co najmniej dwa komponenty;
- `docs/TECHNOLOGIE.md` z wersją i opisem zastosowania.

### Gotowe, gdy

- [ ] W repozytorium używana jest tylko jedna uzgodniona wersja Bootstrap.
- [ ] Framework upraszcza wybrane fragmenty.
- [ ] Strona nadal odpowiada przyjętej makiecie.
- [ ] Komponenty działają na małym ekranie i klawiaturą.
- [ ] Potrafisz wyjaśnić użyte klasy.

---

## Dzień 10 – audyt frontendu i wersja 0.2

Gałąź: `day-10-audyt`

### Cel

Sprawdzić jakość całej części widocznej w przeglądarce i nauczyć się dokumentować problemy zamiast poprawiać je przypadkowo.

### Instrukcja krok po kroku

1. Utwórz `docs/RAPORT_FRONTEND.md`.
2. Zapisz datę, przeglądarki, system i szerokości użyte podczas testu.
3. Sprawdź wszystkie podstrony w dwóch różnych przeglądarkach.
4. Sprawdź widoki 320 px, 768 px i 1440 px.
5. Użyj klawiatury do przejścia przez menu, formularz, galerię i inne interakcje.
6. Sprawdź konsolę na każdej podstronie.
7. Sprawdź zakładkę Network: błędy 404, bardzo ciężkie obrazy i niepotrzebne zasoby.
8. Dodaj unikalny `title` i opis meta do każdej podstrony.
9. Sprawdź hierarchię nagłówków i opisy alternatywne.
10. Wykonaj audyt w narzędziu przeglądarki, jeśli opiekun je wskaże. Nie skupiaj się tylko na wyniku liczbowym – przeczytaj zalecenia.
11. Podziel wykryte problemy na krytyczne, ważne i drobne.
12. Napraw najpierw problemy krytyczne i ważne.
13. Ponów test i zapisz rezultat po poprawkach.

### Przykładowy wpis w raporcie

| Problem | Priorytet | Jak odtworzyć | Rozwiązanie | Wynik po poprawce |
|---|---|---|---|---|
| Menu wychodzi poza ekran 320 px | wysoki | otworzyć stronę główną w szerokości 320 px | zmieniono układ elementów menu | poprawione |

### Przykładowe opisy meta

Dobry opis krótko wyjaśnia zawartość podstrony i jest dla niej unikalny. Nie upychaj w nim wielokrotnie tych samych słów kluczowych.

```html
<meta name="description" content="Poznaj zakres usług przykładowej firmy i wybierz rozwiązanie dopasowane do swoich potrzeb.">
```

Treść dopasuj do rzeczywistego projektu.

### Typowe błędy

- Testowana jest tylko strona główna.
- Wszystkie problemy otrzymują ten sam priorytet.
- Raport mówi „poprawiono responsywność”, ale nie wyjaśnia problemu.
- Ocena narzędzia automatycznego jest traktowana jako jedyny test.
- Po poprawce nie wykonuje się ponownego testu.

### Co oddajesz

- `docs/RAPORT_FRONTEND.md`;
- poprawki najważniejszych problemów;
- zestaw zrzutów dla głównych szerokości;
- Pull Request do drugiego punktu kontrolnego.

### Gotowe, gdy

- [ ] Wszystkie podstrony sprawdzono w dwóch przeglądarkach.
- [ ] Nie ma błędów 404 ani błędów JavaScript.
- [ ] Każda podstrona ma unikalny tytuł i opis.
- [ ] Problemy i poprawki są zapisane w raporcie.
- [ ] Opiekun zaakceptował drugi tydzień.

Po akceptacji opiekun może oznaczyć wersję tagiem `v0.2`.

