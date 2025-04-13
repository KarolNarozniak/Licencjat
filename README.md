# Analiza Wydatków na Opiekę Zdrowotną - Praca Licencjacka 2025

## Opis Projektu

Projekt ma na celu analizę czynników wpływających na wydatki gospodarstw domowych na opiekę zdrowotną. Dane pochodzą z badania budżetów domowych, zawierających szczegółowe informacje demograficzne, ekonomiczne oraz dotyczące sposobu oszczędzania. Kluczowym celem analizy jest określenie, jakie zmienne (np. wiek, dochód, wykształcenie, miejsce zamieszkania, źródło utrzymania) mają największy wpływ na wydatki na opiekę zdrowotną.

## Struktura Danych

W zbiorze występują trzy główne typy zmiennych:

- **Demograficzne:**

  - `nr_gosp` – numer gospodarstwa
  - `plec` – płeć
  - `wiek` – wiek
  - `wyksz` – poziom wykształcenia
  - `inwalidztwo` – status niepełnosprawności
  - `liczba_osob` – liczba osób w gospodarstwie

- **Ekonomiczne:**

  - `doch_calkowity` – łączny dochód gospodarstwa
  - `doch_os` – dochód na osobę
  - `wyd_calkowite` – całkowite wydatki
  - `wyd_os_lek` – wydatki na opiekę zdrowotną na osobę

- **Kategoryczne:**
  - `klasa_miejsca` – wielkość miejscowości
  - `syt_mat` – sytuacja materialna
  - `glowne_zrod_utrzym` – główne źródło utrzymania
  - `moz_oszcz` – możliwości oszczędzania

## Metodologia

Projekt dzieli się na osiem sekcji:

1. **Instalacja zależności**  
   Instalacja wszystkich bibliotek przy pomocy pliku `requirements.txt`.

2. **Import bibliotek**  
   Importujemy pakiety niezbędne do operacji na danych (pandas, numpy), wizualizacji (matplotlib, seaborn), testów statystycznych (scipy.stats), modelowania (statsmodels, scikit-learn, stargazer, patsy) oraz dodatkowych narzędzi.

3. **Wczytanie i eksploracja danych**  
   Dane są wczytywane z pliku Excel ("Model_Lekarz.xlsx"), a następnie przeglądane metodami `.head()` i `.info()` w celu zapoznania się z ich strukturą.

4. **Czyszczenie danych i przekształcenia**

   - _Kodowanie zmiennych kategorycznych:_ Przypisujemy zmiennym takie etykiety, jak „miejscowosc”, „wyksztalcenie_1”, „mozliwosci_oszczedzania_1”, „zrodlo_utrzymania_1” oraz „sytuacja_materialna_1”.
   - _Filtrowanie obserwacji:_ Utrzymujemy tylko te obserwacje, w których `wyd_os_lek` > 0.

5. **Wizualizacje i raportowanie**

   - Tworzone są histogramy (dla wydatków oraz logarytmu wydatków), boxploty (dla „miejscowosc” i „wyksztalcenie_1”), wykresy rozrzutu (np. wydatki vs. wiek) oraz macierz korelacji.
   - Dokonywana jest wizualizacja wyników wyjściowych, co pozwala na identyfikację zależności między zmiennymi.

6. **Modelowanie statystyczne**

   - **Prosty model regresji:** Model, w którym jako predyktory użyto logarytmów dochodu (oraz kwadrat tej zmiennej) do wyjaśnienia zmiennej `wyd_os_lek`. Wyniki pokazały bardzo niski współczynnik determinacji (R² ≈ 0.081), co sugeruje, że te zmienne tłumaczą zaledwie 8% zmienności wydatków.
   - **Pełny model regresji:** W pełnym modelu zmienną zależną jest `log_wydatki` i uwzględnione są dodatkowe zmienne (wiek, doch_os, dummies dla wykształcenia, miejsca zamieszkania, źródła utrzymania, itp.). Uzyskany R² wynosi około 0.447, co oznacza, że model wyjaśnia prawie 45% zmienności.
   - **Model wielomianowy:** Na wyselekcjonowanym zbiorze (po usunięciu obserwacji odstających) zbudowano model z predyktorami transformowanymi logarytmicznie oraz potęgowymi (kwadrat i sześcian liczby osób). Jego R² wynosi około 0.476.
   - **Diagnoza błędów:** Wykonano test reset, Breuscha-Pagan, test White’a oraz obliczono VIF. Wyniki wskazują na obecność heteroskedastyczności (rozwiązanie: użycie macierzy HC0) oraz problemy z multikolinearnością, szczególnie dla zmiennej `liczba_osob` i jej potęg.
   - **Testy normalności:** Przeprowadzone testy Andersona-Darlinga i D'Agostino-Pearsona wskazują, że rozkład reszt nie jest idealnie normalny (D'Agostino-Pearsona: p-value ≈ 0, co przy dużej próbie, mimo centralnego twierdzenia granicznego, wymaga ostrożności).

7. **Wizualizacje wyników modelowania**

   - Tworzone są wykresy diagnostyczne (influence plot, wykresy reszt) oraz wykresy QQ, co umożliwia ocenę zgodności rozkładu reszt z normalnym.

8. **Wnioski i rekomendacje**  
   **Wnioski:**

   - Prosty model z logarytmicznym dochodem tłumaczy niewielką część zmienności wydatków (R² ≈ 0.081).
   - Pełny model regresji z uwzględnieniem zmiennych demograficznych i ekonomicznych ma R² na poziomie około 44–45%.
   - Model wielomianowy (na zbiorze bez obserwacji odstających) poprawia dopasowanie (R² ≈ 47.6%), jednak występują problemy z multikolinearnością (bardzo wysokie VIF dla zmiennych liczba_osob i jej potęg).
   - Testy normalności reszt (szczególnie D'Agostino-Pearsona) wskazują, że rozkład reszt odbiega od normalnego, choć przy dużej próbie efekty te mogą być mniej istotne.
   - Testy heteroskedastyczności (BP i White) potwierdzają, że wariancja reszt nie jest stała. Zastosowanie macierzy HC0 w modelach odpornych na heteroskedastyczność jest zasadne.

   **Rekomendacje i dalsze kroki:**

   - **Weryfikacja multikolinearności:** Ze względu na wysokie wartości VIF dla zmiennych liczba_osob oraz jej potęg, warto rozważyć centrowanie tej zmiennej przed tworzeniem jej potęg lub zastosowanie metod redukcji wymiarowości (np. PCA) lub regularyzacji (np. regresja Lasso).
   - **Dalsza diagnostyka reszt:** Mimo że CTG może zminimalizować skutki nieznormalności, warto przeprowadzić bootstrap lub analizę kwantylową, aby sprawdzić stabilność estymatorów.
   - **Rozszerzenie modelu:** Można rozważyć włączenie dodatkowych zmiennych (np. interakcje między zmiennymi) lub zastosowanie nieliniowych modeli (np. modele GAM), by lepiej uchwycić relacje między zmiennymi.
   - **Walidacja modelu:** Zaleca się przeprowadzenie walidacji krzyżowej, aby ocenić stabilność i przewidywalność modelu oraz ewentualne dostrojenie parametrów.
   - **Analiza wpływu obserwacji odstających:** Choć usunięcie kilku obserwacji poprawiło dopasowanie modelu, warto dokładniej zbadać te przypadki, aby określić, czy są one błędami pomiarowymi, czy reprezentują ważną część zjawiska.

## Instalacja i Uruchomienie

1. Sklonuj repozytorium.
2. Zainstaluj wymagane biblioteki:

   ```bash
   pip install -r requirements.txt
   ```

3. Otwórz notebook `Model_lekarz_Licencjat.ipynb` w Jupyter Notebook.
4. Uruchom wszystkie komórki w kolejności.

## Wyniki

Projekt wykazał, że czynniki takie jak wiek, dochód na osobę, poziom wykształcenia, wielkość miejscowości oraz źródło utrzymania wywierają istotny wpływ na wydatki na opiekę zdrowotną. Modele regresji i dalsza diagnostyka potwierdzają, że pełny model wyjaśnia około 44–47% zmienności wydatków. Problemy z heteroskedastycznością i multikolinearnością sugerują jednak konieczność dalszej analizy i ewentualnych zmian w specyfikacji modelu.

## Autor

Katarzyna Olbryś

## Licencja

[MIT License](./LICENSE)
