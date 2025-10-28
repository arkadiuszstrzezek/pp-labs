# Instrukcja: CoE Environment Request — krok po kroku
Data: 2025-10-28

Ten dokument prowadzi użytkownika (maker) i administratora CoE przez przykładowy proces zgłoszenia i zatwierdzenia utworzenia środowiska przy użyciu aplikacji CoE Maker Command Center (zgłoszenie) oraz CoE Admin Environment Request (zatwierdzenie).

## Szybkie podsumowanie ról i wymagań
- Maker: składa prośbę przez CoE Maker Command Center. Wymagana rola: Power Platform Maker SR. Licencja: Per User (lub Per App / pay-as-you-go dla środowiska).
- Admin CoE: przegląda i zatwierdza/rejectuje w CoE Admin Environment Request. Wymagana rola: Power Platform Service Admin lub odpowiednie uprawnienia administratorskie.
- Wymagane: Dataverse (tabele CoE), zainstalowany CoE core components.

---

## Scenariusz przykładowy (cel)
Utworzyć środowisko deweloperskie dla zespołu „SalesApps” w regionie „West Europe”, z dostępem do konektorów: SharePoint, SQL, Teams. Potrzeba przypisania właściciela, określenia polityki DLP i daty wygaśnięcia środowiska (6 miesięcy).

---

## Krok 1 — Przygotowanie zgłoszenia (Maker)
1. Otwórz CoE Maker Command Center.
2. Przejdź do strony "Environment Creation Requests".
3. Kliknij "New Request" lub "Create".
4. Wypełnij pola (przykładowe pola i przykładowe wartości):
   - Request title: "Dev — SalesApps — West Europe"
   - Business justification: "Potrzeba środowiska deweloperskiego dla zespołu SalesApps do budowy i testów integracji z SharePoint i SQL"
   - Environment type: Development (lub Trial / Production zależnie od potrzeby)
   - Region: West Europe
   - Requested owner: jan.kowalski@contoso.com
   - Environment administrators: lista adminów (emails)
   - Required connectors: SharePoint, SQL Server, Microsoft Teams
   - DLP policy notes: "allow SharePoint; restrict SQL do konektora zwhitelistowanym connection reference"
   - Estimated users: 5
   - Requested start date: yyyy-mm-dd
   - Expiration / review date: yyyy-mm-dd (np. +180 dni)
   - Cost center / business unit: (jeśli wymagane)
   - Attachments: diagramy/uzasadnienia (opcjonalnie)
5. Zweryfikuj dane i kliknij "Submit".
6. Otrzymasz potwierdzenie zgłoszenia i numer requestu. Zachowaj go do komunikacji z administracją.

Tip: Dołącz wszystkie wymagane informacje, aby przyspieszyć weryfikację (konto właściciela, listę konektorów, wymogi DLP, cost center).

---

## Krok 2 — Weryfikacja i decyzja (Admin CoE)
1. Otwórz CoE Admin Environment Request app.
2. Na liście znajdź nowe zgłoszenie (Status = Pending).
3. Otwórz szczegóły zgłoszenia i sprawdź:
   - Czy właściciel i admini mają wymagane uprawnienia/licencje?
   - Czy region i typ środowiska są zgodne z polityką organizacji?
   - Czy wymagane konektory nie są zablokowane przez aktualne/potencjalne DLP?
   - Czy koszt i cost center są zatwierdzone?
   - Czy istnieją konflikty nazw środowisk?
4. Sprawdź tabelę DLP Policy Change Request w aplikacji — jeśli wymagane są modyfikacje polityki, zaktualizuj je w aplikacji (te zmiany zapiszą żądanie i zaktualizują polityki).
5. Opcje:
   - Approve: nadaj environmencie finalną nazwę, ustaw datę ważności/retencji i zaakceptuj. System utworzy środowisko lub administrator przystąpi do ręcznego utworzenia (zależnie od procesu organizacji).
   - Reject: podaj powód i (opcjonalnie) poproś o uzupełnienia (np. brak cost center, blokowane konektory).
6. Po decyzji wysyłany jest e‑mail/notification do zgłaszającego z informacją o statusie i dalszych krokach.

Checklista przed zatwierdzeniem:
- [ ] Właściciel ma licencję Per User lub środowisko objęte pay-as-you-go
- [ ] Konektory zgodne z DLP (nieblokowane)
- [ ] Region i typ środowiska zgodne z zasadami firmy
- [ ] Cost center / budżet potwierdzone
- [ ] Nazwa środowiska nie koliduje z istniejącymi

---

## Krok 3 — Co zrobić po zatwierdzeniu
1. Utworzone środowisko: przypisz właściciela i członków (security roles).
2. Skonfiguruj DLP zgodnie z wymaganiami zapisanymi w zgłoszeniu.
3. Udostępnij lub zainstaluj starter apps / szablony, jeśli wymagane.
4. Dodaj notatkę z datą przeglądu/wygaśnięcia w CoE (upewnij się, że istnieje proces lifecycle).
5. Powiadom zgłaszającego o dostępie i zamknij zgłoszenie w aplikacji (status = Completed).

---

## Krok 4 — Przykładowy workflow (szybkie podsumowanie)
1. Maker: utwórz request → wypełnij wszystkie pola → submit.
2. Admin: otwórz request → przegląd → sprawdź DLP/konektory/licencje → approve/reject.
3. Jeśli approve → utwórz środowisko, skonfiguruj polityki, przypisz role → powiadom maker.
4. Jeśli reject → zwróć szczegółowe uwagi i poproś o korekty.

---

## Wzór przykładowego zgłoszenia (tekst)
Request title: Dev — SalesApps — West Europe  
Business justification: Development environment for SalesApps team to develop and test integrations with SharePoint and SQL.  
Environment type: Development  
Region: West Europe  
Owner: jan.kowalski@contoso.com  
Admins: [anna.nowak@contoso.com]  
Required connectors: SharePoint, SQL Server, Microsoft Teams  
DLP requirement: Allow SharePoint and Teams; restrict SQL to whitelisted connection refs  
Estimated users: 5  
Start date: 2025-11-01  
Expiration: 2026-05-01  
Cost center: CC-12345

---

## Częste problemy i wskazówki
- Brak licencji właściciela → zgłoszenie odrzucone: poproś o przypisanie licencji Per User lub użyj pay-as-you-go.
- Konektory zablokowane przez DLP → zmodyfikuj DLP lub zaprojektuj bezpieczne connection references; skonsultuj z administratorem bezpieczeństwa.
- Konflikt nazw środowisk → użyj schematu nazewnictwa (np. env-{team}-{type}-{region}).
- Chcesz zachować środowisko dłużej → ustaw politykę lifecycle i mechanizm odnowienia przed datą wygaśnięcia.

---

## Linki i źródła
- CoE Starter Kit: https://aka.ms/CoeStarterKitDownload  
- Dokumentacja Environment Request (MS Learn): https://learn.microsoft.com/power-platform/guidance/coe/environment-request  
- Power Platform admin center: https://admin.powerplatform.microsoft.com

---


## Linki i źródła
- CoE Starter Kit: https://aka.ms/CoeStarterKitDownload  
- Dokumentacja Environment Request (MS Learn): https://learn.microsoft.com/power-platform/guidance/coe/environment-request  
- Power Platform admin center: https://admin.powerplatform.microsoft.com

---