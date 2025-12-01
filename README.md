<!-- zadanie-git.md -->

# Zadanie: Git i praca z repozytorium projektowym

Do wykonania zadania przyda się wiedza zawarta na stronie gita.
Sprawdź: [Progit](https://git-scm.com/book/en/v2)

## Zakres praktyczny

1. W terminalu stwórz folder projektu i wejdź do niego 
   - `mkdir zadanie-git` 
   - `cd zadanie-git`

2. Zainicjalizuj repozytorium Git w folderze projektu za pomocą polecenia `git init`

3. Dodaj plik app-info.md z informacjami:
   - nazwa projektu: *Moja aplikacja*
   - technologia (RN / Flutter / NS): *React Native*
   - numer indeksu: *144856*

4. Wykonaj commit o nazwie `initial project setup`:

   - `git add app-info.md`

   - `git commit -m "initial project setup"`

5. Utwórz branch feature/header.
   - `git checkout -b feature/header`

6. W pliku np. Header.js, header.dart lub header.component.ts stwórz prosty komponent nagłówka (dowolna treść).

7. Zrób commit `feat(header): add basic header component`:
   - `git add Header.js`
   - `git commit -m "feat(header): add basic header component"`

8. Wróć na main (w moim przypadku master) i wykonaj merge z feature/header (PR lub lokalnie).
   - `git checkout master`
   - `git merge feature/header`

9. Utwórz branch feature/footer.
   - `git checkout -b feature/footer`

10. Dodaj inny plik komponentu (Footer.js), ale tym razem o konfliktowym fragmencie (np. modyfikacja app-info.md).
    - Stwórz plik `Footer.js`
    - Otwórz plik `app-info.md` i zmień technologię na "Flutter"
  
11. Na branchu master zmodyfikuj plik app-info.md aby stworzyć konflikt
    - Otwórz plik `app-info.md` i zmień technologię na "NativeScript"

12. Zrób commit `feat(footer): add footer component`:
    - `git add Footer.js app-info.md`
    - `git commit -m "feat(footer): add footer component"`

13. Spróbuj scalić z main (master), aby wywołać konflikt.
    - `git checkout master`
    - `git merge feature/footer`

      **Powstał konflikt:**
      > git merge feature/footer;
      > Auto-merging app-info.md;
      > CONFLICT (content): Merge conflict in app-info.md;
      > Automatic merge failed; fix conflicts and then commit the result.

14. Rozwiąż konflikt ręcznie (wybierając odpowiednie części).
    - Otwórz plik `app-info.md`
    - W dokumencie .md pojawiły się znaczniki <<<<<, =======, >>>>>.
    - Usuń je i zostaw wersję poprawną lub je połącz
    - Zapisz plik

15.  Zrób commit po konflikcie `fix: resolve merge conflict in app-info.md`:
     - `git add app-info.md`
     - `git commit -m "fix: resolve merge conflict in app-info.md"`


16.  Dodaj plik .gitignore dopasowany do technologii **React Native:** ignoruj node_modules, android/, ios/, bundlery.
     - `git add .gitignore`
     - `git commit -m "add gitignore for react native"`
<!-- - Flutter: ignoruj .dart_tool, .flutter-plugins, build/ itd.
- NativeScript: ignoruj platforms/, hooks/, node_modules/. -->

17. Skonfiguruj GitHub Actions z prostym workflow, który wykonuje test (npm test, flutter test, ns build — uproszczone).
    - Stwórz `package.json` aby komenda `npm test` faktycznie działała
    - Skonfiguruj `.github/workflows/test.yml`
    - `git add .github package.json`
    - `git commit -m "configure react native workflow"`

18. Otwórz Pull Request z opisem:
    - co zostało zrobione,
    - jakie konflikty rozwiązano,
    - jakie były problemy.    

Wymagania dotyczące commitów

Commity muszą:
- być jasne, zgodne z konwencją Conventional Commits
- oddawać realne kroki prac
- nie zawierać artefaktów build

## Sprawozdanie z zadania

**Imię i nazwisko:** Konrad Krziżok,

**Grupa:** 42_Inf_FD_ST_7_Grupa_6

**Link do repozytorium:** [https://github.com/konrad533/zadanie-git](https://github.com/konrad533/zadanie-git) 

### Cel zadania
> Krótko opisz, czego dotyczyło zadanie i jakie czynności miałeś wykonać.
>
> **Odpowiedź:** Zadanie miało na celu praktyczne przećwiczenie workflow w systemie git. Kluczowymi elementami w tym zadaniu były: inicjalizacja repozytorium projektu, praca na wielu branchach, wywołanie i rozwiązanie konfliktu oraz konfiguracja CI/CD dla ReactNative przy użyciu GitHub Actions i skryptów npm.

### Przebieg pracy

#### Inicjalizacja repozytorium  
> Opisz, jak stworzyłeś repozytorium oraz pierwszy commit.
> 
> **Odpowiedź:** Stworzyłem folder i zainicjowałem repozytorium komendą `git init`. Utworzyłem plik `app-info.md` który dodałem do pierwszego commita - `initial project setup` 

#### Praca na branchach  
> Opisz utworzone branche oraz ich role.
> 
> **Odpowiedź:** Praca odbywała się na trzech gałęziach:
> 1. `master` - główna gałęź posiadająca pliki z obu gałęzi `feature/header` i `feature/footer`
> 2. `feature/header` - gałęź posiadająca komponent nagłówka - `Header.js`.
> 3. `feature/footer` - gałęź posiadająca `Footer.js` czyli stopkę. Na tej gałęzi był również wywoływany celowy konflikt merge z główną gałęzią `master` poprzez zmianę nazwy technologii w `app-info.md`

#### Konflikt i jego rozwiązanie  
> Wyjaśnij, w jaki sposób powstał konflikt i jak go rozwiązałeś.
> 
> **Odpowiedź:** Konflikt został wywołany celowo poprzez równoległą edycję pliku `app-info.md`:
> * Na gałęzi `feature/footer` zmieniłem technologię z **React Native** na **Flutter**.
> * Na głównej gałęzi `master` zmieniłem technologię z **React Native** na **NativeScript**.
> Podczas próby mergu `feature/footer` z `master` git wykrył konflikt w lini technologii. Konflikt został rozwiązany poprzez zostawienie obu wersji gałęzi w pliku `app-info.md`

#### Pull Request
> Opisz treść i cel PR.
> 
> **Odpowiedź:** 
> **Co zostało zrobione:**
> 1. Stworzono i zaimplementowano komponent stopki - `Footer.js` na dedykowanej gałęzi `feature/footer`.
> 2. Dodano plik `.gitignore` skonfigurowany pod projekt React Native (ignorowanie `node_modules`, folderów `android/`, `ios/`).
> 3. Wdrożono automatyzację CI/CD poprzez GitHub Actions: utworzono workflow `.github/workflows/test.yml` oraz plik `package.json`, co pozwala na automatyczne uruchamianie testów za pomocą `npm test` przy każdym poleceniu push.
>
> **Jakie konflikty rozwiązano:**
> Rozwiązano konflikt w pliku `app-info.md` wynikający z równoległej edycji na dwóch gałęziach. Na gałęzi `feature/footer` technologia w pliku `app-info.md` została zmieniona na "Flutter", natomiast na gałęzi `master` na "NativeScript". Konflikt rozwiązano ręcznie w edytorze pozostawiając wpisy z obu gałęzi.
>
> **Jakie były problemy:**
> Głównym problemem była konfiguracja uwierzytelniania do zdalnego repozytorium GitHub. Wystąpił błąd uprawnień - `refusing to allow an OAuth App to create or update workflow`, który wymagał wygenerowania nowego tokena PAT z uprawnieniami `workflow` oraz zalogowania się na nowo za pomocą nowego tokenu z uprawnieniami.

### Drzewo commitów

(Wklej wynik polecenia)
`git log –-oneline –-graph`
* f582e6f (HEAD -> master) configure react native workflow
* 7a59cf0 add gitignore for react native
*   ea72560 fix: resolve merge conflict in app-info.md
|\  
| * be9a856 (feature/footer) feat(footer): creat conflict in .md
| * 20ec60c feat(footer): added conflict to app-
| * a070c33 feat(footer): add footer component
* | 5e290e4 change technology to NativeScript to cause conflict
|/  
* 0f63cfe (feature/header) feat(header): add basic header component
* 9d73cf2 initial project setup
---
* be9a856 (HEAD -> feature/footer) feat(footer): creat conflict in .md
* 20ec60c feat(footer): added conflict to app-
* a070c33 feat(footer): add footer component
* 0f63cfe (feature/header) feat(header): add basic header component
* 9d73cf2 initial project setup
---
* 0f63cfe (HEAD -> feature/header) feat(header): add basic header component
* 9d73cf2 initial project setup


### Refleksja
> Czego nauczyłeś się z tej pracy? Co sprawiło trudność? Jak oceniasz swoje zrozumienie Gita?
>
> **Odpowiedź:** Zadanie pozwoliło mi na poszerzenie wiedzy i umiejętności praktycznych na temat podstawowych operacji w Gicie. Najwięcej nauczyłem się konfigurując **CI/CD** - stworzenie działającego workflow w GitHub Actions i pliku `package.json` było dla mnie nowością.
> 
> Największą trudność sprawiły mi problemy techniczne z uwierzytelnianiem (błędy uprawnień tokena przy wysyłaniu plików workflow).
> 
> Swoje zrozumienie Gita oceniam jako dobre - potrafię sprawnie zarządzać repozytorium, a teraz dodatkowo wiem, jak podpiąć pod nie automatyzację.