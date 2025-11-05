# LAB05: Testowanie mechanizmów administracyjnych Power Platform

Celem laboratorium jest zrozumienie, jak skutecznie zarządzać środowiskiem domyślnym (Default Environment) w Power Platform, w szczególności w kontekście governance, bezpieczeństwa i automatyzacji nadzoru.

---

## Wymagania wstępne
- Konto z rolą Power Platform Service Admin lub Administrator środowiska.
- Windows z PowerShell (uruchom jako Administrator jeśli instalujesz moduły).
- Uprawnienia do instalacji modułów PowerShell (jeśli ich brakuje, poproś administratora).
- Zarządzane środowisko testowe.

---

## Krok 0 — Przygotowanie środowiska PowerShell
1. Otwórz PowerShell (PowerShell 7 lub Windows PowerShell).
2. Zainstaluj (jeśli potrzeba) moduł administracyjny Power Platform i załaduj go:

```powershell
Install-Module -Name Microsoft.PowerPlatform.Administration.PowerShell -Scope CurrentUser -Force
Import-Module Microsoft.PowerPlatform.Administration.PowerShell
```

3. Zaloguj się do Power Platform:

```powershell
Add-PowerAppsAccount
```

(Jeśli Twoje środowisko używa innej komendy logowania, użyj standardowego przepływu logowania administracyjnego.)

---

## LAB 1: Audyt i inwentaryzacja środowiska domyślnego

### Cel
Zrozumienie, jak zebrać dane o wszystkich aplikacjach, przepływach i użytkownikach w środowisku domyślnym oraz jak przeanalizować ich zgodność z polityką organizacji.

### Zakres
PowerShell + Power Platform Admin Center + CoE Starter Kit

### Kroki
1. Uruchom moduł PowerShell `Microsoft.PowerApps.Administration.PowerShell`.
2. Pobierz listę wszystkich środowisk i zidentyfikuj środowisko **Default**:
   ```powershell
   Get-AdminPowerAppEnvironment
   ```
3. Wylistuj wszystkie aplikacje w środowisku domyślnym:
   ```powershell
   Get-AdminPowerApp -EnvironmentName <default_env_id>
   ```
4. Zidentyfikuj właścicieli, daty ostatniego użycia i powiązane konektory.
5. Uruchom raport **CoE Starter Kit (App Inventory)** i porównaj wyniki z danymi PowerShell.
6. Oceń, które aplikacje lub przepływy są „osierocone”.

### Refleksja
- Jakie dane z raportów powinny być częścią cyklicznego audytu governance?
- Jakie ryzyka identyfikujesz przy aplikacjach „bez właściciela”?
- Jak możesz zautomatyzować ten audyt?

---

## LAB 2  — Sprawdzenie stanu kwarantanny aplikacji
Cel: dowiedzieć się, czy wybrana aplikacja znajduje się w kwarantannie.

>**Wskazówka:**
AppName = ef5fad48-4dc8-4e08-8732-2b68bbd54952

>**Wskazówka:**
EnvironmentName = Default-e1c8949c-f766-446b-bfe8-1932fc1143a7 



1. Zidentyfikuj EnvironmentName i AppName (np. z admin center lub z CoE).
2. Uruchom polecenie sprawdzające stan:

```powershell
Get-AppQuarantineState -EnvironmentName "<EnvironmentName>" -AppName "<AppName>"
```

3. Odczyt interpretacji:
- Jeśli wynik pokazuje, że aplikacja jest w kwarantannie — zanotuj powód (jeśli dostępny) i identyfikator.
- Jeśli aplikacja nie jest w kwarantannie — wynik zazwyczaj wskaże stan "Not quarantined" lub brak wpisu.

4. Zadanie dla uczestnika:
- Uruchom powyższe polecenie dla testowej aplikacji i zapisz wynik.
- Jeśli aplikacja jest w kwarantannie, zgłoś to prowadzącemu lub odtwórz scenariusz powiadomień (nie zmieniaj produkcyjnych polityk).

---

## LAB 3 — Dodaj aplikację do kwarantanny

Upewnij się, że pracujesz w środowisku **Default** i utwórz prostą aplikację **Canvass App**. Zapisz ja a następnie Opublikuj.


1. Upewnij się, że masz wartości:
   - EnvironmentName = "<EnvironmentName>"
   - AppName = "<AppName>" (np. "xyz")
2. Umieść aplikację w kwarantannie:

```powershell
Set-AppAsQuarantined -EnvironmentName "<EnvironmentName>" -AppName "<AppName>"
```

3. Oczekiwany efekt: cmdlet potwierdzi operację lub zwróci obiekt stanu kwarantanny.

---

## LAB 4 — Sprawdź stan kwarantanny (Get)
1. Zweryfikuj, że aplikacja jest w kwarantannie:

```powershell
Get-AppQuarantineState -EnvironmentName "<EnvironmentName>" -AppName "<AppName>"
```

2. Odczyt:
   - Szukaj właściwości Status (np. Quarantined), Reason/Comment i Timestamp.  
   - Zapisz wynik (screenshot/kopię tekstową) do raportu ćwiczeniowego.

---

## LAB 5 — Usuń aplikację z kwarantanny (Approve / Unquarantine)
1. Usuń kwarantannę (akcja Approve / Unquarantine):

```powershell
Set-AppAsUnquarantined -EnvironmentName "<EnvironmentName>" -AppName "<AppName>"
```

2. Weryfikacja: ponownie uruchom Get-AppQuarantineState i potwierdź, że Status zmienił się na NotQuarantined lub wpis zniknął:

```powershell
Get-AppQuarantineState -EnvironmentName "<EnvironmentName>" -AppName "<AppName>"
```

---

## Materiały referencyjne
- [Microsoft Learn – Manage the Default Environment](https://learn.microsoft.com/en-us/power-platform/guidance/adoption/manage-default-environment)
- [CoE Starter Kit Documentation](https://learn.microsoft.com/en-us/power-platform/guidance/coe/starter-kit-overview)
- [Power Platform PowerShell Module](https://learn.microsoft.com/en-us/powershell/powerapps/overview)

