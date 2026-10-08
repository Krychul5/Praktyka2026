# Tydzień 4 – bezpieczeństwo, testy, dokumentacja i odbiór

W ostatnim tygodniu dokończysz panel, zabezpieczysz dostęp, przetestujesz cały projekt, usuniesz usterki i przygotujesz wersję końcową.

## Dzień 16 – usuwanie rekordów, logowanie i sesja

Gałąź: `day-16-logowanie`

### Cel

Dokończyć CRUD, wprowadzić bezpieczne logowanie i zablokować dostęp do panelu osobom niezalogowanym.

### Co warto wiedzieć

Hasła zapisuje się w postaci hasha utworzonego przez `password_hash`, a sprawdza przez `password_verify`. Nie szyfruj ich samodzielnie i nie używaj szybkich funkcji takich jak MD5 lub SHA-1 do przechowywania haseł.

Sesja PHP pozwala przechowywać po stronie serwera informację, że użytkownik został poprawnie zalogowany. Samo ukrycie linku do panelu nie zabezpiecza adresu.

### Część A – bezpieczne usuwanie

1. Dodaj przycisk „Usuń” na liście rekordów.
2. Wykonuj usuwanie wyłącznie metodą POST. Zwykłe wejście na adres metodą GET nie może usuwać danych.
3. Wyświetl jasne potwierdzenie wskazujące, który rekord zostanie usunięty.
4. Sprawdź identyfikator i istnienie rekordu.
5. Usuń rekord przez prepared statement.
6. Po operacji przekieruj na listę i wyświetl jednorazowy komunikat.
7. Sprawdź anulowanie oraz próbę usunięcia nieistniejącego rekordu.

### Część B – utworzenie użytkownika

1. Przygotuj lokalny skrypt jednorazowy lub uzgodniony seed tworzący użytkownika demonstracyjnego.
2. Wygeneruj hash funkcją `password_hash`.
3. W bazie zapisuj wyłącznie hash.
4. Nie umieszczaj prawdziwego hasła w repozytorium ani w skrypcie SQL.
5. Instrukcja może mówić użytkownikowi, jak samodzielnie ustawić hasło podczas instalacji.

Przykład generowania hasha w PHP:

```php
$hash = password_hash($password, PASSWORD_DEFAULT);
```

Nie wpisuj do kodu zmiennej `$password` z prawdziwym hasłem. Pobierz ją bezpiecznie w lokalnym narzędziu lub formularzu przygotowanym tylko do instalacji.

### Część C – logowanie i ochrona panelu

1. Utwórz formularz logowania z nazwą użytkownika lub e-mailem oraz hasłem.
2. Pobierz użytkownika przez prepared statement.
3. Sprawdź hasło przez `password_verify`.
4. Po udanym logowaniu rozpocznij sesję i zapisz minimalne informacje, np. ID użytkownika.
5. Po logowaniu odśwież identyfikator sesji.
6. Na początku każdej strony panelu sprawdź, czy sesja potwierdza zalogowanie.
7. Jeśli nie, przekieruj użytkownika do logowania.
8. Dodaj wylogowanie metodą POST, które usuwa dane sesji.
9. Użyj jednego ogólnego komunikatu dla błędnego loginu lub hasła, aby nie zdradzać, czy konto istnieje.
10. Uzgodnij z opiekunem dodanie tokena CSRF do formularzy zmieniających dane: dodawania, edycji, usuwania i wylogowania.

### Pseudokod logowania

```text
odczytaj login i hasło
znajdź użytkownika po loginie

jeżeli użytkownik istnieje i password_verify zwraca true:
    odśwież identyfikator sesji
    zapisz ID użytkownika w sesji
    przekieruj do panelu
w przeciwnym razie:
    pokaż ogólny komunikat błędu
```

### Przypadki testowe

- poprawny login i hasło;
- poprawny login, błędne hasło;
- nieistniejący login;
- puste pola;
- próba wejścia bezpośrednio na `admin/edit.php` bez logowania;
- odświeżenie strony po zalogowaniu;
- wylogowanie i próba powrotu przyciskiem przeglądarki;
- usuwanie metodą GET;
- usuwanie nieistniejącego ID.

### Typowe błędy

- Hasło albo jego kopia znajduje się w repozytorium.
- Do porównania hasła używane jest `===` zamiast `password_verify`.
- Zabezpieczona jest tylko strona główna panelu, ale `edit.php` nadal jest publiczna.
- Link GET usuwa rekord po samym otwarciu.
- Komunikat ujawnia, że konkretny login istnieje.
- Sesja jest uruchamiana po wysłaniu HTML do przeglądarki.

### Co oddajesz

- usuwanie metodą POST;
- logowanie oparte o hash hasła;
- ochronę każdej podstrony panelu;
- wylogowanie;
- listę wykonanych testów bezpieczeństwa.

### Gotowe, gdy

- [ ] W bazie nie ma jawnych haseł.
- [ ] Każda strona panelu sprawdza sesję.
- [ ] Niepoprawne dane nie zdradzają, czy użytkownik istnieje.
- [ ] Usuwanie nie działa metodą GET.
- [ ] Wylogowany użytkownik nie może wykonać operacji administracyjnej.

---

## Dzień 17 – plan testów i zgłaszanie usterek

Gałąź: `day-17-testy`

### Cel

Przetestować projekt systematycznie, zapisać wyniki i utworzyć listę usterek z priorytetami.

### Co warto wiedzieć

Przypadek testowy powinien być powtarzalny. Zawiera warunki początkowe, kroki, oczekiwany wynik i wynik rzeczywisty. „Kliknąłem i działa” nie wystarcza, ponieważ inna osoba nie wie, co dokładnie wykonano.

### Instrukcja krok po kroku

1. Utwórz `docs/TESTY.md`.
2. Zapisz środowisko: system, wersję PHP, bazę i przeglądarki.
3. Przygotuj bazę w znanym stanie, korzystając z danych demonstracyjnych.
4. Napisz przypadki testowe dla:
   - nawigacji;
   - responsywności;
   - filtrowania galerii;
   - walidacji formularza w JS i PHP;
   - zapisu wiadomości;
   - logowania i wylogowania;
   - listy, dodawania, edycji i usuwania;
   - nieistniejących rekordów;
   - ochrony panelu.
5. Uwzględnij dane poprawne, błędne i graniczne.
6. Wykonaj przypadki po kolei i zapisz rezultat.
7. Dla niepowodzenia utwórz zgłoszenie usterki.
8. Nadaj każdej usterce priorytet.
9. Dołącz zrzut ekranu albo treść komunikatu, jeżeli pomaga odtworzyć problem.
10. Nie naprawiaj wszystkiego natychmiast podczas testu. Najpierw zakończ badanie danego obszaru, aby zachować pełną listę.

### Szablon przypadku testowego

```text
ID: FORM-03
Nazwa: Odrzucenie niepoprawnego adresu e-mail
Warunki: strona kontaktowa jest otwarta, JavaScript jest włączony
Kroki:
1. Wpisz poprawne imię.
2. W polu e-mail wpisz „jan.example”.
3. Uzupełnij pozostałe pola poprawnie.
4. Naciśnij „Wyślij”.
Oczekiwany wynik: formularz nie zostaje wysłany, a przy polu e-mail pojawia się jasny komunikat.
Wynik rzeczywisty: ...
Status: zaliczony / niezaliczony
```

### Szablon usterki

```text
Tytuł: Po edycji usługi znika opis
Priorytet: wysoki
Środowisko: Firefox ..., PHP ...
Warunki: w bazie istnieje usługa testowa
Kroki odtworzenia:
1. Zaloguj się.
2. Otwórz edycję usługi.
3. Zmień tylko tytuł i zapisz.
Wynik oczekiwany: tytuł zmienia się, opis pozostaje bez zmian.
Wynik rzeczywisty: opis staje się pusty.
Załączniki: ...
```

### Priorytety

- **Krytyczny** – utrata danych, brak możliwości uruchomienia, obejście logowania.
- **Wysoki** – główna funkcja nie działa, brak rozsądnego obejścia.
- **Średni** – problem utrudnia pracę, ale istnieje obejście.
- **Niski** – drobna wada wizualna lub tekstowa.

### Typowe błędy

- Testowanie tylko poprawnej ścieżki.
- Kilka różnych problemów w jednym zgłoszeniu.
- Brak dokładnych danych użytych w teście.
- Brak ponownego ustawienia bazy, przez co test zależy od poprzedniego.
- Zrzut ekranu bez opisu kroków.
- Uznanie własnego kodu za poprawny bez próby jego „zepsucia”.

### Co oddajesz

- `docs/TESTY.md` z przypadkami i wynikami;
- listę usterek z priorytetami;
- dowody dla najważniejszych problemów.

### Gotowe, gdy

- [ ] Każda obowiązkowa funkcja ma co najmniej jeden test.
- [ ] Uwzględniono przypadki błędne i graniczne.
- [ ] Inna osoba może powtórzyć kroki.
- [ ] Wszystkie niezaliczone testy mają zgłoszenie usterki.
- [ ] Priorytety odpowiadają wpływowi problemu.

---

## Dzień 18 – poprawki, regresja i optymalizacja

Gałąź: `day-18-poprawki`

### Cel

Usunąć najważniejsze usterki, upewnić się, że poprawki nie zepsuły innych funkcji, i przygotować stabilnego kandydata do wersji 1.0.

### Co warto wiedzieć

**Test regresji** sprawdza, czy zmiana nie uszkodziła wcześniej działającej funkcji. Po poprawieniu formularza nie testuj wyłącznie przypadku błędnego – ponownie sprawdź także poprawne wysłanie.

### Instrukcja krok po kroku

1. Przejrzyj listę usterek z dnia 17.
2. Najpierw napraw krytyczne, następnie wysokie.
3. Każdą usterkę poprawiaj w osobnym, niewielkim commicie, jeśli to możliwe.
4. Po poprawce wykonaj dokładnie kroki z jej zgłoszenia.
5. Następnie wykonaj powiązane testy regresji.
6. Zapisz numer commita albo opis poprawki w raporcie testów.
7. Sprawdź logi PHP i konsolę na wszystkich podstronach.
8. Sprawdź stronę w dwóch przeglądarkach i na telefonie lub emulatorze.
9. Usuń nieużywane pliki, tymczasowe komentarze i testowe komunikaty.
10. Nie usuwaj kodu, którego przeznaczenia nie rozumiesz – najpierw sprawdź użycia.
11. Zoptymalizuj ciężkie obrazy i niepotrzebne zasoby.
12. Ponownie wykonaj najważniejsze scenariusze od początku do końca.

### Przykład testu regresji po zmianie formularza

- puste dane nadal są odrzucane;
- błędny e-mail nadal jest odrzucany;
- poprawna wiadomość zapisuje się raz;
- polskie znaki wyświetlają się poprawnie;
- odświeżenie nie tworzy duplikatu;
- strona nadal wygląda dobrze na telefonie.

### Co można bezpiecznie uporządkować

- powtarzające się fragmenty przenieść do funkcji;
- zmienne nazwać bardziej jednoznacznie;
- usunąć nieużywane klasy CSS po sprawdzeniu całego projektu;
- ujednolicić komunikaty;
- zmniejszyć obrazy o przesadnych wymiarach.

Nie wykonuj dużej przebudowy całej aplikacji dzień przed dokumentacją, jeśli nie jest potrzebna do naprawy istotnego problemu.

### Typowe błędy

- Poprawianie kilku niezależnych problemów jednym dużym commitem.
- Zamknięcie usterki bez ponownego testu.
- Naprawa widoku Chrome bez sprawdzenia Firefox/Edge.
- Usunięcie ostrzeżenia przez ukrycie błędów zamiast naprawy przyczyny.
- Zmiana działającej struktury tuż przed wydaniem bez potrzeby.

### Co oddajesz

- poprawki usterek krytycznych i wysokich;
- wyniki testów regresji;
- zaktualizowany raport z pozostałymi znanymi problemami;
- stabilną wersję kandydującą do wydania.

### Gotowe, gdy

- [ ] Nie ma otwartych usterek krytycznych ani wysokich.
- [ ] Każdą poprawkę przetestowano ponownie.
- [ ] Konsola i logi nie zawierają nieobsłużonych błędów.
- [ ] Główne scenariusze działają w dwóch przeglądarkach.
- [ ] Projekt nie zawiera zbędnych plików testowych i sekretów.

---

## Dzień 19 – dokumentacja i próba czystej instalacji

Gałąź: `day-19-dokumentacja`

### Cel

Przygotować dokumentację pozwalającą nowej osobie uruchomić i zrozumieć projekt bez ustnych podpowiedzi autora.

### Instrukcja krok po kroku

1. Uzupełnij główny `README.md` projektu, nie myląc go z README repozytorium zadań.
2. Dodaj krótki opis celu i głównych funkcji aplikacji.
3. Wymień wymagane wersje PHP, MySQL i ważnych bibliotek.
4. Opisz strukturę katalogów.
5. Napisz instrukcję instalacji krok po kroku:
   - sklonowanie repozytorium;
   - utworzenie bazy;
   - import `schema.sql` i `seed.sql`;
   - utworzenie lokalnej konfiguracji z pliku przykładowego;
   - uruchomienie serwera;
   - utworzenie lub ustawienie konta administratora.
6. Opisz korzystanie z części publicznej i panelu.
7. Dodaj zrzuty ekranu najważniejszych widoków.
8. Wymień znane ograniczenia i niezrealizowane pomysły dodatkowe.
9. Dodaj źródła wykorzystanych materiałów i bibliotek.
10. Sprawdź, czy instrukcja nie zawiera prawdziwych danych dostępowych.
11. Sklonuj projekt do nowego katalogu albo poproś inną osobę o wykonanie instrukcji.
12. Zapisz każdy krok, którego w instrukcji brakowało, i popraw dokument.

### Przykładowy spis README projektu

```text
# Nazwa projektu
## Opis
## Funkcje
## Technologie
## Wymagania środowiska
## Instalacja
## Konfiguracja bazy danych
## Uruchomienie
## Konto demonstracyjne / sposób utworzenia konta
## Struktura katalogów
## Testy
## Znane ograniczenia
## Autor i źródła materiałów
```

### Zasada dobrego kroku instalacji

Słabo:

> Skonfiguruj bazę i uruchom projekt.

Lepiej:

> Utwórz pustą bazę o nazwie wybranej lokalnie. Zaimportuj najpierw `database/schema.sql`, a następnie `database/seed.sql`. Skopiuj `config.example.php` jako `config.local.php` i wpisz lokalne dane połączenia. Plik lokalny jest ignorowany przez Git.

Nie umieszczaj w instrukcji hasła działającego na prawdziwym serwerze.

### Test czystej instalacji

Uznaj go za zaliczony dopiero, gdy:

- projekt został pobrany do nowego katalogu;
- nie korzysta z plików spoza repozytorium, o których nie wspomina instrukcja;
- baza powstała ze skryptów;
- strona publiczna działa;
- można utworzyć konto administratora i zalogować się;
- formularz i CRUD działają.

### Typowe błędy

- Dokumentacja opisuje stan sprzed kilku dni.
- Instrukcja zakłada, że użytkownik zna lokalne ścieżki autora.
- Brakuje informacji o wersjach lub rozszerzeniach PHP.
- Screenshoty zawierają dane prywatne.
- Projekt działa tylko dlatego, że autor ma lokalnie dodatkowy plik niewymieniony w instrukcji.
- „Znane ograniczenia” są ukrywane zamiast rzetelnie opisane.

### Co oddajesz

- kompletne README projektu;
- aktualną dokumentację techniczną;
- zrzuty ekranu;
- wynik czystej instalacji.

### Gotowe, gdy

- [ ] Osoba bez wcześniejszej znajomości projektu może go uruchomić.
- [ ] Dokumentacja odpowiada bieżącej wersji kodu.
- [ ] Wszystkie wymagane pliki i kroki są wymienione.
- [ ] Nie ma sekretów ani danych osobowych.
- [ ] Znane ograniczenia są uczciwie opisane.

---

## Dzień 20 – prezentacja, odbiór i wersja 1.0

Gałąź: `day-20-final`

### Cel

Zaprezentować wykonany projekt, wykazać znajomość własnego kodu, wprowadzić ostatnie drobne poprawki i przygotować wydanie 1.0.

### Przygotowanie prezentacji

Przygotuj prezentację trwającą około 10–15 minut. Możesz użyć kilku slajdów albo prowadzić prezentację bezpośrednio w aplikacji. Zachowaj następującą kolejność:

1. Problem i odbiorcy strony.
2. Najważniejsze wymagania.
3. Makieta i sposób dostosowania do telefonu.
4. Część publiczna: oferta, galeria i kontakt.
5. Wysłanie formularza i zapis wiadomości.
6. Logowanie do panelu i jedna pełna operacja CRUD.
7. Krótkie pokazanie bazy danych.
8. Historia Git oraz wybrany Pull Request.
9. Jeden trudny problem i sposób jego rozwiązania.
10. Znane ograniczenia i pomysł na dalszy rozwój.

### Instrukcja krok po kroku

1. Przygotuj czystą bazę demonstracyjną.
2. Upewnij się, że znasz lokalne dane demonstracyjne bez pokazywania prawdziwych haseł.
3. Przećwicz prezentację z zegarkiem.
4. Przygotuj awaryjne zrzuty ekranu najważniejszych widoków.
5. Otwórz wcześniej wszystkie potrzebne narzędzia i zamknij prywatne karty oraz aplikacje.
6. Podczas prezentacji pokaż działanie, a nie tylko kod.
7. Następnie pokaż jeden fragment kodu i wyjaśnij go własnymi słowami.
8. Odpowiedz na pytania. Jeśli nie znasz odpowiedzi, powiedz, jak byś ją sprawdził.
9. Zapisz uwagi odbiorowe opiekuna.
10. Wprowadź wyłącznie uzgodnione drobne poprawki. Większe pomysły zapisz jako dalszy rozwój.
11. Ponownie uruchom najważniejsze testy.
12. Sprawdź `git status`, dokumentację i listę plików.
13. Otwórz końcowy Pull Request.

### Pytania, na które warto umieć odpowiedzieć

- Dlaczego strona ma taką strukturę?
- Jak działa filtrowanie galerii?
- Dlaczego walidacja jest zarówno w JavaScript, jak i PHP?
- W jaki sposób prepared statements poprawiają bezpieczeństwo?
- Jak przechowywane jest hasło?
- Co dzieje się po wysłaniu formularza?
- Jak odtworzyć bazę na nowym komputerze?
- Który fragment zmieniłbyś przy większym projekcie?

### Kontrola przed wydaniem

- [ ] Projekt uruchamia się według README.
- [ ] Baza odtwarza się ze skryptów.
- [ ] Część publiczna działa na telefonie i komputerze.
- [ ] Formularz jest walidowany w przeglądarce i na serwerze.
- [ ] Wiadomość zapisuje się dokładnie raz.
- [ ] Logowanie, wylogowanie i cały CRUD działają.
- [ ] Osoba niezalogowana nie ma dostępu do panelu.
- [ ] Nie ma nieobsłużonych błędów w konsoli i logach.
- [ ] Repozytorium nie zawiera sekretów ani danych prywatnych.
- [ ] Dokumentacja i zrzuty są aktualne.
- [ ] Wszystkie wymagania MUST mają potwierdzony rezultat.

### Typowe błędy

- Prezentacja zaczyna się od długiego czytania kodu.
- Używana jest prywatna baza z prawdziwymi danymi.
- Demonstracja nie została wcześniej przećwiczona.
- Autor nie potrafi wyjaśnić skopiowanego fragmentu.
- Ostatnie duże zmiany są dodane bez ponownych testów.
- Tag wersji powstaje przed akceptacją opiekuna.

### Co oddajesz

- końcowy Pull Request;
- działającą i udokumentowaną aplikację;
- krótką prezentację;
- listę uwag odbiorowych i wprowadzonych zmian.

### Gotowe, gdy

- [ ] Projekt został zaprezentowany.
- [ ] Potrafisz wyjaśnić najważniejsze elementy własnego kodu.
- [ ] Wszystkie obowiązkowe zadania są wykonane.
- [ ] Ostatnie testy zakończyły się powodzeniem.
- [ ] Opiekun zaakceptował wersję końcową.

Po akceptacji opiekun może połączyć Pull Request i utworzyć tag `v1.0.0`.

---

# Zadania dodatkowe po ukończeniu zakresu obowiązkowego

Nie rozpoczynaj ich przed zaakceptowaniem wersji 1.0:

- wyszukiwanie i filtrowanie po stronie serwera;
- paginacja długiej listy;
- bezpieczne przesyłanie zdjęć;
- role użytkowników;
- testy automatyczne;
- proste API JSON;
- automatyczna kontrola jakości w CI;
- wdrożenie demonstracyjne na uzgodniony serwer testowy.

Każde dodatkowe zadanie najpierw opisz jako wymaganie, oszacuj i uzgodnij z opiekunem.

