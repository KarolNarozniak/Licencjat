# Analiza Wydatków na Opiekę Zdrowotną - Praca Licencjacka 2025

## Opis Projektu

Projekt analizuje czynniki wpływające na wydatki gospodarstw domowych na opiekę zdrowotną. Analiza opiera się na danych z badania budżetów gospodarstw domowych, zawierających informacje o charakterystykach społeczno-demograficznych oraz wydatkach na usługi medyczne.

## Struktura Danych

Dane zawierają następujące zmienne:

- **Zmienne demograficzne:**

  - `nr_gosp` - numer gospodarstwa domowego
  - `plec` - płeć respondenta
  - `wiek` - wiek respondenta
  - `wyksz` - wykształcenieś
  - `inwalidztwo` - status niepełnosprawności
  - `liczba_osob` - liczba śosób w gospodarstwie domowym

- **Zmienne ekonomiczne:**

  - `doch_calkowity` - całkowity dochód gospodarstwa
  - `doch_os` - dochód na osobę
  - `wyd_calkowite` - całkowite wydatki
  - `wyd_os_lek` - wydatki na opiekę zdrowotną na osobę

- **Zmienne kategoryczne:**
  - `klasa_miejsca` - wielkość miejscowości
  - `syt_mat` - sytuacja materialna
  - `glowne_zrod_utrzym` - główne źródło utrzymania
  - `moz_oszcz` - możliwości oszczędzania

## Metodologia

Projekt wykorzystuje następujące metody analizy:

1. **Analiza opisowa** - statystyki podstawowe i wizualizacje
2. **Analiza korelacji** - badanie zależności między zmiennymi
3. **Modelowanie regresji** - analiza wpływu różnych czynników na wydatki zdrowotne

## Wymagania

Projekt wymaga następujących bibliotek Pythona:

- pandas
- numpy
- matplotlib
- seaborn
- scipy
- scikit-learn
- statsmodels
- stargazer
- openpyxl
- jupyter

## Instalacja

1. Sklonuj repozytorium
2. Zainstaluj wymagane biblioteki:

```bash
pip install -r requirements.txt
```

## Uruchomienie

1. Otwórz notebook `Model_lekarz_Licencjat.ipynb` w Jupyter Notebook
2. Uruchom wszystkie komórki w kolejności

## Struktura Analizy

1. **Przygotowanie danych**

   - Wczytanie i wstępna eksploracja danych
   - Kodowanie zmiennych kategorycznych
   - Transformacja zmiennych

2. **Analiza statystyczna**

   - Statystyki opisowe
   - Testy normalności rozkładu
   - Analiza korelacji

3. **Modelowanie**

   - Budowa modeli regresji
   - Weryfikacja założeń
   - Interpretacja wyników

4. **Wizualizacje**
   - Wykresy rozkładów
   - Wykresy zależności
   - Wizualizacja wyników modelowania

## Wyniki

Projekt dostarcza szczegółowej analizy czynników wpływających na wydatki na opiekę zdrowotną, w tym:

- Wpływ sytuacji materialnej
- Wpływ wykształcenia
- Wpływ miejsca zamieszkania
- Wpływ źródła utrzymania

## Autor

Katarzyna Olbryś

## Licencja

[MIT License]
