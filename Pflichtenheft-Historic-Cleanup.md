# Pflichtenheft

## KI_PROJEKT_SOSSEN_SOURCING

---

## Abschnitt 1: Deckblatt

|  |  |
| :---- | :---- |
| **Projekt** | KI_PROJEKT_SOSSEN_SOURCING |
| **Auftraggeber** | AVO-Werke August Beisse GmbH |
| **Auftragnehmer** | Wilsch AI Services OÜ |

---

## Abschnitt 2: Zielbestimmung

### Muss (POC-Umfang)

**Suche nach Zutatennamen, Artikelnummern und prozentualen Zusammensetzungen**

- Identifikation von Duplikaten und ähnlichen Rezepten unter ca. 8000 bestehenden Rezepten
- Vergleich von Rezepten basierend auf Zutatenzusammensetzung und Mengenangaben
- Darstellung von Ähnlichkeitsrankings zur Ermöglichung manueller Harmonisierungsentscheidungen
- Reduzierung der Produktionskomplexität durch Konsolidierung redundanter Rezepte
- POC-Validierung beginnt mit einer Teilmenge von ca. 100 Rezepten

### Zurückgestellt (Nach POC)

**Historische Rezeptbereinigung - Erweiterte Filterfunktionen**

- Filterung von Rezepten nach speziellen Zutatenattributen (VLOG, TK, Bio, Halal, Koscher)

---

## Abschnitt 3: Funktionale Anforderungen

### Muss (POC-Umfang)

**Rezeptvergleich basierend auf Zutatenzusammensetzung und Mengenangaben**

- **FR-02:** Das System muss Zutaten über die Material_ID (Artikelnummer) zur eindeutigen Identifizierung abgleichen.
- **FR-02a:** Das System muss die Überschneidungsrate der Zutaten zwischen Rezeptpaaren berechnen.
- **FR-04:** Das System muss prozentuale Mengenangaben zwischen übereinstimmenden Zutatenpaaren vergleichen und Ähnlichkeitswerte berechnen.
- **FR-08:** Das System muss nicht übereinstimmende Zutaten identifizieren, die dieselbe Rohstoffkategorie teilen, um potenzielle Substitutionsübereinstimmungen zu ermöglichen.

**Darstellung von Ähnlichkeitsrankings zur Ermöglichung manueller Harmonisierungsentscheidungen**

- **FR-05:** Das System muss Ähnlichkeitsrankings (keine binären Ja/Nein-Angaben) ausgeben, die prozentuale Übereinstimmungswerte zwischen Rezeptpaaren anzeigen.
- **FR-06:** Das System muss Ergebnisse im Excel-Format mit Rezeptdetails und Übereinstimmungswerten exportieren.

**Validierung der POC-Funktionalität**

- **FR-11:** Das System muss die POC-Funktionalität mit einer Teilmenge von ca. 100 Rezepten validieren, bevor auf die vollständige Datenbank von ca. 8000 Rezepten skaliert wird.


### Zurückgestellt (Nach POC)

**Historische Rezeptbereinigung**

*Erweiterte Vergleichsfunktionen*

- **FR-03:** Das System muss hierarchische Rezeptstrukturen (Vormischungen) mit der Option unterstützen, auf derselben Ebene zu vergleichen oder auf Basiszutaten herunterzubrechen.

*Erweiterte Filter- und UI-Funktionen*

- **FR-07:** Das System muss Rezepte nach speziellen Zutatenattributen filtern können (z.B. VLOG, TK/Tiefkühl, Bio, Halal, Koscher).
- **FR-10:** Das System muss konfigurierbare Schwellenwertparameter für Ähnlichkeitsberechnungen verwenden.
- **FR-12:** Das System muss eine Chat-Oberfläche für interaktive Ähnlichkeitssuchanfragen bereitstellen.

*Visuelle Vergleichserweiterungen*

- **FR-23:** Das System muss vom Benutzer akzeptierte Zutatenaustausche für zukünftige Vergleichsvorschläge speichern.
- **FR-24:** Das System muss visuelle Hervorhebungen von prozentualen Unterschieden mit konfigurierbarer Farbcodierung und Schiebereglern bereitstellen.
- **FR-25:** Das System muss Ansichten auf Zutaten- und Rezeptebene mit spaltenweiser Anzeige prozentualer Unterschiede bereitstellen.

*Dateninfrastruktur*

- **FR-26:** Das System muss die Rezeptdatenbank direkt über JDBC für den Datenzugriff abfragen.
- **FR-27:** Das System muss die Metadatenstrukturdatei durch Stapelverarbeitung automatisch generieren und aktualisieren, um eine konsistente Datensynchronisation zu gewährleisten.

*Benutzeroberfläche*

- **FR-28:** Das System muss eine benutzerdefinierte Vergleichsansicht für die Integration mit OpenWebUI-Chat bereitstellen, die interaktive Steuerelemente und Dual-View-Layouts unterstützt (Desktop-optimiert).

---

## Abschnitt 4: Nicht-funktionale Anforderungen

**Hinweis:** Die finalen quantifizierten Metriken werden in Zusammenarbeit mit Thomas Erhard (Infrastrukturspezialist) definiert.

### Leistung

- **NFR-01 [TBD]:** Das System muss Vergleichsoperationen auf einer Datenbank von ca. 8000 Rezepten unterstützen.

  - *Zu quantifizieren: Antwortzeitschwellen, Durchsatzanforderungen*


- **NFR-02 [TBD]:** Der POC muss Ähnlichkeitsanalysen auf einer Teilmenge von ca. 100 Rezepten durchführen.

  - *Zu quantifizieren: Maximal akzeptable Verarbeitungszeit*

### Kompatibilität

- **NFR-03:** Das System muss mit dem IBM AS/400 Datenbanksystem integriert werden.

- **NFR-04:** Das System muss Ergebnisse in einem Excel-kompatiblen Format exportieren.

### Sicherheit

- **NFR-05 [TBD]:** Das System muss VPN-Tunnel-Zugriff für die POC-Bereitstellungsphase erfordern.
  - *Mit Thomas Erhard zu definieren: Verschlüsselungsstandards, Authentifizierungsanforderungen*

### Benutzerfreundlichkeit

- **TBD**


---

## Abschnitt 5: Abnahmekriterien

**Hinweis:** Abnahmekriterien für zurückgestellte Anforderungen werden während ihrer jeweiligen Implementierungsphasen definiert.

### FR-02: Material_ID Abgleich

- **Gegeben** zwei Rezepte mit gemeinsamen Material_IDs
- **Wenn** der Vergleich ausgeführt wird
- **Dann** identifiziert das System alle exakten Material_ID-Übereinstimmungen zwischen den Rezepten

### FR-02a: Berechnung der Überschneidungsrate

Hinweis: Dies kann sich während der Implementierung ändern

- **Gegeben** Rezept A (20 Zutaten) und Rezept B (10 Zutaten) mit 8 gemeinsamen Zutaten
- **Wenn** die Überschneidungsrate berechnet wird
- **Dann** gibt das System eine Überschneidungsrate von 0,40 zurück

### FR-04: Prozentuale Ähnlichkeit

- **Gegeben** eine übereinstimmende Zutat mit 5,2% in Rezept A und 5,8% in Rezept B
- **Wenn** die prozentuale Ähnlichkeit berechnet wird
- **Dann** berechnet das System einen Ähnlichkeitswert basierend auf der prozentualen Differenz

### FR-08: Rohstoffkategorie-Abgleich

- **Gegeben** nicht übereinstimmende Zutaten aus zwei Rezepten
- **Wenn** der Rohstoffkategorie-Vergleich ausgeführt wird
- **Dann** identifiziert und markiert das System Zutatenpaare, die dieselbe Rohstoffkategorie teilen

### FR-05: Ausgabe von Ähnlichkeitsrankings

- **Gegeben** ein Vergleich von Rezept A gegen alle Rezepte in der Datenbank
- **Wenn** die Ähnlichkeitssuche abgeschlossen ist
- **Dann** gibt das System eine Rangliste ähnlicher Rezepte mit prozentualen Übereinstimmungswerten aus

### FR-06: Excel-Export

- **Gegeben** abgeschlossene Ähnlichkeitsanalyseergebnisse
- **Wenn** ein Export angefordert wird
- **Dann** generiert das System eine Excel-Datei mit Rezeptpaaren, Übereinstimmungswerten und Zutatendetails

### FR-11: POC-Validierung

- **Gegeben** POC-Teilmenge von 100 Rezepten
- **Wenn** Validierungstests ausgeführt werden
- **Dann** führt das System alle Vergleichsoperationen erfolgreich ohne Fehler durch, bevor auf die vollständige Datenbank skaliert wird

---

## Abschnitt 6: Technische Rahmenbedingungen

### Bereitstellungsumgebung

**POC-Phase:**

- Hosting: WPH-Rechenzentrum auf IBM Power 10
- Datenformat: IBM Save-File (*SAVF) mit Metadatentabelle
- Testdatensatz: 100 Rezepte mit 5 bekannten Duplikatpaaren (bereitgestellt von AVO)
- Hosting-Kosten im Angebot enthalten

**Produktionsphase:**

- On-Premise-Bereitstellung auf AVOs IBM Power 10 Server
- Hardware: 8 CPU-Kerne, 512GB RAM
- Betriebssystem: IBM i
- AI-LPAR-Setup-Aufwand: 4-5 Personentage
- Keine zusätzliche Hardware erforderlich (aktuelle Einschätzung)

### Erforderliche Integrationen

**Datenbankintegration:**

- IBM AS/400 / IBM i System mit DB2-Datenbank
- Datenzugriff: Metadatendatei im IBM Save-File-Format (*SAVF)
- Metadatenstruktur: Denormalisierte Tabelle mit abgeflachter Rezepthierarchie
- Ca. 8000 Rezepte in der Produktionsdatenbank
- Stapelverarbeitung für Metadatendatei-Aktualisierungen (Zyklus mit AVO abzustimmen)

**Ausgabeintegration:**

- Excel-Exportformat (basierend auf AVO-Vorlage aus Workshop)
- Top 5 ähnliche Rezepte pro Anfrage
- Drei Kriterien separat pro Übereinstimmung angezeigt

**Kontext bestehender Systeme:**

- DIA-LIMS-System (Laborinformationen, verknüpft mit Metadaten)
- SoftM/Comarch ERP-System
- Lotus Notes/Domino (Produktanfrage-System - Ersatz geplant)

### Technologie-Stack-Entscheidungen

**Backend [mit Thomas Erhard abzustimmen]:**

- Bevorzugt: FastAPI (Python)
- Einschränkung: IBM Power Prozessorkompatibilität muss verifiziert werden

**Datenverarbeitung:**

- Metadatendatei: Hierarchische Rezeptstrukturen auf eine Ebene abgeflacht
- Relative Mengen auf 100% pro Herstellvorschrift berechnet
- Integration mit DIA-LIMS-Datenfeldern

**AVO-Infrastrukturkontext:**

- Bestehende Technologien: RPG, Java, Profound UI
- Datenbank: DB2 auf IBM i

---

## Abschnitt 7: Datenmodell

### Metadatentabellen-Struktur

Der POC verwendet eine denormalisierte Metadatendatei mit abgeflachten Rezeptdaten. Wesentliche Transformationen:

- Hierarchische Baukasten-Struktur → Tabelle auf einer Ebene
- Relative Mengen auf 100% pro Herstellvorschrift normalisiert
- DIA-LIMS-Daten pro Zutat integriert

**Vollständige Spaltenstruktur:** Siehe [AVO_WS2_Tabellenstruktur Metadatei_20251108.xlsx](https://docs.google.com/spreadsheets/u/0/d/1Avdw2iuCZdbvZSIVa7cGe_zAv2K6298B/edit)

---

## Abschnitt 8: Fachbegriffe

### Rezeptstruktur-Begriffe

**Vormischungen**
Zwischenprodukte mit "V"-Präfix, die eigene Rezepte haben und als Zutaten in Endprodukten verwendet werden.

**Baukasten**
Hierarchisches Rezeptsystem, bei dem Rezepte andere Rezepte als Komponenten enthalten können.

**Herstellvorschrift**
Rezeptspezifikation, die Zutaten und deren Anteile definiert.

**Ansatzgröße**
Produktionsmenge für einen einzelnen Herstelldurchlauf.

### Zutatenkategorisierung

**Material_ID**
Eindeutige Kennung für Zutaten und Komponenten in der Datenbank.

**Rohstoffkategorie**
Funktionale Gruppierung von Zutaten für Substitutionsabgleiche (z.B. "Gewürze/Paprika" für alle Paprikavarianten).

**Materialgruppe**
Einkaufsorientierte Zutatenkategorien (M-Präfix).

### Technische Begriffe

**DIA-LIMS**
Laborinformationsmanagementsystem mit Spezifikationsdaten.

**IBM Save-File (SAVF)**
IBM i Dateiformat zur Datenübertragung zwischen Systemen.

**Metadatei**
Denormalisierte Tabellenstruktur mit abgeflachten Rezeptdaten für die KI-Verarbeitung.

**Muster**
Artikel mit Musterstatus (M-Präfix), die sich noch in der Entwicklung befinden.

---

## Abschnitt 9: Evaluierungsmethodik

### Testdatensatz-Struktur

**Größe:** 100 Rezepte aus der Produktionsdatenbank

**Zusammensetzung:**

- Mindestens 5 bekannte Duplikatpaare, manuell von der AVO-Produktentwicklung identifiziert
- Repräsentiert realistische Produktionsdatenverteilung
- Bekannte Duplikate dienen als Validierungsbasis

**Format:**
IBM Save-File (*SAVF) in Metadatentabellen-Struktur

**Bereitsteller:**
AVO (Mitwirkungspflicht)

### Input/Output-Spezifikation

**Input:**

- Artikelnummer als Abfrageparameter
- Ein Rezeptvergleich pro Anfrage

**Output:**

- Top 5 ähnlichste Rezepte nach Ähnlichkeit geordnet
- Excel-Format basierend auf AVO-Workshop-Vorlage
- Drei Kriterien separat pro Übereinstimmung angezeigt:
  1. Komponenten-Übereinstimmung (Überschneidungsrate)
  2. Mengenähnlichkeit (Prozentuale Ähnlichkeit)
  3. Kategorie-Matching (Rohstoffkategorie-Übereinstimmungen)

### Erfolgskriterien

**Primäre Validierung:**

- Der Algorithmus muss die 5 bekannten Duplikatpaare identifizieren
- Bekannte Duplikate sollten in den Top 5 Ergebnissen für ihre Gegenstücke erscheinen

**Iterative Verfeinerung:**

- AVO-Produktentwicklung prüft Excel-Ausgaben
- Algorithmusparameter werden basierend auf Feedback angepasst
- Schwellenwerte werden iterativ abgestimmt

**Abnahme:**

- Bekannte Duplikate korrekt identifiziert
- Ergebnisse von der Produktentwicklung als nützlich für Harmonisierungsentscheidungen bewertet

### Evaluierungsprozess

1. Testdatensatz (100 Rezepte) in POC-Umgebung laden
2. Ähnlichkeitssuche für jedes Rezept im Testset durchführen
3. Ergebnisse mit AVO-Vorlage nach Excel exportieren
4. AVO prüft Ausgaben und validiert gegen bekannte Duplikate
5. Bei Bedarf Algorithmusparameter anpassen
6. Wiederholen, bis Abnahmekriterien erfüllt sind

**Verantwortung:** Wilsch AI Services implementiert die Evaluierung, AVO validiert die Ergebnisse
