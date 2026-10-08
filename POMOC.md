# Pomoc i słownik pojęć

## Jak szukać rozwiązania

1. Przeczytaj cały komunikat błędu, łącznie z nazwą pliku i numerem linii.
2. Sprawdź konsolę przeglądarki: klawisz `F12`, zakładka **Console**.
3. Dla problemu z siecią lub formularzem sprawdź zakładkę **Network**.
4. Sprawdź, czy edytujesz właściwy plik i czy zapisałeś zmianę.
5. Cofnij się do ostatniej małej zmiany i porównaj działanie.
6. Wyszukaj dokładny komunikat błędu, pomijając dane lokalne.
7. Korzystaj przede wszystkim z dokumentacji MDN, PHP, MySQL i Bootstrap.
8. Jeśli nadal nie działa, przygotuj konkretny opis dla opiekuna.

Dobry opis problemu:

> Po wysłaniu poprawnego formularza strona przeładowuje się, ale rekord nie pojawia się w tabeli `messages`. W zakładce Network odpowiedź ma status 500. Sprawdziłem nazwy pól i połączenie z bazą. Komunikat w logu wskazuje plik `contact.php`, linia 42.

Słaby opis problemu:

> Nie działa.

## Słownik

**HTML** – opisuje strukturę i znaczenie treści strony, np. nagłówek, menu, artykuł i formularz.

**CSS** – odpowiada za wygląd i układ strony: kolory, odstępy, rozmiary i zachowanie na różnych ekranach.

**JavaScript** – pozwala dodać zachowanie w przeglądarce, np. filtrowanie galerii lub sprawdzanie formularza.

**PHP** – kod wykonywany na serwerze. Może odebrać formularz, połączyć się z bazą i wygenerować HTML.

**MySQL** – system bazy danych przechowujący uporządkowane rekordy w tabelach.

**Frontend** – część aplikacji widoczna w przeglądarce.

**Backend** – część działająca po stronie serwera, np. PHP i połączenie z bazą.

**Responsywność** – dostosowanie wyglądu do telefonu, tabletu i komputera.

**Walidacja** – sprawdzenie, czy dane mają poprawny format i spełniają wymagania.

**CRUD** – cztery podstawowe operacje na danych: utworzenie, odczyt, edycja i usunięcie.

**Prepared statement** – bezpieczny sposób przekazywania danych do zapytania SQL bez sklejania ich z treścią zapytania.

**Sesja** – mechanizm pozwalający serwerowi zapamiętać, że użytkownik jest zalogowany.

**Commit** – zapis wybranego etapu zmian w historii Git.

**Gałąź** – oddzielna linia pracy nad zadaniem, która nie psuje zaakceptowanej wersji głównej.

**Pull Request** – prośba o przejrzenie i dołączenie zmian do głównej gałęzi.

**Breakpoint** – szerokość ekranu, przy której układ strony zmienia się za pomocą reguły CSS.

**Dostępność** – projektowanie strony tak, aby mogły z niej korzystać również osoby używające klawiatury, czytnika ekranu lub mające ograniczenia wzroku.

## Przydatne skróty w narzędziach przeglądarki

- `F12` – otwarcie narzędzi deweloperskich;
- `Ctrl+Shift+M` – tryb podglądu urządzeń mobilnych w wielu przeglądarkach;
- zakładka **Elements/Inspector** – podgląd HTML i stylów;
- zakładka **Console** – błędy JavaScript;
- zakładka **Network** – żądania, odpowiedzi i rozmiary plików.

## Jak poprosić opiekuna o pomoc

Przekaż cztery informacje:

1. Co próbujesz osiągnąć?
2. Jaki jest aktualny rezultat?
3. Jaki rezultat był oczekiwany?
4. Co już sprawdziłeś lub zmieniłeś?

Nie ukrywaj błędu i nie kasuj niedziałającej próby przed rozmową. Czasami właśnie ona najlepiej pokazuje tok rozumowania.

