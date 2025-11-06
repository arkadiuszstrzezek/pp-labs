# Case Study

**Fabrikam Innovations** to firma technologiczna z **20 deweloperami Power Platform**.  
Każdy tworzy prototypy aplikacji i automatyzacji, które są później integrowane w jeden produkt lub rozwiązanie.  
Firma chce umożliwić **indywidualną pracę twórców**, ale utrzymać **kontrolę nad spójnością i zasadami bezpieczeństwa**.

## Wyzwania

- Duża liczba indywidualnych środowisk DEV.  
- Ryzyko niespójności zasad i konektorów.  
- Trudność w integracji aplikacji.  
- Konieczność testowania współdziałania aplikacji przed wdrożeniem.

---

## Strategia środowiskowa

### Struktura

- **Grupa:** Fabrikam Dev Group  
- **Środowiska:** DEV-A, DEV-B, DEV-C (indywidualne dla twórców), TEST, PROD

### Zasady

- Każdy twórca ma pełny dostęp tylko do swojego środowiska **DEV**.  
- Wszystkie środowiska w grupie dziedziczą wspólne **polityki DLP**.  
- **Routing:**  
  - Deweloperzy → do własnych środowisk **DEV**  
  - Zespół integracyjny → **TEST**  
  - Użytkownicy → **PROD**

---

## Schemat przepływu zmian

- Eksport rozwiązania (**Solution**) z indywidualnego środowiska **DEV**.  
- Import do środowiska **TEST** w celu integracji i testów międzyaplikacyjnych.  
- Po zatwierdzeniu – eksport z TEST i import do **PROD**.  
- Wszystkie rozwiązania wersjonowane w repozytorium (np. **Azure DevOps / GitHub**).

---

## Pytania do analizy

1. **Jak grupy środowisk pomagają kontrolować dużą liczbę indywidualnych środowisk DEV?**  
2. **Jak routing środowisk wspiera proces ALM i integracji?**  
3. **Jakie ryzyka wiążą się z indywidualnymi środowiskami twórców?**  
4. **Jakie mechanizmy governance warto wdrożyć?**