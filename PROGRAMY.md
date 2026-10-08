# Programy potrzebne na laptopie praktykanta

Instrukcja jest przygotowana przede wszystkim dla **Windows 11 w wersji 64-bitowej**. Jeśli laptop ma Windows 10, macOS albo Linux, przed instalacją uzgodnij środowisko z opiekunem, ponieważ obsługiwane wersje, nazwy programów i ścieżki mogą być inne.

Do projektu używamy jednego, wspólnego zestawu narzędzi. Nie instaluj kilku różnych pakietów PHP/MySQL jednocześnie, ponieważ mogą zajmować te same porty i utrudniać diagnozowanie problemów.

## Programy obowiązkowe

### 1. Visual Studio Code – edytor kodu

Zastosowanie:

- tworzenie plików HTML, CSS, JavaScript, PHP, SQL i Markdown;
- przeglądanie całego katalogu projektu;
- korzystanie z terminala;
- sprawdzanie zmian Git.

Pobieranie: [oficjalna strona Visual Studio Code](https://code.visualstudio.com/download)

Wybierz:

- wydanie **Stable**, nie Insiders;
- **Windows User Installer 64-bit**, jeśli laptop ma standardowy procesor Intel lub AMD;
- podczas instalacji pozostaw włączone dodanie programu do PATH i menu kontekstowego, jeśli instalator proponuje te opcje.

Po instalacji:

1. Uruchom Visual Studio Code.
2. Wybierz `File > Open Folder` i otwieraj cały katalog projektu, a nie pojedynczy plik.
3. Gdy pojawi się pytanie o zaufanie do katalogu, zaakceptuj je tylko dla repozytorium przekazanego przez opiekuna.

### 2. Git for Windows – historia zmian i wysyłanie kodu

Zastosowanie:

- pobieranie repozytorium na laptop;
- tworzenie osobnej gałęzi na każde zadanie;
- zapisywanie commitów;
- wysyłanie pracy do zdalnego repozytorium.

Pobieranie: [oficjalna strona Git for Windows](https://git-scm.com/install/windows)

Wybierz standardowy instalator 64-bit. Podczas pierwszej instalacji możesz pozostawić ustawienia domyślne, chyba że opiekun wskaże inaczej.

Po instalacji zamknij i ponownie otwórz Visual Studio Code. W terminalu sprawdź:

```text
git --version
```

Następnie skonfiguruj dane autora commitów. Użyj własnych prawdziwych danych przeznaczonych do podpisu pracy, ale nie wpisuj hasła:

```text
git config --global user.name "Imię Nazwisko"
git config --global user.email "adres-powiązany-z-kontem@example.com"
```

Adres e-mail ustal z opiekunem. Jeżeli platforma Git udostępnia prywatny adres typu `noreply`, można użyć właśnie jego.

### 3. XAMPP – lokalny serwer PHP i baza danych

Zastosowanie:

- uruchamianie Apache;
- wykonywanie kodu PHP;
- uruchamianie lokalnej bazy MariaDB zgodnej z zadaniami MySQL;
- obsługa bazy przez phpMyAdmin.

Pobieranie: [oficjalna strona Apache Friends](https://www.apachefriends.org/download.html)

Wybierz wersję dla Windows zawierającą PHP 8.2 lub nowszą dostępną na oficjalnej stronie. Nie pobieraj XAMPP z portali z programami.

Podczas instalacji potrzebne są co najmniej:

- Apache;
- PHP;
- MySQL/MariaDB;
- phpMyAdmin.

Pozostałe składniki, np. FileZilla, Mercury, Tomcat lub Perl, nie są potrzebne w tym projekcie.

Ważne zasady:

- XAMPP służy tylko do lokalnej nauki i tworzenia projektu. Nie publikuj za jego pomocą aplikacji bezpośrednio w internecie.
- Nie uruchamiaj Apache ani bazy jako usług startujących stale z systemem, jeśli opiekun tego nie zaleci.
- Podczas pracy uruchamiaj w XAMPP Control Panel tylko moduły **Apache** i **MySQL**.
- Po zakończeniu pracy zatrzymaj oba moduły.

Sprawdzenie instalacji:

1. Uruchom XAMPP Control Panel.
2. Włącz Apache i MySQL.
3. Otwórz `http://localhost/` – powinna pojawić się lokalna strona startowa.
4. Otwórz `http://localhost/phpmyadmin/` – powinien uruchomić się panel bazy.

Jeśli Apache lub MySQL nie startuje, nie wyłączaj zapory i nie zmieniaj losowo portów. Zapisz komunikat z panelu i pokaż go opiekunowi.

### 4. Mozilla Firefox – główna przeglądarka testowa

Zastosowanie:

- sprawdzanie wyglądu strony;
- korzystanie z narzędzi deweloperskich;
- testowanie widoku telefonu;
- wykrywanie błędów JavaScript i nieudanych żądań.

Pobieranie: [oficjalna strona Mozilla Firefox](https://www.mozilla.org/firefox/new/)

Wybierz standardowe stabilne wydanie Firefox, nie Beta ani Nightly.

Najważniejsze narzędzia:

- `F12` – narzędzia deweloperskie;
- zakładka **Inspector** – HTML i CSS;
- zakładka **Console** – błędy JavaScript;
- zakładka **Network** – ładowane pliki i żądania formularza;
- `Ctrl+Shift+M` – widok urządzeń mobilnych.

### 5. Microsoft Edge – druga przeglądarka testowa

Microsoft Edge jest standardowo dostępny w Windows. Nie trzeba instalować Chrome, jeżeli Edge działa poprawnie.

Zastosowanie:

- porównanie działania strony w drugiej przeglądarce;
- sprawdzenie widoku mobilnego;
- wykonanie podstawowego audytu dostępności i wydajności.

Projekt nie jest zaliczony po sprawdzeniu wyłącznie w jednej przeglądarce. Główne funkcje testuj co najmniej w Firefox i Edge.

## Narzędzia używane w przeglądarce

Nie wymagają instalowania programu.

### diagrams.net – mapa strony, makiety i diagram bazy

Adres: [app.diagrams.net](https://app.diagrams.net/)

Możesz użyć tego narzędzia do:

- mapy podstron;
- prostych makiet;
- diagramu tabel i relacji.

Zapisuj plik źródłowy diagramu oraz eksport PNG lub PDF w katalogu `docs`. Nie umieszczaj w diagramach danych prywatnych.

### Walidator HTML

Adres: [Nu HTML Checker](https://validator.w3.org/nu/)

Używaj go do sprawdzania struktury HTML. Przeczytaj komunikat i popraw przyczynę – nie usuwaj kodu losowo tylko po to, aby zmniejszyć liczbę ostrzeżeń.

### Dokumentacja MDN

Adres: [MDN Web Docs](https://developer.mozilla.org/)

To podstawowe źródło informacji o HTML, CSS i JavaScript. Przy wyszukiwaniu konkretnego elementu dodaj do zapytania `MDN`, np. `input type email MDN`.

### Dokumentacja PHP

Adres: [PHP Manual](https://www.php.net/manual/)

Sprawdzaj tutaj znaczenie funkcji takich jak `password_hash`, `password_verify`, `filter_var`, `htmlspecialchars` i obsługę PDO.

### Dokumentacja Bootstrap

Adres: [Bootstrap Documentation](https://getbootstrap.com/docs/)

Korzystaj z dokumentacji tej samej wersji Bootstrap, którą zastosujesz w projekcie. Nie mieszaj przykładów pochodzących z różnych wydań.

## Zalecane rozszerzenia Visual Studio Code

Rozszerzenia instaluj w panelu **Extensions** wewnątrz Visual Studio Code. Przed instalacją sprawdź dokładną nazwę i wydawcę. Nie instaluj wielu rozszerzeń wykonujących to samo.

### PHP Intelephense

Pomaga wykrywać błędy składni PHP, podpowiada funkcje i umożliwia przechodzenie do definicji. Po instalacji sprawdź, czy jest aktywne wyłącznie dla plików PHP.

### Prettier – Code formatter

Pomaga zachować spójne formatowanie HTML, CSS i JavaScript. Ustal z opiekunem ustawienia przed automatycznym formatowaniem całego projektu.

### Live Server

Można go używać tylko podczas pracy nad statycznym HTML, CSS i JavaScript w pierwszych tygodniach. **Live Server nie wykonuje PHP i nie obsługuje MySQL**. Od rozpoczęcia PHP używaj Apache w XAMPP i adresu `http://localhost/...`.

Rozszerzenia są pomocą, a nie wymaganiem zaliczenia. Jeśli któreś powoduje problemy lub komputer jest słabszy, można je wyłączyć po uzgodnieniu z opiekunem.

## Program opcjonalny do zdjęć

Do zmniejszania i kadrowania fotografii można użyć edytora wskazanego przez opiekuna, np. GIMP albo Paint.NET. Jeżeli nie jest potrzebna zaawansowana obróbka, wystarczy wbudowana aplikacja systemowa umożliwiająca zmianę rozmiaru oraz bezpieczne narzędzie do konwersji.

Nie wysyłaj zdjęć firmowych i danych klientów do przypadkowych internetowych konwerterów.

## Programy, których nie potrzebujesz

W tym projekcie nie instaluj bez wyraźnego polecenia opiekuna:

- WordPressa;
- Dockera;
- Node.js i npm;
- frameworków PHP, np. Laravel lub Symfony;
- dodatkowego serwera MySQL obok XAMPP;
- kilku różnych pakietów XAMPP/WAMP/Laragon jednocześnie;
- klientów FTP;
- płatnych edytorów i narzędzi AI.

Nie są one złe, ale nie są potrzebne do realizacji obecnego planu i zwiększają liczbę możliwych problemów.

## Checklista przed pierwszym dniem

- [ ] Visual Studio Code uruchamia się i otwiera cały katalog.
- [ ] Polecenie `git --version` działa w terminalu VS Code.
- [ ] Imię i e-mail autora Git są skonfigurowane.
- [ ] Apache i MySQL uruchamiają się w XAMPP.
- [ ] `http://localhost/` otwiera się w Firefox.
- [ ] `http://localhost/phpmyadmin/` działa lokalnie.
- [ ] Firefox i Edge są dostępne do testów.
- [ ] Zakładki Console i Network w narzędziach przeglądarki są odnalezione.
- [ ] Praktykant zna adres zdalnego repozytorium i sposób logowania ustalony przez opiekuna.

Jeśli którykolwiek punkt nie działa, napraw środowisko wspólnie z opiekunem przed rozpoczęciem zadań projektowych.

