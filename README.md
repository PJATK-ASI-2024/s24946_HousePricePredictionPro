## Dokumentacja Projektu

### 1. Opis projektu

**Nazwa projektu:**  
Przewidywanie cen nieruchomości (lub dowolna inna nazwa odpowiadająca zakresowi tematycznemu).

**Cel projektu:**  
Projekt został stworzony w celu zbudowania modelu predykcyjnego, który umożliwi przewidywanie cen nieruchomości na podstawie historycznych danych o transakcjach,
parametrach lokalizacji oraz cech nieruchomości (np. liczba pokoi, wielkość działki, rok budowy). Wiedza o prognozowanych cenach może pomóc pośrednikom, inwestorom,
a także osobom prywatnym w podejmowaniu lepszych decyzji dotyczących kupna czy sprzedaży nieruchomości.

**Kluczowe korzyści i zastosowania:**
- Ułatwienie analizy rynku nieruchomości i monitorowanie trendów cenowych.  
- Zmniejszenie ryzyka inwestycyjnego poprzez wskazanie nieruchomości o największym potencjale wzrostu wartości.  
- Automatyzacja czasochłonnych procesów wyceny nieruchomości przez banki lub agencje nieruchomości.

### 2. Dane

**Źródło danych:**  
- [Kaggle: House Prices - Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)  
  *LUB*  
- Zewnętrzna baza danych z urzędów nieruchomości / API dostarczające dane o transakcjach nieruchomości  
  *(w zależności od konkretnego źródła)*.

**Charakterystyka danych:**
- **Dane tabelaryczne** zawierające informacje o nieruchomościach:  
  - Identyfikator nieruchomości (ID).  
  - Parametry budynku (powierzchnia, liczba pokoi, rok budowy itp.).  
  - Informacje o lokalizacji (np. miasto, dzielnica, współrzędne geograficzne).  
  - Dane rynkowe (cena, data transakcji).  
- **Liczba rekordów**:  
  - Zależnie od źródła — w przypadku przykładowego zbioru z Kaggle jest to ponad 2000 wierszy (rekordów), co spełnia wymagania minimalne dla danych tabelarycznych.  
- **Format danych**: najczęściej plik CSV, który może być łatwo wczytany i przetwarzany w języku Python z wykorzystaniem bibliotek takich jak `pandas`.

**Powody wyboru danego zbioru danych:**
1. **Dostępność** – Dane są publicznie dostępne i łatwo je pobrać z platformy Kaggle (lub innego źródła).  
2. **Adekwatność** – Zawierają informacje istotne dla wyceny nieruchomości (cechy fizyczne domu, parametry lokalizacji, ceny transakcyjne).  
3. **Skalowalność** – Można w razie potrzeby rozbudować projekt o dodatkowe dane (np. dane gospodarcze, statystyki demograficzne).  

---
**Opis modelu: Jakiego modelu użyto i dlaczego**

W projekcie zdecydowano się na zastosowanie **StackingRegressor**, czyli metody zespołowej (ensemble), łączącej prognozy kilku różnych algorytmów bazowych w celu uzyskania bardziej precyzyjnych wyników. 

1. **Czym jest StackingRegressor?**  
   - *Stacking* (lub *stacked generalization*) to podejście, w którym wykorzystuje się wiele różnych modeli (tzw. estymatory bazowe), 
    a ich wyjścia są następnie przetwarzane przez model nadrzędny (tzw. meta-estymator).  
   - Meta-estymator uczy się optymalnego sposobu łączenia prognoz poszczególnych modeli bazowych. Dzięki temu może on kompensować słabości jednych modeli mocnymi stronami innych.  

2. **Dlaczego użyto StackingRegressor w tym projekcie?**  
   - **Lepsza wydajność**: Wstępne testy pokazały, że pojedyncze modele, takie jak *LinearSVR* czy *RandomForestRegressor*, choć osiągały przyzwoite wyniki, 
    nie dorównywały kombinacji kilku algorytmów. StackingRegressor potrafił wyciągnąć korzyści z różnych perspektyw predykcyjnych (np. drzew decyzyjnych, modeli liniowych), poprawiając ostateczną trafność prognoz.  
   - **Różnorodność modeli bazowych**: Dzięki użyciu modeli o różnej naturze (np. model liniowy, model drzewiasty), StackingRegressor może skuteczniej uogólniać zależności w danych. 
    Jeżeli jeden typ modelu pomija pewne wzorce w danych, drugi może je przechwycić, a meta-estymator wyważy ostateczną predykcję.  
   - **Elastyczność**: StackingRegressor pozwala na łatwe skalowanie i dopasowywanie liczby modeli bazowych. Można też dołożyć nowy model bazowy, jeśli okaże się, że wnosi dodatkową wartość do zespołu.  
   - **Stabilizacja wyników**: Zespół modeli zazwyczaj jest bardziej odporny na specyficzne błędy poszczególnych algorytmów (np. przeuczenie). Dzięki temu końcowa predykcja bywa stabilniejsza i dokładniejsza.

3. **Podsumowanie zalet StackingRegressor dla danych z housing.csv**  
   - **Wielowymiarowość problemu**: Dane o nieruchomościach zawierają zarówno cechy liniowo powiązane z ceną (np. powierzchnia), jak i potencjalnie nieliniowe (np. interakcje między cechami lokalizacyjnymi). 
    Stacking może łączyć modele liniowe i nieliniowe, by uchwycić różnorodne wzorce.  
   - **Niejednorodność cech**: Niektóre cechy mogą być skwantyfikowane liczbowo (powierzchnia, liczba pokoi), inne są kategoryczne (np. rodzaj ogrzewania, parking). 
    Dzięki połączeniu np. modelu drzewiastego (dobrego w obsłudze cech kategorycznych) oraz liniowego (dobrego w interpretacji wpływu konkretnych zmiennych liczbowych) zyskuje się większą dokładność.  
   - **Lepsza generalizacja**: W porównaniu do pojedynczych algorytmów, StackingRegressor często zapewnia lepszą zdolność do prognozowania cen nowych nieruchomości, których model nie widział w trakcie trenowania.

**Pobieranie i uruchamianie aplikacji**

1. zależnie do czego chcemy użyć aplikacji 

1. Pobieranie Aplikacji z GitHub

Wejdź na github w repozytorium aplikacji oraz zklonuj repozytorium.

Zależnie do czego chcesz ją wykorzystać wejdź w odpowiedni branch.

Jeśli chcesz pracować z dagami polecam pobrać docker-desktop. Używaj komend w cmd "docker-compose build", a następnie "docker-compose up -d" i wejdź na adres podany airflow. 
Login i hasło to "airflow". Korzystaj z dostępnych dagów.

Analize i modele danych jest w branchu "Projekt-2" jak i również raport z analizy modeli.


