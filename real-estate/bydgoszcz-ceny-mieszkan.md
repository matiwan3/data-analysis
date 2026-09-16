# Ceny mieszkań w Bydgoszczy (2006–2026) vs stopy procentowe NBP

## Cel badania

Sprawdzenie dwóch hipotez na 20-letnim horyzoncie danych:
1. Czy ceny mieszkań w Bydgoszczy rosły liniowo w czasie
2. Czy zmiany stóp procentowych NBP wpływały na dynamikę cen (z opóźnieniem)

## Źródła danych

- **Ceny mieszkań:** NBP, Baza Cen Nieruchomości Mieszkaniowych (BaRN), dane kwartalne 2006 Q3 – 2026 Q1
- **Stopy procentowe:** archiwum stopy referencyjnej NBP

## Wykres
<img width="1288" height="687" alt="image" src="https://github.com/user-attachments/assets/922243b7-35ba-4f36-a70f-a0800f048d57" />

## Metodologia

Dane zostały załadowane do PostgreSQL i przeanalizowane przy pomocy zapytań SQL liczących korelację Pearsona (`CORR()`), zarówno na surowych poziomach, jak i na zmianach kwartał-do-kwartału (żeby wyeliminować wspólny trend czasowy).

## Wyniki

| Test | Korelacja | Interpretacja |
|---|---|---|
| Poziomy, bez opóźnienia | 0,471 | Zaburzone wspólnym trendem |
| Zmiany, bez opóźnienia | 0,159 | Słaba |
| Poziomy, z opóźnieniem 4kw | 0,608 | Zaburzone wspólnym trendem |
| **Zmiany, z opóźnieniem 4kw** | **-0,214** | Najbardziej wiarygodny wynik |
| Trend liniowy cen (R²) | 0,770 | Silny, systematyczny wzrost |

## Wnioski

**Hipoteza 1 (ceny rosły liniowo):** potwierdzona. Sam upływ czasu tłumaczy 77% zmienności ceny — rynek charakteryzował się silnym, systematycznym trendem wzrostowym.

**Hipoteza 2 (stopy wpływały na dynamikę popytu):** odrzucona przy analizie na surowych poziomach danych (efekt wspólnego trendu), ale po usunięciu tego trendu widoczny jest słaby, zgodny z teorią ekonomiczną efekt: wzrost stóp procentowych z rocznym opóźnieniem koreluje ujemnie ze zmianą cen (-0,214).

Kluczowa lekcja metodologiczna: analiza korelacji na surowych poziomach dwóch rosnących w czasie zmiennych może prowadzić do mylących wniosków. Testowanie na zmianach (różnicach) zamiast poziomów jest bardziej wiarygodne przy podejrzeniu wspólnego trendu.

## Ograniczenia

- Dane o stopach procentowych za lata 2006-2020 to średnie roczne (nie precyzyjne wartości kwartalne)
- 20 lat danych to nadal stosunkowo mała próbka do wnioskowania o zależnościach makroekonomicznych
