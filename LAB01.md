# Konfiguracja Power BI dla CoE Starter Kit
Data: 2025-08-18

## Przegląd
Ten przewodnik opisuje kroki konfiguracji pulpitu Power BI dla Center of Excellence (CoE) Starter Kit. Dashboard daje przegląd zasobów tenant-a: środowiska, aplikacje, Power Automate flows, konektory, connection references, twórców (makers) oraz logi audytu. Telemetria z logu audytu umożliwia analizę trendów w czasie.
![Pulpit CoE Starter Kit — Power BI](/media/pb-1.png)

_Rys. 1 — Pulpit CoE Starter Kit Power BI_

Link: film — krótki przewodnik wideo (opcjonalnie)

---

## Który dashboard wybrać?
Pobierz CoE Starter Kit: https://aka.ms/CoeStarterKitDownload

Plik ZIP zawiera szablony Power BI (.pbit):
- `Production_CoEDashboard_MMMYY.pbit` — użyj, jeśli źródłem danych jest Inventory z cloud flows.
- `BYODL_CoEDashboard_MMMYY.pbit` — użyj, jeśli źródłem jest Data Export.
- `PowerPlatformGovernance_CoEDashboard_MMMYY.pbit` — dodatkowy dashboard dla raportów governance/compliance.

---

## Wymagania wstępne
- Zainstalowany CoE core components solution.
- Uruchomiony CoE Setup and Upgrade Wizard.
- Dopuszczone do działania core components solution sync flows (pozwól na ukończenie ich wykonania).
- Skonfigurowana sekcja Audit Log w rozwiązaniu, aby widzieć dane o użyciu aplikacji (np. last launched).

---

## Pobierz URL środowiska
Power BI łączy się z tabelami Dataverse w środowisku, gdzie zainstalowano CoE.

1. Zaloguj się do Power Platform admin center.
2. W menu wybierz **Manage** → **Environments**.
3. Wybierz środowisko, gdzie jest zainstalowany CoE.
4. Skopiuj pole Organization URL z okna szczegółów. Dodaj przedrostek `https://` i końcowy slash `/` (np. `https://contoso.crm.dynamics.com/`).

![Wstaw zrzut ekranu Power Platform admin center z podświetlonym Environment URL](/media/coe19.png)

Uwaga: jeśli URL jest obcięty, kliknij **See all**, aby wyświetlić pełny adres.

![Wstaw zrzut ekranu Settings → Environment details](/media/coe20.png)

---

## Konfiguracja Production i Governance Power BI dashboard
Możesz edytować pbit bezpośrednio w Power BI Desktop, aby dopasować branding, strony i wizualizacje.

Kroki:
1. Pobierz i zainstaluj Microsoft Power BI Desktop.
2. Otwórz w Power BI Desktop odpowiedni plik `.pbit` z paczki CoE Starter Kit.
3. Wprowadź wartość parametru OrgUrl — pełny URL środowiska (z `https://`).
4. (Production pbit) Wybierz Tenant Type: domyślnie `Commercial`. Jeśli używasz chmury suwerennej, zmień selektor.
5. Jeśli pojawi się monit, zaloguj się kontem organizacyjnym posiadającym dostęp do środowiska CoE.
![Wstaw zrzut ekranu pola parametru OrgUrl w Power BI Desktop](/media/pbit.png)

6. Zapisz plik lokalnie lub wybierz **Publish** i wskaż workspace, gdzie opublikować raport (np. Power BI service).
   - Tip: jeśli chcesz zachować stały URL raportu między aktualizacjami, nadaj stałą nazwę (np. "Contoso CoE Governance") i kopiuj ją przy każdym miesiącu.
7. Skonfiguruj scheduled refresh dla datasetu, np. codzienny, aby raport był aktualizowany.
8. Raport można odnaleźć później w https://app.powerbi.com

---

## Pytania do sprawdzenia aplikacji Power Apps i Copilot
Aby zidentyfikować liczbę aplikacji i wykorzystanie Copilot, odpowiedz na poniższe pytania podczas przeglądu środowisk/Dataverse:

1. Ile jest łącznie aplikacji Power Apps w tenancie?  
2. Ile aplikacji Power Apps znajduje się w środowisku Project?
1. W których środowiskach znajdują się aplikacje z Copilot — podaj liczbę aplikacji z Copilot per środowisko.

## Źródła
- Pobierz CoE Starter Kit: https://aka.ms/CoeStarterKitDownload  
- Power BI: https://powerbi.microsoft.com  
- Power Platform admin center: https://admin.powerplatform.microsoft.com

```
https://learn.microsoft.com/en-us/power-platform/guidance/coe/setup-powerbi