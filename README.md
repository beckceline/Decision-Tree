# Decision-Tree
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/beckceline/Decision-Tree/HEAD)

Für dieses Projekt werden wir öffentlich verfügbare Daten von LendingClub.com verwenden. Lending Club bringt Leute zusammen, die Geld brauchen (Leihende) und solche, die Geld investieren möchten (Geldgeber). Als Invester möchte man dann verständlicherweise vor allem an die Leute sein Geld verleihen, die es mit einer hohen Wahrscheinlichkeit zurückzahlen. Wir werden versuchen ein Modell zu erstellen, dass bei dieser Vorhersage hilft.

Wir werden Daten von 2007 bis 2010 verwenden, bevor das Unternehmen an die Börse ging. Anhand der Daten werden wir versuchen vorherzusagen, ob ein Leihender das Geld zurückgezahlt hat oder nicht. Die Daten stehen als CSV zur Verfügung und wurden bereits um die nicht verfügbaren Einträge gesäubert.

Der Datensatz beinhaltet folgende verfügbare Spalten:

* credit.policy: 1 falls der Kunde die Risikobewertung besteht, 0 falls nicht.
* purpose: Der Zweck des Kreidts (Werte sind "credit_card", "debt_consolidation", "educational", "major_purchase", "small_business", und "all_other").
* int.rate: Der Zinssatz des Kreidts als Anteil (eine Rate von 11% würde 0.11 sein). Kreditnehmer, die LendingClub.com als riskanter einstuft erhalten einen höheren Zins.
* installment: Die monatliche Zeilzahlung, die der Kreditnehmer leistet, wenn der Kredit finaziert wird.
* log.annual.inc: Der natürliche Log des angegebenen jährlichen Einkommens des Kreditnehmers.
* dti: Die "debt-to-income" Rate des Kreditnehmers (Kredit geteilt durch jährliches Einkommen.
* fico: Der FICO Kreditscore des Kreditnehmers.
* days.with.cr.line: Anzahl der Tage an denen der Kunde einen Dispokredit hatte.
* revol.bal: Die Bilanz am Ende eines Kreditkartenabrechnungszeitraums.
* revol.util: Der erstattete Anteil am Gesamtkredit.
* inq.last.6mths: Die Anzahl an Anfragen, die Kreditgeber in den letzten 6 Monaten an den Kreditnehmer gestellt haben.
* delinq.2yrs: Die Anzahl der Vorkommnisse eines Verzugs von über 30 Tagen innerhalb der letzten 2 Jahre.
* pub.rec: Die Anzahl an negativen Einträgen (Bankrott, Steuerverzug, Verurteilungen,...) des Kreditnehmers.


### Schritte

1. Daten laden und Überblick verschaffen: Zu Beginn des Projekts importieren wir verschiedene Python-Bibliotheken, darunter Pandas, NumPy, Matplotlib und Seaborn, um Daten zu analysieren, zu visualisieren und Modelle zu erstellen. Anschließend laden wir die CSV-Datei "loan_data.csv" mithilfe von Pandas in ein DataFrame namens "loans". Wir führen auch einige grundlegende Überprüfungen der Daten durch, um Informationen über die Datenstruktur und den Inhalt zu erhalten.

2. Datenvisualisierung: In diesem Schritt verwenden wir verschiedene Visualisierungstechniken, um ein besseres Verständnis der Daten zu entwickeln. Wir erstellen Histogramme, Countplots und Jointplots, um die Verteilung der FICO-Scores zu untersuchen und Zusammenhänge zwischen verschiedenen Merkmalen und der Rückzahlung von Krediten zu identifizieren.

3. Daten vorbereiten: Um die Daten für die Modellierung vorzubereiten, konzentrieren wir uns auf die Kategorisierung von Merkmalen. Insbesondere konvertieren wir die Spalte "purpose" in Dummy-Variablen. Dies ermöglicht es uns, kategoriale Daten in einer Form zu verwenden, die von maschinellen Lernalgorithmen verarbeitet werden kann. Der bereinigte DataFrame wird "final_data" genannt.

4. Train-Test-Split: Um die Leistung unserer Modelle zu bewerten, teilen wir die Daten in Trainings- und Testsets auf. Dieser Schritt ist entscheidend, um sicherzustellen, dass unsere Modelle in der Lage sind, unbekannte Daten effektiv vorherzusagen. Wir verwenden die train_test_split-Funktion aus dem sklearn-Modul, um diese Aufteilung durchzuführen.

5. Decision Tree-Modell: Zu Beginn erstellen und trainieren wir ein einfaches Decision Tree-Modell mit dem DecisionTreeClassifier aus dem sklearn.tree-Modul. Wir passen dieses Modell auf die Trainingsdaten an und verwenden es dann, um Vorhersagen für die Testdaten zu erstellen. Die Leistung des Modells wird anhand eines Classification Reports und einer Confusion Matrix bewertet.

6. Random Forest-Modell: Anschließend erstellen und trainieren wir ein Random Forest-Modell mit dem RandomForestClassifier aus dem sklearn.ensemble-Modul. Dieses Modell basiert auf einer Sammlung von Entscheidungsbäumen und bietet in der Regel bessere Vorhersageleistungen als einzelne Bäume. Wir trainieren das Modell mit den Trainingsdaten, erstellen Vorhersagen für die Testdaten und bewerten seine Leistung.

### Ergebnis

Abschließend vergleichen wir die Leistung der beiden Modelle, des Decision Trees und des Random Forests. Wir betrachten Genauigkeits-, F1-Score- und Recall-Werte für die positive Klasse (Kreditnehmer, die ihre Schulden nicht vollständig zurückzahlen). 

- Entscheidungsbaummodell:

| Recall für die Klasse "1" (not.fully.paid) | Genauigkeit (accuracy) |
|----------|----------|
| 0.24 | 0.73 |

- Random Forest-Modell:

| Recall für die Klasse "1" (not.fully.paid) | Genauigkeit (accuracy) |
|----------|----------|
| 0.02 | 0.85 |

Die genauen Zahlen zeigen, dass das Random Forest-Modell eine niedrigere Wiederfindungsrate (Recall) für die Klasse "1" aufweist, was bedeutet, dass es weniger effektiv bei der Identifizierung von nicht vollständig zahlenden Kreditnehmern ist als das Entscheidungsbaummodell. Dennoch ist die Genauigkeit des Random Forest-Modells insgesamt höher, was darauf hindeutet, dass es besser in der Lage ist, insgesamt korrekte Vorhersagen zu treffen. Dies zeigt, dass die Wahl zwischen den Modellen von den Prioritäten und Anforderungen des Anwendungsfalls abhängt.

Dennoch ist zu beachten, dass keines der Modelle besonders gut darin ist, Kreditnehmer vorherzusagen, die ihre Schulden nicht vollständig zurückzahlen. Dies könnte darauf hinweisen, dass weitere Anpassungen an den Merkmalen oder Modellverbesserungen erforderlich sind.
