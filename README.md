# Automated Valuation Model (AVM) – Warsaw Real Estate Prediction
### Zaawansowany silnik predykcyjny wspierający zarządzanie ryzykiem kredytowym

---

## 📌 O projekcie
Niniejszy projekt prezentuje budowę i walidację modelu **Automated Valuation Model (AVM)** dla rynku wtórnego nieruchomości w Warszawie. Narzędzie zostało zaprojektowane jako wsparcie procesów masowej wyceny zabezpieczeń oraz monitorowania portfela kredytowego w reżimie nowoczesnych instytucji finansowych.

## 🎯 Kontekst Strategiczny (Risk Management)
Głównym celem analitycznym jest dostarczenie precyzyjnych estymat wartości rynkowej (Fair Value), które stanowią fundament dla:
* **Szacowania LGD (Loss Given Default):** Precyzyjna wycena zabezpieczenia bezpośrednio wpływa na poziom odzysków w przypadku niewypłacalności klienta.
* **Zgodności z IFRS 9:** Optymalizacja procesów wyliczania **ECL (Expected Credit Loss)** poprzez dostarczanie wiarygodnych danych o wartości portfela zabezpieczeń.
* **Zarządzania Kapitałem:** Monitorowanie adekwatności kapitałowej poprzez bieżącą aktualizację wycen masowych.

## 🛠️ Architektura Analityczna i Model Governance

### Silnik Predykcyjny
Sercem systemu jest algorytm **XGBoost (Extreme Gradient Boosting)**, wybrany ze względu na jego zdolność do mapowania nieliniowych zależności geograficznych oraz wysoką odporność na multikoliniowość cech fizycznych nieruchomości.

### Pipeline Przetwarzania Danych (Data Pipeline)
* **Ingestia Danych:** Zautomatyzowany proces agregacji snapshotów rynkowych (08.2023 – 06.2024), zapewniający spójność typów danych i eliminację błędów wczytywania.
* **Geospatial Feature Engineering:** Modelowanie oparte na precyzyjnych współrzędnych GPS (latitude/longitude), pozwalające na identyfikację nieliniowych "hot-spotów" cenowych.
* **Model Governance:** Rygorystyczna strategia walidacji ($80/20$) z zachowaniem pełnej replikowalności wyników (`random_state=42`) oraz eliminacja wycieku danych (**Data Leakage**).

### Framework Kontroli Jakości (Sanity Check)
Zastosowano zaawansowany moduł detekcji anomalii oparty na **rozstępie ćwiartkowym (IQR)**. Podejście to gwarantuje, że parametry modelu nie są estymowane na podstawie szumu rynkowego, co bezpośrednio przekłada się na stabilność operacyjną modelu.

## 📈 Wyniki i Metryki Jakości
Model uzyskał bardzo wysoką zdolność do generalizacji na danych testowych:
* **Współczynnik determinacji ($R^2$):** $0.9424$
* **MAE (Mean Absolute Error):** $\approx 66,000$ PLN
* **Analiza Rezyduów:** Zidentyfikowano segmenty o najwyższej wariancji (Premium), co pozwala na optymalne zaprojektowanie procesów biznesowych (kierowanie do rzeczoznawców).

## 🚀 Implementacja w Procesach Bankowych
1. **Dynamiczne Monitorowanie LTV:** Cykliczna aktualizacja wskaźnika *Loan-to-Value*:
   $$LTV_{current} = \frac{Saldo\ zadłużenia}{Wycena\ modelu\ AVM}$$
2. **Stress Testing:** Możliwość przeprowadzania natychmiastowych symulacji typu *What-if* (np. wpływ szoku rynkowego na poziom rezerw banku).
3. **Optymalizacja Kosztów:** AVM służy jako „pierwsze sito”, automatycznie procesując standardowe przypadki i uwalniając zasoby rzeczoznawców do wycen trudnych.

