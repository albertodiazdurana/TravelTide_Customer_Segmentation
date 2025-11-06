# TravelTide – Methodik-Erklärungen
**Für Präsentation & technische Fragen**

---

## 1. WIE ENTSTEHEN DIE CLUSTER?

### 🎯 Business-freundliche Erklärung (für Elena & Marketing)

**Kurz:** "Wir gruppieren Kunden mit ähnlichem Verhalten zusammen."

**Detailliert:**
"Stellen Sie sich vor, Sie haben 5.765 Kunden und für jeden Kunden 50 Merkmale – wie oft sie buchen, wie viel sie ausgeben, welche Hotels sie bevorzugen, wie preissensitiv sie sind. Das sind wie 50 Eigenschaften pro Person. Jetzt wollen wir Kunden finden, die sich **ähnlich verhalten**.

Das ist wie wenn Sie in einem Raum mit 5.765 Menschen stehen und sagen: 'Findet Gruppen von Leuten, die ähnliche Interessen haben.' Einige werden sich natürlich zu **Premium-Reisenden** gruppieren, andere zu **Budget-Orientierten**, und wieder andere zu **Erlebnis-Suchenden**.

**Unser Algorithmus macht genau das – automatisch:**
1. Er misst, wie ähnlich sich zwei Kunden sind (basierend auf den 50 Merkmalen)
2. Er beginnt mit 5.765 einzelnen Kunden und fusioniert schrittweise die **ähnlichsten** zu Gruppen
3. Am Ende haben wir 3 große Gruppen gefunden: Paula, David, Fiona

**Warum 3 Gruppen?** Weil bei K=4 oder K=5 die Gruppen nicht mehr unterschiedlich genug waren – die Kunden innerhalb würden sich zu ähnlich sein. Bei K=3 haben wir die **optimale Balance** zwischen 'genug Unterschiede zwischen Gruppen' und 'genug Gemeinsamkeiten innerhalb der Gruppen'."

---

### 🔧 Technische Erklärung (für Tech-Team)

**Algorithmus:** Hierarchical Clustering mit Ward-Linkage

**Prozess:**
1. **Input:** 50 skalierte Features pro User (StandardScaler)
   - 45 Basis-Features (Engagement, Buchungen, Finanzen, Discount-Verhalten)
   - **5 Perk-Propensity Scores mit 4x Gewichtung** (wichtigste Prädiktoren)

2. **Hierarchical Clustering:**
   - **Linkage-Methode:** Ward (minimiert Varianz innerhalb der Cluster)
   - **Distanzmetrik:** Euclidean (nach Normalisierung)
   - **Bottom-Up-Approach:** Startet mit N=5.765 einzelnen Punkten, fusioniert schrittweise

3. **K-Selection:**
   - Getestet: K=2 bis K=10
   - **Optimal bei K=3:**
     - Silhouette Score: 0.378 (gut - Threshold >0.25)
     - Davies-Bouldin Index: 0.888 (exzellent - je niedriger, desto besser)
     - Calinski-Harabasz: 1625.56 (hoch = gut definierte Cluster)
   - K=4, K=5 zeigten schlechtere Metriken und kleinere, weniger stabile Cluster

4. **Output:** 3 Cluster-Labels (0, 1, 2) pro User

**Warum Hierarchical statt K-Means?**
- K-Means: Silhouette ~0.32
- Hierarchical (Ward): Silhouette ~0.38 (18% besser)
- Hierarchical ist deterministischer bei unserem Datenset

**Code-Referenz:**
```python
from scipy.cluster.hierarchy import linkage, fcluster
linkage_matrix = linkage(X_scaled, method='ward', metric='euclidean')
cluster_labels = fcluster(linkage_matrix, t=3, criterion='maxclust')
```

---

## 2. WIE ENTSTEHEN DIE PERK-ZUWEISUNGEN?

### 🎯 Business-freundliche Erklärung (für Elena & Marketing)

**Kurz:** "Jeder Kunde bekommt den Perk, für den er das stärkste Interesse zeigt."

**Detailliert:**
"Die Cluster zeigen uns **Gruppen ähnlicher Kunden**, aber innerhalb jeder Gruppe haben einzelne Kunden trotzdem unterschiedliche Vorlieben. Stellen Sie sich vor: Paula-Kunden lieben generell Hotels, aber manche bevorzugen die kostenlose Nacht, andere das Frühstück, wieder andere einfach einen Rabatt.

**Deshalb:** Wir weisen Perks **individuell** zu, nicht cluster-basiert.

**So funktioniert es:**

1. **Perk-Propensity Scores:**
   Für jeden Kunden haben wir in Woche 2 berechnet, wie stark er zu jedem der 5 Perks 'passt'. Das ist ein Score zwischen 0 und 1.
   
   **Beispiel Customer 12345:**
   - Free Bag: 0.23 (niedrig)
   - Hotel Meal: 0.67 (mittel)
   - Hotel Night: **0.89** (sehr hoch) ← **GEWINNER**
   - Exclusive Discount: 0.45 (mittel)
   - No Cancel Fee: 0.12 (sehr niedrig)

   → **Dieser Kunde bekommt 'Hotel Night'** weil 0.89 der höchste Score ist.

2. **Confidence-Level:**
   Wir berechnen auch, **wie sicher** wir sind:
   - **HIGH Confidence:** Score ≥0.7 UND großer Abstand zum zweitbesten Perk (Gap ≥0.2)
     - Beispiel: Top-Score 0.89, Zweiter 0.67 → Gap = 0.22 → **HIGH**
   - **MEDIUM Confidence:** Score ≥0.5 ODER Gap ≥0.1
   - **LOW Confidence:** Alles andere (kein klarer Favorit)

3. **Ergebnis:**
   - Jeder der 5.765 Kunden bekommt **genau einen Perk**
   - 63,5% mit HIGH Confidence (sehr zuverlässig)
   - 33,8% mit MEDIUM Confidence (gut)
   - 2,8% mit LOW Confidence (A/B-Test nötig)

**Warum nicht einfach Cluster = Perk?**
Weil dann **alle 4.596 Paula-Kunden denselben Perk** bekommen würden. Aber unsere Daten zeigen: Paula-Kunden sind divers. 28% wollen Hotel Night, 26% wollen Meal, 24% wollen Bag. **Personalisierung schlägt Cluster-Pauschale.**"

---

### 🔧 Technische Erklärung (für Tech-Team)

**Algorithmus:** Propensity-basierte Max-Score-Zuweisung mit Confidence-Scoring

**Prozess:**

1. **Input:** 5 Perk-Propensity Scores pro User (aus Notebook 04)
   - `propensity_free_bag`
   - `propensity_no_cancel_fee`
   - `propensity_hotel_meal`
   - `propensity_free_hotel_night`
   - `propensity_exclusive_discount`
   
   Diese wurden berechnet als **gewichtete Summe relevanter Features:**
   ```python
   # Beispiel: Free Bag Propensity
   propensity_free_bag = (
       0.30 * norm(avg_bags_per_trip) +
       0.20 * norm(flight_only_rate) +
       0.30 * norm(bag_traveler_score) +
       0.20 * norm(total_flight_spend)
   )
   ```
   → Alle Komponenten MinMax-skaliert auf [0,1], dann gewichtet

2. **Perk-Assignment:**
   ```python
   # 1. Finde Top-2-Perks pro User
   perk_cols = ['propensity_free_bag', 'propensity_no_cancel_fee', 
                'propensity_hotel_meal', 'propensity_free_hotel_night',
                'propensity_exclusive_discount']
   
   primary_perk = user_features[perk_cols].idxmax(axis=1)  # Höchster Score
   primary_score = user_features[perk_cols].max(axis=1)     # Wert des höchsten
   
   # 2. Berechne Gap (Präferenzstärke)
   sorted_scores = user_features[perk_cols].apply(lambda x: sorted(x, reverse=True), axis=1)
   perk_gap = sorted_scores.apply(lambda x: x[0] - x[1])  # Abstand Top-1 zu Top-2
   
   # 3. Confidence-Level
   confidence = np.where(
       (primary_score >= 0.7) & (perk_gap >= 0.2), 'HIGH',
       np.where(
           (primary_score >= 0.5) | (perk_gap >= 0.1), 'MEDIUM',
           'LOW'
       )
   )
   ```

3. **Output:**
   - `primary_perk`: String (z.B. 'propensity_free_bag')
   - `primary_score`: Float [0,1]
   - `secondary_perk`: String (zweitbester)
   - `perk_gap`: Float [0,1] (Präferenzstärke)
   - `confidence`: Categorical ('HIGH', 'MEDIUM', 'LOW')

4. **Validierung:**
   - **Mutual Exclusivity:** Jeder User hat genau 1 primary_perk
   - **Coverage:** 100% (alle 5.765 User zugewiesen)
   - **Balance-Check:** Kein Perk <10% oder >30% der User

**Confidence-Schwellenwerte Begründung:**
- **HIGH (≥0.7 & Gap ≥0.2):** Statistisch signifikante Präferenz
- **MEDIUM (≥0.5 | Gap ≥0.1):** Klare Tendenz, aber moderater
- **LOW:** Keine starke Präferenz → A/B-Test empfohlen

**Alternative betrachtet:**
- Cluster-basiert: Alle User in Cluster 0 → 1 Perk
  - Problem: Ignoriert intra-cluster Varianz (Paula hat 3 dominante Perks)
- Fuzzy Assignment: Top-2-Perks pro User
  - Problem: Kompliziert Kampagnen, schwer zu messen
- **Gewählt:** Propensity Max-Score (einfach, personalisiert, messbar)

---

## 3. TOP 5 FEATURES PRO CLUSTER

### Cluster 0: Premium Paula (79.7% | 4.596 User)

**Die 5 wichtigsten unterscheidenden Merkmale:**

1. **propensity_free_hotel_night** (Perk-Propensity Score)
   - Höchster Wert auf PC1 (0.5691) → Hauptmerkmal für Cluster-Trennung
   - 27.8% der Paula-Kunden erhalten Hotel Night als optimalen Perk
   - Zeigt starke Affinität für Premium-Hotel-Erlebnisse
   - Berechnet aus package_seeker_score, package_booking_rate, uses_both_channels

2. **propensity_free_bag** (Perk-Propensity Score) 
   - Hoher PC1-Wert (0.4126) → Zweitwichtigstes Cluster-Merkmal
   - 29.1% der Paula-Kunden erhalten Free Bag (häufigster Perk in diesem Cluster)
   - Korreliert mit avg_bags_per_trip und Familien-/Gruppenreisen
   - Zeigt diverse Reisemuster innerhalb des Segments

3. **estimated_annual_clv** (Customer Lifetime Value)
   - Durchschnitt: $4.985 (15.6x höher als Fiona)
   - Treibt 98% des gesamten Kundenwerts ($22.9M von $23.4M)
   - PC1-Wert: 0.1078 → Korreliert mit Hotel-Fokus
   - Definition: Geschätzter jährlicher Kundenwert aus historischem Verhalten

4. **total_hotels_booked** (Anzahl Hotel-Buchungen)
   - PC1-Wert: 0.1405 → Indikator für Hotel-Präferenz  
   - Höchste Hotel-Buchungsfrequenz aller Cluster
   - Zeigt Loyalität und wiederkehrende Hotel-Nutzung
   - Basis für hotel_booking_rate Berechnung

5. **package_booking_rate** (Paket-Buchungsrate)
   - PC1-Wert: 0.1391 → Zeigt Präferenz für Flug+Hotel-Pakete
   - Berechnung: total_package_bookings / total_all_bookings  
   - Paula bevorzugt Komplettlösungen über separate Buchungen
   - Korreliert stark mit propensity_free_hotel_night

**Charakterisierung:** Premium-Reisende mit sehr hohem Wert, häufigen Hotel-Buchungen, und diverser Perk-Präferenz. Dominantes Segment (79.7%) mit 72.5% HIGH-Confidence-Zuweisungen.

---

### Cluster 1: Dining David (5.0% | 287 User)

**Die 5 wichtigsten unterscheidenden Merkmale:**

1. **propensity_hotel_meal** (Perk-Propensity Score) 
   - **Dominierendes Merkmal:** Score 1.64 (höchster Wert aller User/Cluster)
   - 86.8% der David-Kunden erhalten Hotel Meal (stärkste Cluster-Perk-Korrelation)
   - Hoher Wert auf PC1 (0.4728) und PC2 (0.3025)
   - Zeigt klare erlebnisorientierte Reisephilosophie

2. **hotel_enthusiast_score** (Hotel-Enthusiasmus-Score)
   - PC2-Wert: 0.0893 → Experiential Traveler
   - Zusammengesetzter Score aus hotel_booking_rate, avg_nights_per_stay
   - Wert 0-1, gewichtete Kombination normalisierter Hotel-Metriken
   - Hotels als Erlebnis-Zentrum, nicht nur Übernachtung

3. **estimated_annual_clv** (Customer Lifetime Value)  
   - Durchschnitt: $768 (Mittelfeld zwischen Paula und Fiona)
   - Zeigt moderates, aber stabiles Ausgabeverhalten
   - Höher als Volumen-Segment, niedriger als Premium
   - Wachstumspotenzial durch Frequenz-Steigerung

4. **avg_nights_per_stay** (Durchschnittliche Aufenthaltsdauer)
   - PC1-Wert: 0.0742 → Moderate bis längere Aufenthalte
   - Ausreichend Zeit für kulinarische Exploration  
   - Berechnung: total_nights_stayed / total_hotels_booked
   - Korreliert mit Erlebnis-Fokus (nicht Business-Reisen)

5. **hotel_booking_rate** (Hotel-Buchungsrate pro Session)
   - Zeigt Hotel-Fokus ähnlich wie Paula, aber mit anderem Motiv
   - Berechnung: total_hotels_booked / total_sessions
   - Hotel als Ausgangspunkt für Dining-Erlebnisse
   - Nicht rein transaktional wie bei Paula

**Charakterisierung:** Erlebnisorientierte Mid-Tier-Reisende mit klarem Dining-Fokus. Kleinstes, aber am stärksten homogenes Segment mit 84.7% HIGH-Confidence-Zuweisungen.

---

### Cluster 2: Flexible Fiona (15.3% | 882 User)

**Die 5 wichtigsten unterscheidenden Merkmale:**

1. **propensity_no_cancel_fee** (Perk-Propensity Score)
   - **Dominierendes Merkmal:** 87.4% erhalten No Cancel Fee
   - Stärkste Cluster-Perk-Korrelation nach David/Meal
   - PC1/PC2-Wert: ~0 (orthogonal zu Hotel/Discount-Achsen)
   - Basiert primär auf cancellation_rate und cancellation_frequency

2. **cancellation_rate** (Stornierungsrate)
   - Berechnung: total_cancellations / total_all_bookings  
   - Höchste Rate aller Cluster → Flexibilitätsbedürfnis
   - PC1/PC2-Wert: ~0 (eigene Dimension)
   - Haupttreiber für No Cancel Fee Präferenz

3. **price_sensitivity_index** (Preissensitivitäts-Index)
   - PC2-Wert: 0.1977 → Discount Seeker
   - Zusammengesetzter Score aus Discount-Verhalten und Ausgaben-Verhältnis
   - Gewichtete Kombination von avg_spend_per_booking, discount_usage_rate
   - Höhere Werte = preisbewusster, elastischere Nachfrage

4. **discount_dependency_score** (Rabatt-Abhängigkeit)
   - PC2-Wert: 0.1788 → Zeigt Discount-Sensitivität
   - Berechnung: sessions_with_discount / total_sessions
   - Rabatte beeinflussen Kaufentscheidung stärker als bei Paula/David
   - Korreliert mit niedrigerem CLV

5. **estimated_annual_clv** (Customer Lifetime Value)
   - Durchschnitt: $319 (niedrigster Wert, aber stabil)
   - 15.3% der Kunden generieren <2% des Gesamt-CLV ($281K von $23.4M)
   - Volumen-Segment mit Konversionspotenzial
   - Zeigt Wachstumsmöglichkeit bei richtiger Ansprache

**Charakterisierung:** Budget-bewusste Gelegenheitsreisende mit Flexibilitätsbedürfnis. 90.4% MEDIUM-Confidence (stabiles Segment mit klaren, aber weniger extremen Präferenzen).

---

## 4. PERK PROPENSITY SCORE GLEICHUNGEN

Alle Perk-Propensity Scores werden als **gewichtete Summe relevanter Features** berechnet, wobei alle Komponenten zunächst mit MinMax-Normalisierung auf [0,1] skaliert werden.

**Normalisierungsfunktion:**
```python
def normalize_0_1(series):
    return (series - series.min()) / (series.max() - series.min())
```

---

### PERK 1: Free Checked Bag (Freigepäck)

**Formel:**
```
propensity_free_bag = 
    0.70 × normalize(avg_bags_per_trip) +
    0.30 × bag_traveler_score
```

**Komponenten-Definition:**
```python
avg_bags_per_trip = total_bags_checked / total_flights_booked
bag_traveler_score = normalize(avg_bags_per_trip)
```

**Logik:** 
- 70% Gewicht auf tatsächliches Gepäckverhalten (avg_bags_per_trip)
- 30% Gewicht auf normalisiertem Traveler-Score
- Hoher Score = Kunde bucht regelmäßig Gepäck → profitiert stark von Freigepäck

**Beispiel:**  
Customer mit 2.5 Bags/Flug → Score ≈ 0.85 → HIGH Propensity für Free Bag

---

### PERK 2: No Cancellation Fee (Keine Stornierungsgebühr)

**Formel:**
```
propensity_no_cancel_fee = 
    0.40 × normalize(cancellation_rate) +
    0.40 × normalize(cancellation_frequency) +
    0.20 × has_cancelled
```

**Komponenten-Definition:**
```python
cancellation_rate = total_cancellations / total_all_bookings
cancellation_frequency = total_cancellations / total_sessions  
has_cancelled = 1 if total_cancellations > 0 else 0
```

**Logik:**
- 40% Gewicht auf Stornierungsrate (Anteil stornierter Buchungen)
- 40% Gewicht auf Stornierungsfrequenz (Häufigkeit pro Session)
- 20% Gewicht auf binäres Flag (hat überhaupt schon storniert)
- Hoher Score = Kunde storniert oft → braucht Flexibilität

**Beispiel:**  
Customer mit 3 Stornierungen bei 10 Buchungen (30% Rate) → Score ≈ 0.72 → HIGH Propensity

---

### PERK 3: Free Hotel Meal (Kostenloses Hotelfrühstück/-essen)

**Formel:**
```
propensity_hotel_meal = 
    0.50 × hotel_enthusiast_score +
    0.30 × normalize(hotel_booking_rate) +
    0.20 × normalize(avg_nights_per_stay)
```

**Komponenten-Definition:**
```python
hotel_booking_rate = total_hotels_booked / total_sessions
avg_nights_per_stay = total_nights_stayed / total_hotels_booked

# hotel_enthusiast_score ist selbst zusammengesetzt:
hotel_enthusiast_score = normalize(hotel_booking_rate)
```

**Logik:**
- 50% Gewicht auf Hotel-Enthusiasmus (Präferenz für Hotels)
- 30% Gewicht auf Hotel-Buchungsrate (Frequenz)
- 20% Gewicht auf Aufenthaltsdauer (längere Stays = mehr Meals)
- Hoher Score = Hotel-fokussierter Reisender → Meals sind wertvoll

**Beispiel:**  
Customer mit 80% Hotel-Buchungsrate, 3 Nächte/Stay → Score ≈ 0.68 → HIGH Propensity

---

### PERK 4: Free Hotel Night with Flight (Gratis-Hotelnacht bei Flugbuchung)

**Formel:**
```
propensity_free_hotel_night = 
    0.50 × package_seeker_score +
    0.30 × normalize(package_booking_rate) +
    0.20 × uses_both_channels
```

**Komponenten-Definition:**
```python
package_booking_rate = total_package_bookings / total_all_bookings
uses_both_channels = 1 if (total_flights_booked > 0 AND total_hotels_booked > 0) else 0

# package_seeker_score ist normalisiert:
package_seeker_score = normalize(package_booking_rate)
```

**Logik:**
- 50% Gewicht auf Paket-Affinität (bevorzugt Komplettlösungen)
- 30% Gewicht auf tatsächliche Paket-Buchungsrate  
- 20% Gewicht auf Nutzung beider Kanäle (Flug + Hotel)
- Hoher Score = Paket-Reisender → Free Night ist perfekter Anreiz

**Beispiel:**  
Customer mit 70% Package-Rate, nutzt beide Kanäle → Score ≈ 0.75 → HIGH Propensity

---

### PERK 5: Exclusive Discounts (Exklusive Rabatte)

**Formel:**
```
propensity_exclusive_discount = 
    0.40 × discount_hunter_score +
    0.30 × normalize(discount_usage_rate) +
    0.30 × normalize(price_sensitivity_index)
```

**Komponenten-Definition:**
```python
discount_usage_rate = sessions_with_discount / total_sessions
price_sensitivity_index = (normalize(discount_dependency_score) + 
                            normalize(1 / avg_spend_per_booking)) / 2

# discount_hunter_score ist zusammengesetzt:
discount_dependency_score = sessions_with_discount / total_sessions
discount_hunter_score = (normalize(discount_dependency_score) + 
                         normalize(price_sensitivity_index)) / 2
```

**Logik:**
- 40% Gewicht auf Discount-Hunter-Score (kombiniert Dependency + Sensitivity)
- 30% Gewicht auf tatsächliche Discount-Nutzungsrate
- 30% Gewicht auf Preissensitivitäts-Index
- Hoher Score = Preisbewusster Kunde → Discounts beeinflussen Kaufentscheidung

**Beispiel:**  
Customer mit 60% Discount-Usage, niedriger Avg Spend → Score ≈ 0.82 → HIGH Propensity

---

## 5. INTERPRETATION DER PROPENSITY SCORES

### Score-Bereiche und Bedeutung

**Score 0.0 - 0.3 (NIEDRIG):**
- Kunde zeigt kaum Verhalten, das auf diesen Perk hindeutet
- Perk würde wenig Mehrwert bieten
- Andere Perks sind deutlich relevanter

**Score 0.3 - 0.5 (MITTEL):**
- Moderates Interesse oder gelegentliches Verhalten
- Perk könnte nützlich sein, aber nicht primär
- Typischerweise Secondary Perk Kandidat

**Score 0.5 - 0.7 (HOCH):**
- Klares, konsistentes Verhalten zeigt Perk-Relevanz
- Perk bietet echten Mehrwert für Kunden
- Gute Kandidaten für Primary Perk Assignment

**Score 0.7 - 1.0 (SEHR HOCH):**
- Starke, eindeutige Präferenz
- Perk ist perfekt auf Kundenverhalten abgestimmt
- Typischerweise HIGH Confidence Assignments

### Confidence-Level Berechnung

Nach Berechnung aller 5 Propensity Scores pro User wird Confidence bestimmt:

```python
primary_score = max(alle 5 scores)
perk_gap = primary_score - second_highest_score

if primary_score >= 0.7 AND perk_gap >= 0.2:
    confidence = 'HIGH'      # 63.5% der User
elif primary_score >= 0.5 OR perk_gap >= 0.1:
    confidence = 'MEDIUM'    # 33.8% der User
else:
    confidence = 'LOW'       # 2.8% der User (A/B-Test empfohlen)
```

**Beispiel:**
```
Customer 12345:
  propensity_free_bag: 0.23
  propensity_no_cancel_fee: 0.12
  propensity_hotel_meal: 0.67
  propensity_free_hotel_night: 0.89  ← PRIMARY (höchster)
  propensity_exclusive_discount: 0.45

→ Primary Score: 0.89
→ Gap: 0.89 - 0.67 = 0.22
→ Confidence: HIGH (score ≥0.7 AND gap ≥0.2)
→ Assignment: Free Hotel Night
```

---

## VERGLEICH: CLUSTER vs. PERK-ASSIGNMENT

| Aspekt | Clustering | Perk-Assignment |
|--------|-----------|-----------------|
| **Ziel** | Gruppen ähnlicher Kunden finden | Jeden Kunden individuell zuweisen |
| **Basis** | 50 Features (Verhalten, Demografie, Finanzen) | 5 Perk-Propensity Scores |
| **Output** | 3 Cluster-Labels (0, 1, 2) | 5 Perk-Labels (Bag, Meal, Night, Discount, Cancel) |
| **Logik** | Ähnlichkeit zwischen Kunden | Höchster Score pro Kunde |
| **Ergebnis** | 3 Segmente (Paula 80%, David 5%, Fiona 15%) | 5 Perks (Bag 24%, Meal 23%, Night 22%, Discount 16%, Cancel 14%) |
| **Warum?** | Verstehen, wer unsere Kunden sind | Entscheiden, was jeder Kunde bekommt |

**Schlüssel-Erkenntnis:**
- **Cluster ≠ Perks**
- Cluster = "Wer bist du?" (Verhaltensgruppe)
- Perk = "Was willst du?" (Individuelle Präferenz)

**Beispiel:**
- Customer A & B sind beide in Cluster 0 (Paula) → ähnliches Gesamtverhalten
- Aber: Customer A bekommt "Hotel Night" (Score 0.89)
- Und: Customer B bekommt "Free Bag" (Score 0.76)
- Warum? Weil trotz ähnlichem Profil ihre **spezifischen Präferenzen** unterschiedlich sind

---

## HÄUFIGE FRAGEN & ANTWORTEN

### "Warum nicht K=5 Cluster für 5 Perks?"

**Kurz:** Cluster basieren auf Verhalten, nicht auf Perks. Das Verhalten zeigt nur 3 natürliche Gruppen.

**Ausführlich:** 
"K=5 würde bedeuten, wir zwingen die Daten in 5 Gruppen. Das würde **künstliche Segmente** schaffen. Die Daten zeigen natürlich nur 3 klare Verhaltensgruppen. Aber innerhalb dieser 3 Gruppen gibt es **diverse Perk-Präferenzen**. Deshalb: 3 Cluster für Verständnis, 5 Perks für Zuweisung."

---

### "Warum ist Paula 80% aber Hotel Night nur 22%?"

**Kurz:** Weil Paula-Kunden verschiedene Perks wollen.

**Ausführlich:**
"Paula (Cluster 0) hat 4.596 Kunden. Aber diese haben unterschiedliche Prioritäten:
- 28% wollen Hotel Night
- 26% wollen Hotel Meal
- 24% wollen Free Bag
- Rest: Discounts und No Cancel

Das zeigt: **Cluster-Zugehörigkeit ≠ Perk-Präferenz**. Paula-Kunden sind sich in ihrem Gesamtverhalten ähnlich (frequent, high-value, hotel-focused), aber ihre spezifischen Wünsche variieren."

---

### "Wie genau sind die Propensity Scores?"

**Kurz:** 97% der Zuweisungen haben hohe oder mittlere Confidence.

**Ausführlich:**
"Propensity Scores basieren auf historischem Verhalten:
- Wer viele Bags gebucht hat → hoher Free Bag Score
- Wer oft storniert hat → hoher No Cancel Fee Score
- Wer lange Hotelaufenthalte hat → hoher Hotel Night Score

Diese Muster sind **stabil und messbar**. 63,5% der Kunden haben HIGH Confidence (sehr klare Präferenz), weitere 33,8% MEDIUM (gute Präferenz). Nur 2,8% haben LOW Confidence (unklar) → diese testen wir mit A/B."

---

### "Können Kunden zwischen Clustern wechseln?"

**Kurz:** Ja, wenn ihr Verhalten sich ändert.

**Ausführlich:**
"Cluster basieren auf aktuellem Verhalten. Wenn ein Fiona-Kunde (Budget, flexibel) plötzlich anfängt, häufiger und teurer zu buchen, wird er in der nächsten Quartals-Analyse zu Paula migrieren. Das Modell ist **dynamisch, nicht statisch**. Deshalb quartalsweise Re-Runs empfohlen."

---

### "Warum Hierarchical und nicht K-Means?"

**Technisch:** Hierarchical (Ward) hatte 18% besseren Silhouette Score (0.378 vs 0.32).

**Business:** Hierarchical ist **deterministischer** – gleiche Daten = gleiche Cluster. K-Means variiert je nach Random-Seed. Für Production wollen wir Stabilität.

---

## ZUSAMMENFASSUNG FÜR PRÄSENTATION

**Wenn gefragt: "Wie habt ihr das gemacht?"**

**Antwort (45 Sekunden):**
"Zwei Schritte. **Schritt 1 – Clustering:** Wir haben für jeden Kunden 50 Verhaltensmerkmale analysiert und Kunden mit ähnlichem Verhalten gruppiert. Das ergab 3 natürliche Segmente – Paula, David, Fiona – basierend auf Buchungsfrequenz, Wert und Präferenzen.

**Schritt 2 – Perk-Assignment:** Dann haben wir für jeden einzelnen Kunden berechnet, wie stark er zu jedem der 5 Perks passt – quasi eine Matching-Wahrscheinlichkeit. Jeder Kunde bekommt den Perk mit dem höchsten Score. Das gibt uns personalisierte Zuweisungen statt Cluster-Pauschalzuweisungen.

**Ergebnis:** 3 Cluster für Strategie, 5 Perks ausgeglichen verteilt, 97% sichere Zuweisungen."

---

**Vorbereitet von:** Alberto Diaz Durana  
**Datum:** November 2025  
**Verwendung:** TravelTide Präsentation & technische Q&A
