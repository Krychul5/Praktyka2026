# Tydzień 3 – PHP, baza danych i panel CRUD

W tym tygodniu statyczna strona stanie się prostą aplikacją. Skonfigurujesz PHP i MySQL, zaprojektujesz bazę, odczytasz dane, zapiszesz formularz i rozpoczniesz panel administracyjny.

Pracuj wyłącznie na danych demonstracyjnych. Nie kopiuj do projektu prawdziwych danych klientów.

## Dzień 11 – środowisko lokalne i podstawy PHP

Gałąź: `day-11-php`

### Cel

Uruchomić stronę przez lokalny serwer PHP, uporządkować wspólne fragmenty i przygotować bezpieczną konfigurację.

### Co warto wiedzieć

Plik HTML jest zwykle wysyłany bez zmian. Kod PHP wykonuje się na serwerze, a przeglądarka otrzymuje dopiero wynik, najczęściej HTML. Dlatego pliku PHP nie testuj przez dwukrotne kliknięcie – musi być otwarty przez adres lokalnego serwera, np. `http://localhost/...`.

### Instrukcja krok po kroku

1. Uruchom środowisko XAMPP opisane w `PROGRAMY.md` i włącz moduły Apache oraz MySQL.
2. Sprawdź wersję PHP i zapisz ją w `docs/TECHNOLOGIE.md`.
3. Uruchom minimalny plik testowy i sprawdź, czy PHP jest wykonywane.
4. Zmień rozszerzenia potrzebnych podstron z `.html` na `.php`.
5. Zaktualizuj wszystkie odnośniki prowadzące do zmienionych plików.
6. Przenieś wspólny nagłówek, nawigację i stopkę do katalogu `includes/`.
7. Wczytaj je przez `require` lub `require_once`.
8. Przekaż do wspólnego nagłówka tytuł podstrony w prosty, uzgodniony sposób.
9. Utwórz lokalny plik konfiguracji, np. `config.local.php`, i upewnij się, że jest w `.gitignore`.
10. Utwórz plik przykładowy, np. `config.example.php`, zawierający wyłącznie nazwy ustawień i fikcyjne wartości.
11. Dodaj do projektowego README sekcję „Uruchomienie lokalne”.

### Przykład idei wspólnego fragmentu

W podstronie:

```php
<?php
$pageTitle = 'Oferta';
require __DIR__ . '/includes/header.php';
?>

<main>
  <!-- Treść konkretnej podstrony -->
</main>

<?php require __DIR__ . '/includes/footer.php'; ?>
```

To tylko przykład. Ścieżki dopasuj do struktury własnego projektu. Stała `__DIR__` wskazuje katalog aktualnego pliku i pomaga uniknąć ścieżek zależnych od miejsca uruchomienia.

### Przykład pliku konfiguracyjnego do repozytorium

```php
<?php
return [
    'db_host' => 'localhost',
    'db_name' => 'example_database',
    'db_user' => 'example_user',
    'db_password' => 'change_me',
];
```

Nie wstawiaj do przykładowego pliku działającego hasła. Rzeczywiste wartości mają znajdować się wyłącznie w ignorowanym pliku lokalnym.

### Typowe błędy

- Otwieranie pliku PHP jako `file:///...` zamiast przez serwer.
- Powtarzanie całego menu na każdej podstronie.
- Twarde ścieżki typu `C:\Users\...` w kodzie.
- Dodanie lokalnego hasła do commita.
- Włączenie szczegółowych błędów na stronie przeznaczonej do publikacji.
- Biała strona bez sprawdzenia logu PHP.

### Co oddajesz

- projekt działający przez lokalny serwer;
- wspólne pliki nagłówka i stopki;
- przykładową konfigurację bez sekretów;
- instrukcję uruchomienia PHP.

### Gotowe, gdy

- [ ] Wszystkie podstrony otwierają się przez lokalny serwer.
- [ ] Menu i stopka są współdzielone, a nie skopiowane.
- [ ] Linki po zmianie rozszerzeń nadal działają.
- [ ] Rzeczywisty plik konfiguracji jest ignorowany przez Git.
- [ ] Nowa osoba wie z README, jak uruchomić projekt.

---

## Dzień 12 – projektowanie bazy danych MySQL

Gałąź: `day-12-baza`

### Cel

Zaprojektować prostą bazę, którą da się odtworzyć z plików SQL na innym komputerze.

### Co warto wiedzieć

Tabela przechowuje rekordy jednego rodzaju. Kolumna opisuje cechę, a wiersz pojedynczy rekord. **Klucz główny** jednoznacznie identyfikuje rekord. **Klucz obcy** łączy rekord z inną tabelą.

Nie zapisuj kilku informacji w jednej kolumnie, jeśli trzeba je później osobno filtrować lub zmieniać.

### Zakres minimalny

Zaprojektuj co najmniej:

- tabelę treści, np. `services`, `gallery_items` albo `news`;
- tabelę `messages` dla formularza kontaktowego;
- tabelę `users` potrzebną do późniejszego logowania.

### Instrukcja krok po kroku

1. Wypisz dane potrzebne w każdej tabeli.
2. Dla każdej kolumny określ typ, wymaganie `NULL/NOT NULL` i ewentualną wartość domyślną.
3. Dodaj liczbowy klucz główny lub inne uzgodnione jednoznaczne ID.
4. Zastanów się, które wartości muszą być unikalne, np. login użytkownika.
5. Dodaj datę utworzenia do wiadomości i innych rekordów, jeśli jest potrzebna.
6. Narysuj prosty diagram lub przygotuj tabelę opisującą model.
7. Utwórz `database/schema.sql` z poleceniami tworzącymi tabele.
8. Utwórz `database/seed.sql` z kilkoma fikcyjnymi rekordami demonstracyjnymi.
9. Usuń testową bazę i odtwórz ją wyłącznie z obu skryptów.
10. Zapisz instrukcję importu w README.

### Przykład opisu tabeli

| Kolumna | Typ | Wymagana | Znaczenie |
|---|---|---|---|
| id | INT UNSIGNED | tak | klucz główny |
| title | VARCHAR(120) | tak | krótka nazwa usługi |
| description | TEXT | tak | opis widoczny na stronie |
| is_active | BOOLEAN | tak | czy rekord ma być publikowany |
| created_at | DATETIME | tak | data utworzenia |

To przykład. Dobierz długości i kolumny do własnej zawartości.

### Fragment przykładowej definicji

```sql
CREATE TABLE services (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(120) NOT NULL,
    description TEXT NOT NULL,
    is_active BOOLEAN NOT NULL DEFAULT TRUE,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

Nie kopiuj tej tabeli, jeśli projekt wymaga innych danych. Potraf wyjaśnić znaczenie każdego typu i ograniczenia.

### Dane demonstracyjne

Używaj wpisów typu:

- `anna@example.test` zamiast prawdziwego e-maila;
- `Jan Testowy` zamiast danych realnej osoby;
- fikcyjnych treści bez informacji poufnych.

Domena `.test` jest przeznaczona do przykładów i nie powinna prowadzić do przypadkowej skrzynki.

### Typowe błędy

- Jedna tabela przechowuje wszystko, niezależnie od rodzaju danych.
- Każda kolumna ma typ `TEXT`.
- Brak klucza głównego.
- Hasło użytkownika jest przechowywane jako jawny tekst.
- Plik `seed.sql` zawiera dane prawdziwych osób.
- Skrypt działa tylko wtedy, gdy tabele wcześniej utworzono ręcznie.

### Co oddajesz

- diagram lub opis modelu w `docs/BAZA_DANYCH.md`;
- `database/schema.sql`;
- `database/seed.sql`;
- instrukcję odtworzenia bazy.

### Gotowe, gdy

- [ ] Każda tabela ma uzasadniony cel i klucz główny.
- [ ] Typy danych są dobrane świadomie.
- [ ] Login użytkownika może być unikalny.
- [ ] W seedzie znajdują się wyłącznie fikcyjne dane.
- [ ] Czystą bazę można odtworzyć bez ręcznych poprawek.

---

## Dzień 13 – połączenie z bazą i odczyt danych

Gałąź: `day-13-odczyt`

### Cel

Połączyć PHP z MySQL i wygenerować fragment strony na podstawie rekordów zamiast treści wpisanej na stałe.

### Co warto wiedzieć

PDO to interfejs PHP do pracy z bazą. Pozwala ustawić zgłaszanie wyjątków oraz korzystać z prepared statements. Dane pobrane z bazy nie są automatycznie bezpieczne do wstawienia w HTML – przed wyświetleniem należy je zakodować.

### Instrukcja krok po kroku

1. Wczytaj dane dostępowe z lokalnego pliku konfiguracji.
2. Utwórz jeden współdzielony mechanizm połączenia z bazą.
3. Ustaw kodowanie `utf8mb4`.
4. Skonfiguruj PDO tak, aby błędy powodowały wyjątki.
5. Przechwyć błąd połączenia. Użytkownikowi pokaż ogólny komunikat, a szczegóły sprawdź w bezpiecznym logu lokalnym.
6. Wybierz jedną sekcję, np. ofertę, która będzie generowana z bazy.
7. Pobierz tylko potrzebne kolumny i rekordy, np. wyłącznie aktywne usługi.
8. Zdefiniuj sensowne sortowanie w zapytaniu.
9. Wyświetl rekordy w pętli.
10. Każdą wartość tekstową zakoduj przed wstawieniem do HTML.
11. Dodaj przyjazny komunikat, gdy zapytanie nie zwróci żadnego rekordu.
12. Zmień rekord w bazie i potwierdź, że zmiana pojawia się na stronie.

### Idea połączenia PDO

Poniższy fragment pokazuje sposób myślenia, ale wymaga dopasowania konfiguracji i obsługi błędów:

```php
$dsn = sprintf(
    'mysql:host=%s;dbname=%s;charset=utf8mb4',
    $config['db_host'],
    $config['db_name']
);

$pdo = new PDO($dsn, $config['db_user'], $config['db_password'], [
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
]);
```

### Kodowanie tekstu w HTML

Przy wyświetlaniu tytułu pobranego z bazy użyj mechanizmu kodowania, np.:

```php
<?= htmlspecialchars($service['title'], ENT_QUOTES, 'UTF-8') ?>
```

Bez tego tekst zawierający znaczniki mógłby zostać potraktowany jak kod HTML.

### Typowe błędy

- Dane dostępowe są zapisane bezpośrednio w pliku dodanym do Git.
- Błąd połączenia pokazuje użytkownikowi login, ścieżki lub pełne zapytanie.
- Dane z bazy są wstawiane do HTML bez kodowania.
- Zapytanie używa `SELECT *`, choć potrzebne są tylko dwie kolumny.
- Przy pustej tabeli strona wygląda na zepsutą.
- Każda karta otwiera nowe połączenie z bazą.

### Co oddajesz

- działające połączenie z bazą;
- jedną sekcję publiczną generowaną z rekordów;
- bezpieczną obsługę pustego wyniku i błędu połączenia;
- opis ręcznego testu w Pull Requeście.

### Gotowe, gdy

- [ ] Zmiana rekordu w bazie pojawia się na stronie.
- [ ] Polskie znaki wyświetlają się poprawnie.
- [ ] Tekst z bazy jest kodowany przed wstawieniem do HTML.
- [ ] Pusta tabela ma czytelny stan pusty.
- [ ] Dane dostępowe nie znajdują się w historii Git.

---

## Dzień 14 – zapis formularza i walidacja po stronie serwera

Gałąź: `day-14-zapis-formularza`

### Cel

Bezpiecznie odebrać dane metodą POST, sprawdzić je po stronie serwera i zapisać wiadomość w bazie.

### Co warto wiedzieć

Nigdy nie ufaj danym przychodzącym z przeglądarki. Atrybut `required` i JavaScript można ominąć. PHP musi samodzielnie sprawdzić wszystkie dane.

**Prepared statement** oddziela treść polecenia SQL od wartości użytkownika. Nie buduj zapytania przez doklejanie tekstu formularza.

### Instrukcja krok po kroku

1. Ustaw formularz na metodę `POST` i poprawny adres obsługi.
2. W PHP wykonuj logikę zapisu tylko dla żądania POST.
3. Odczytaj spodziewane pola. Nie zakładaj, że zawsze istnieją.
4. Usuń zbędne białe znaki z początku i końca.
5. Sprawdź wymagane pola, długości i format e-maila.
6. Zapisuj błędy w tablicy przypisanej do konkretnych pól.
7. Jeśli występują błędy, pokaż formularz ponownie, zachowaj bezpieczne wartości i wyświetl komunikaty.
8. Jeśli dane są poprawne, wykonaj INSERT przez prepared statement.
9. Po powodzeniu zastosuj schemat POST–Redirect–GET: przekieruj użytkownika na stronę potwierdzenia albo ten sam adres z informacją o sukcesie.
10. Nie wyświetlaj treści wyjątku SQL użytkownikowi.
11. Przetestuj nietypowe dane i próbę wielokrotnego odświeżenia.

### Przykład walidacji e-maila

```php
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    $errors['email'] = 'Wpisz poprawny adres e-mail.';
}
```

### Idea prepared statement

```php
$statement = $pdo->prepare(
    'INSERT INTO messages (name, email, subject, message) '
    . 'VALUES (:name, :email, :subject, :message)'
);

$statement->execute([
    'name' => $name,
    'email' => $email,
    'subject' => $subject,
    'message' => $message,
]);
```

Nazwy tabel i kolumn dopasuj do swojego schematu. Nie dodawaj do zapytania zmiennych przez konkatenację.

### Przypadki testowe

- puste pola;
- pola zawierające tylko spacje;
- niepoprawny e-mail;
- tekst dłuższy niż limit bazy;
- apostrof, cudzysłów i polskie znaki;
- treść wyglądająca jak znacznik HTML;
- poprawny formularz;
- odświeżenie po poprawnym wysłaniu.

### Typowe błędy

- Sprawdzenie danych tylko w JavaScript.
- Sklejanie zapytania SQL ze zmiennych użytkownika.
- Używanie samego `htmlspecialchars` jako „zabezpieczenia SQL”. Kodowanie HTML i prepared statement rozwiązują inne problemy.
- Czyszczenie formularza po błędzie, przez co użytkownik musi wpisać wszystko ponownie.
- Powtórny zapis wiadomości po odświeżeniu.

### Co oddajesz

- zapis wiadomości metodą POST;
- walidację serwerową;
- prepared statement;
- komunikaty błędów i sukcesu;
- listę wyników testów.

### Gotowe, gdy

- [ ] Wyłączenie JavaScript nie pozwala ominąć walidacji.
- [ ] Poprawna wiadomość pojawia się w bazie dokładnie raz.
- [ ] Błędne dane nie są zapisywane.
- [ ] Zapytanie używa parametrów.
- [ ] Użytkownik nie widzi szczegółów błędu bazy.

---

## Dzień 15 – panel CRUD: lista, dodawanie i edycja

Gałąź: `day-15-panel-crud`

### Cel

Rozpocząć panel zarządzania danymi. Dziś wykonasz odczyt, dodawanie i edycję. Usuwanie i zabezpieczenie dostępu powstaną następnego dnia.

### Co warto wiedzieć

CRUD oznacza:

- **Create** – utworzenie rekordu;
- **Read** – odczyt;
- **Update** – edycję;
- **Delete** – usunięcie.

Panel administracyjny powinien być prosty i czytelny. Najważniejsze są poprawność, bezpieczeństwo i jednoznaczne komunikaty, nie efekty graficzne.

### Instrukcja krok po kroku

1. Utwórz katalog `admin/`.
2. Dodaj stronę listy rekordów, np. usług.
3. Pokaż tylko kolumny przydatne administratorowi: ID, tytuł, status, datę oraz działania.
4. Dodaj komunikat dla pustej listy.
5. Utwórz formularz dodawania rekordu.
6. Wykonaj walidację po stronie serwera i zapis przez prepared statement.
7. Dodaj stronę edycji przyjmującą identyfikator rekordu.
8. Sprawdź, czy ID ma oczekiwany format.
9. Jeśli rekord nie istnieje, pokaż stronę błędu 404 lub czytelny komunikat, zamiast pustego formularza.
10. Wczytaj bieżące dane do formularza edycji.
11. Zapisz zmianę przez przygotowane zapytanie UPDATE.
12. Po dodaniu lub edycji przekieruj na listę i pokaż jednorazowy komunikat sukcesu.
13. Sprawdź, czy zmiana jest widoczna w publicznej części strony.

### Przykładowa organizacja panelu

```text
admin/
├── index.php          # lista rekordów
├── create.php         # dodawanie
├── edit.php           # edycja
└── includes/          # wspólne fragmenty panelu, jeśli potrzebne
```

To jedna z możliwości. Opiekun może zalecić inną strukturę.

### Pseudokod edycji

```text
odczytaj i sprawdź ID
znajdź rekord
jeżeli nie istnieje -> zwróć 404

jeżeli żądanie to POST:
    odczytaj dane
    zwaliduj
    jeżeli poprawne:
        wykonaj UPDATE z parametrami
        przekieruj na listę

wyświetl formularz z danymi i ewentualnymi błędami
```

Najpierw napisz ten przepływ własnymi słowami, a dopiero później kod.

### Typowe błędy

- ID rekordu jest wstawiane bezpośrednio do SQL.
- Edycja nie sprawdza, czy rekord istnieje.
- Ten sam kod walidacji dodawania i edycji jest skopiowany w wielu miejscach.
- Po odświeżeniu formularz wykonuje operację drugi raz.
- Użytkownik dostaje komunikat „sukces”, mimo że zapytanie się nie wykonało.
- Panel ma dziś „tymczasowe hasło” zapisane w kodzie. Logowanie zostanie wykonane poprawnie następnego dnia.

### Co oddajesz

- listę rekordów;
- dodawanie z walidacją;
- edycję z obsługą braku rekordu;
- zmianę widoczną w części publicznej;
- Pull Request do trzeciego punktu kontrolnego.

### Gotowe, gdy

- [ ] Lista ma czytelny stan pusty.
- [ ] Poprawny rekord można dodać i edytować.
- [ ] Błędne dane pozostawiają użytkownika w formularzu z komunikatem.
- [ ] Nieprawidłowe lub nieistniejące ID jest obsłużone.
- [ ] Wszystkie zapytania z danymi użytkownika korzystają z parametrów.
- [ ] Opiekun zaakceptował trzeci tydzień.

