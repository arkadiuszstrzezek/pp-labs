# LAB03: Tworzenie reguły alertu w Power Platform
Data: 2025-10-29

## Cel ćwiczenia
Utworzenie reguły alertu monitorującej wydajność aplikacji w środowisku produkcyjnym. Alert będzie informował gdy liczba uruchomień aplikacji przekroczy 50 dziennie.

## Wymagania wstępne
- Konto z uprawnieniami administratora tenant lub środowiska
- Dostęp do Power Platform Admin Center
- Zarządzane środowisko produkcyjne

## Scenariusz ćwiczenia
Jako administrator chcesz monitorować wykorzystanie aplikacji w środowisku produkcyjnym. Utworzysz alert, który powiadomi Cię email-em gdy jakakolwiek aplikacja canvas przekroczy 50 uruchomień dziennie.

## Krok 1: Dostęp do sekcji alertów
1. Otwórz [Power Platform Admin Center](https://admin.powerplatform.microsoft.com)
2. Z menu po lewej wybierz **Monitor**
3. W sekcji Monitor kliknij **Alerts**

## Krok 2: Tworzenie reguły alertu
1. Kliknij przycisk **+ Alert rule**
2. Wypełnij formularz:
   - Alert rule name: "High App Usage Alert"
   - Product: Power Apps
   - Product type: Canvas app
   - Scope: Environment
   - Identifier: [wybierz swoje środowisko produkcyjne]
   - Metric: Daily active users
   - Operator: Is above
   - Value: 50
   - Severity: High
   - Notification type: Email
   - Recipients: [twój email służbowy]
3. Kliknij **Save**

## Weryfikacja
- Sprawdź czy alert pojawił się na liście w zakładce "Alert rules"
- Status alertu powinien być "Active"
- Możesz przetestować alert zmniejszając próg do niższej wartości, aby wymusić jego wyzwolenie

## Modyfikacja alertu (opcjonalnie)
1. Na liście alertów znajdź utworzoną regułę
2. Użyj ikony "More actions" (...)
3. Wybierz "Edit"
4. Możesz zmienić:
   - Próg (value)
   - Ważność (severity)
   - Dodać więcej odbiorców email (max 4)

## Czego się nauczyłeś
- Jak tworzyć reguły alertów w Power Platform
- Jak monitorować wykorzystanie aplikacji
- Jak konfigurować powiadomienia email dla alertów

## Zadanie dodatkowe
Utwórz drugi alert monitorujący czas ładowania aplikacji (metric: app load time) z progiem 5 sekund.

## Przydatne linki
- [Dokumentacja alertów Power Platform](https://learn.microsoft.com/power-platform/admin/alerts)
- [Metryki dla Power Apps](https://learn.microsoft.com/power-apps/maker/monitor-apps)

---

**Tip**: Zapisz w notatkach utworzone alerty i ich progi - przyda się to przy dokumentacji środowiska.