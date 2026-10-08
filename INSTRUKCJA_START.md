# Instrukcja rozpoczęcia i pracy z Git

## 1. Przygotuj narzędzia

Zainstaluj programy z listy [PROGRAMY.md](PROGRAMY.md). W projekcie przyjmujemy jeden wspólny zestaw: Visual Studio Code, Git for Windows, XAMPP, Firefox oraz Microsoft Edge. Dzięki temu instrukcje i pomoc opiekuna będą dotyczyć takiego samego środowiska.

Nie instaluj przypadkowych zamienników ani dodatkowych programów bez uzgodnienia z opiekunem. Instalatory pobieraj wyłącznie z oficjalnych stron wskazanych w instrukcji.

## 2. Sklonuj repozytorium

Opiekun poda adres repozytorium. W terminalu użyj:

```text
git clone ADRES_REPOZYTORIUM
cd NAZWA_KATALOGU
```

`ADRES_REPOZYTORIUM` i `NAZWA_KATALOGU` są przykładami – wstaw właściwe wartości.

Sprawdź stan:

```text
git status
```

Prawidłowy rezultat powinien informować, że pracujesz na gałęzi `main` i nie masz niezapisanych zmian.

## 3. Rozpoczynaj każdy dzień na osobnej gałęzi

Najpierw pobierz zaakceptowane zmiany:

```text
git switch main
git pull
```

Następnie utwórz gałąź wskazaną w zadaniu, np.:

```text
git switch -c day-01-analiza
```

Jeżeli polecenie `git switch` nie działa w używanej wersji Git, poproś opiekuna o pomoc. Nie próbuj naprawiać repozytorium poleceniami usuwającymi historię.

## 4. Zapisuj małe commity

Po ukończeniu logicznego fragmentu pracy:

```text
git status
git add NAZWA_PLIKU
git commit -m "docs: dodaj wymagania projektu"
```

Przykłady dobrych komunikatów:

- `docs: opisz odbiorców strony`
- `feat: dodaj menu główne`
- `style: przygotuj mobilny układ oferty`
- `fix: popraw komunikat błędu formularza`
- `test: opisz test logowania`

Nie używaj komunikatów typu `zmiany`, `poprawka`, `aaa` lub `final`, ponieważ nie wyjaśniają, co zostało zrobione.

## 5. Wyślij gałąź i otwórz Pull Request

```text
git push -u origin day-01-analiza
```

Na stronie repozytorium otwórz Pull Request z Twojej gałęzi do `main`. Uzupełnij dostępny szablon. Opisz:

- co zrobiłeś;
- jak to sprawdzić;
- z czym miałeś problem;
- w jakim miejscu szczególnie potrzebujesz opinii.

Nie łącz Pull Requesta samodzielnie, jeśli opiekun nie ustali inaczej.

## 6. Gdy Git pokazuje konflikt

Konflikt oznacza, że dwie wersje zmieniły to samo miejsce. Nie wybieraj zmian losowo i nie usuwaj plików. Zatrzymaj się, wykonaj `git status`, skopiuj komunikat i poproś opiekuna o wspólne rozwiązanie konfliktu. Rozwiązywanie konfliktów jest normalną częścią pracy zespołowej.

## 7. Czego nie wolno dodawać do repozytorium

- plików `.env` i `config.local.php`;
- prawdziwych haseł i danych dostępowych;
- kopii prawdziwej bazy klientów;
- danych osobowych z formularzy;
- katalogów `vendor`, `node_modules`, logów i plików tymczasowych;
- obrazów bez pozwolenia na użycie.

Przed każdym `git push` uruchom `git status` i przeczytaj listę wysyłanych plików.

## Codzienna checklista Git

- [ ] Rozpocząłem od aktualnej gałęzi `main`.
- [ ] Utworzyłem gałąź zgodną z nazwą w zadaniu.
- [ ] Wykonałem kilka małych commitów z czytelnymi opisami.
- [ ] Sprawdziłem `git status`.
- [ ] Nie dodałem haseł ani danych prywatnych.
- [ ] Wysłałem gałąź i otworzyłem Pull Request.
- [ ] Opisałem sposób sprawdzenia zmiany.

