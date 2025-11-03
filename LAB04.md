# Instrukcja krok-po-kroku — Dataverse for Teams + prosta Canvas App do zarządzania pojazdami (PL)

Poniżej znajdziesz kompletny, praktyczny przewodnik od utworzenia zespołu w Microsoft Teams, przez zrobienie prostej aplikacji Canvas (formularz + galeria + etykiety) powiązanej z tabelą Dataverse for Teams, aż po opublikowanie aplikacji dla wszystkich w zespole i **promowanie/ przeniesienie** rozwiązania do środowiska produkcyjnego. Tam, gdzie to ważne, podaję odwołania do dokumentacji Microsoftu.

> Krótka uwaga przed startem: Dataverse for Teams (DVfT) tworzy się automatycznie dla zespołu w momencie tworzenia pierwszej aplikacji w Teams. Musisz mieć odpowiednie licencje Power Platform/Teams (sprawdź politykę licencyjną w swojej organizacji).

---

## A. Utworzenie zespołu w Microsoft Teams
1. Otwórz Microsoft Teams i zaloguj się (konto Microsoft 365 z prawami do tworzenia zespołów).  
2. W lewym pasku wybierz **Teams** → kliknij **Dołącz lub utwórz zespół** (Join or create team) → **Utwórz zespół** (Create team).  
3. Wybierz: *Utwórz od zera* (From scratch) lub na podstawie istniejącej grupy. Wpisz nazwę (np. **Fleet Management**), opis, ustaw prywatność (Public/Private).  
4. Dodaj członków zespołu (użytkownicy, którzy będą korzystać z aplikacji). Zatwierdź.

---

## B. Utworzenie Dataverse for Teams + nowej aplikacji Canvas w Teams
> Gdy po raz pierwszy utworzysz aplikację w danym zespole, DVfT środowisko zostanie utworzone automatycznie (może chwilę potrwać).

1. W Teams, w lewym panelu kliknij **Aplikacje** (Apps) → wyszukaj **Power Apps** i dodaj ją do Teams (jeśli jeszcze nie ma).  
2. Otwórz **Power Apps** w Teams → kliknij **Start now** → wybierz z listy zespół, w którym chcesz utworzyć aplikację (np. *Fleet Management*) → **Create**. Podaj nazwę aplikacji, np. **FleetTracker**.  
3. Po chwili (po utworzeniu środowiska) zostaniesz przeniesiony do kreatora — wybierz **Canvas app** (domyślnie Power Apps Studio w Teams).  

---

## C. Utworzenie tabeli Dataverse „Vehicles” (Pojazdy)
1. W kreatorze aplikacji (albo w portalu Power Apps w Teams) wybierz **Add table** / **Create table**. Nazwij tabelę: **Vehicles** lub **Pojazdy**.  
2. Dodaj kolumny (przykładowy zestaw kolumn):
   - `VehicleId` — typ: Autonumber (klucz, opcjonalnie)
   - `Name` — Single line of text (np. "Ford Transit")
   - `RegistrationNumber` — Single line of text
   - `Make` — Single line of text
   - `Model` — Single line of text
   - `Year` — Number
   - `Status` — Choice (Dostępny / W użyciu / Serwis)
   - `Notes` — Multiline text  
   Zapisz tabelę i utwórz kilka przykładowych rekordów (testowych).

---

## D. Zbudowanie prostej Canvas App (ekrany, etykiety, formularz, galeria)
Poniżej krok po kroku w Power Apps Studio w Teams.

### 1. Struktura aplikacji
- **Ekran główny (Home)**: nagłówek + przycisk „Dodaj pojazd” + galeria listująca pojazdy.
- **Ekran edycji/dodawania (EditForm)**: formularz powiązany z tabelą Vehicles.
- **Ekran detali (Details)**: opcjonalnie — szczegóły pojazdu.

### 2. Dodać galerię powiązaną z tabelą Dataverse
1. Na ekranie głównym wstaw komponent **Gallery** (Vertical gallery).  
2. W **Items** galerii ustaw źródło danych: `Vehicles` (wybierz tabelę Dataverse utworzoną wcześniej). Po chwili w galerii pojawią się pola.  
3. Dostosuj layout galerii: pokaż `Name`, `RegistrationNumber`, `Status`. Możesz dodać etykiety (Labels) wewnątrz szablonu galerii i ustawić ich `Text` na np.:  
   - `ThisItem.Name`  
   - `ThisItem.RegistrationNumber`  
   - `ThisItem.Status.Value` (jeśli Choice)

### 3. Dodać formularz (edit/new)
1. Wstaw **Edit form** na osobny ekran (np. `EditVehicleForm`).  
2. Ustaw właściwość `DataSource` formularza na `Vehicles`.  
3. Wybierz pola, które mają się pojawić w formularzu (Name, RegistrationNumber, Make, Model, Year, Status, Notes).  
4. Dodaj przyciski: **Save** i **Cancel**.  
   - `Save` → akcja: `SubmitForm(EditForm1)`  
   - `Cancel` → `ResetForm(EditForm1); Navigate(HomeScreen, ScreenTransition.None)`

### 4. Przejścia i logika
- Kliknięcie elementu w galerii: `OnSelect` → `Set(varSelectedVehicle, ThisItem); Navigate(DetailScreen, ScreenTransition.Fade)`  
- Kliknięcie „Add new”: `NewForm(EditForm1); Navigate(EditVehicleForm, ScreenTransition.None)`  
- Kliknięcie „Edit” w detalu: `EditForm(EditForm1); Navigate(EditVehicleForm, ScreenTransition.None)`  

### 5. Etykiety i wygląd
Wstaw etykietę nagłówkową na ekranie: `Text = "FleetTracker — Pojazdy"`. Dostosuj czcionki i ułożenie. Nie zapomnij zapisać aplikacji regularnie (File → Save).

---

## E. Testowanie aplikacji
1. W Power Apps Studio użyj przycisku **Play** (preview) i przetestuj: wyświetlanie listy, otwieranie detali, dodawanie nowego pojazdu, edycję, zapis.  
2. Upewnij się, że rekordy pojawiają się w tabeli Dataverse for Teams (możesz sprawdzić dane tabeli w zakładce *Tables* w Power Apps w Teams).

---

## F. Publikacja aplikacji do zespołu Teams (udostępnienie wszystkim w zespole)
1. W Power Apps w Teams (gdzie edytowałeś aplikację) wybierz **Publish** → **Publish to Teams** (lub opcję **Share** / **Publish**).  
2. Wybierz, czy chcesz dodać aplikację jako **karta** do konkretnego kanału (np. `General`) lub udostępnić w katalogu aplikacji zespołu.  
3. Ustaw uprawnienia: zwykle członkowie zespołu automatycznie otrzymają dostęp, ale możesz też dodatkowo udostępnić aplikację użytkownikom spoza zespołu (opcjonalnie).

---

## G. Promocja środowiska do produkcyjnego (ALM)
### Opcja 1 — Eksport/import rozwiązania
1. W DVfT utwórz **Solution** i dodaj tabelę Vehicles, formularze, widoki, aplikację Canvas.  
2. Eksportuj rozwiązanie jako plik (Managed lub Unmanaged).  
3. W środowisku produkcyjnym Dataverse zaimportuj plik.  
4. Skonfiguruj uprawnienia i publikuj aplikację.

### Opcja 2 — Upgrade środowiska DVfT
Administrator może zaktualizować środowisko Teams do pełnego Dataverse w centrum admina Power Platform.

---

## H. Checklist przed promocją
- [ ] Wszystkie kolumny wspierane w Dataverse
- [ ] Rozwiązanie eksportowane jako managed
- [ ] Role i uprawnienia skonfigurowane
- [ ] Konektory działają poprawnie
- [ ] Plan backup/restore i monitoring

---

## I. Podsumowanie
1. Utworzyłeś zespół w Teams.  
2. Utworzyłeś środowisko Dataverse for Teams i tabelę Vehicles.  
3. Zbudowałeś aplikację Canvas (galeria, formularz, etykiety).  
4. Opublikowałeś ją w Teams.  
5. Przygotowałeś środowisko do promocji produkcyjnej.