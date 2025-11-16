# Richtpreisangebot: Produktionssystem-Erweiterungen

## KI gestützte Rezeptur-Ähnlichkeitserkennung - Post-POC Features

**Projekt:** KI_PROJEKT_SOSSEN_SOURCING
**Kunde:** AVO-Werke August Beisse GmbH
**Auftragnehmer:** Wilsch AI Services OÜ
**Datum:** 2025-11-16

---

## 1. Zusammenfassung

Dieser Kostenvorschlag definiert die Aufwandsschätzungen für die Produktionssystem-Erweiterungen der historischen Rezeptur-Bereinigung nach erfolgreichem POC-Abschluss. Die geschätzten Funktionalitäten erweitern das POC-System um erweiterte Vergleichsfunktionen, intelligente Assistenzfunktionen, erweiterte Vergleichsansichten und eine custom Frontend-Integration.

**Geschätzter Gesamtaufwand:** 32-51 Personentage (exklusive Infrastruktur-FRs)

**Art des Angebots:** Richtpreisangebot (unverbindliche Schätzung)

**Hinweis:** Diese Schätzungen basieren auf der aktuellen Anforderungsdefinition im Pflichtenheft. FR-26 und FR-27 erfordern separate Schätzung durch Thomas Erhard (Infrastruktur-Spezialist). Präzise Aufwandsschätzungen erfordern detaillierte technische Klärung nach POC-Validierung.

---

## 2. Funktionsumfang und Aufwandsschätzung

### 2.1 Erweiterte Vergleichsfunktionen (9-13 Tage)

#### FR-03: Hierarchische Rezepturstrukturen (5-7 Tage)

Unterstützung für Vergleiche auf Vormischungs-Ebene oder aufgelöst auf Basis-Zutaten.

**Teilaufgaben:**
- **Algorithmus-Anpassung für Dual-Modus-Vergleich: 3-4 Tage**
  - Implementierung Vormischungs-Level-Vergleich (Vormischungen als Einheiten behandeln)
  - Implementierung Flattened-Level-Vergleich (alle Basis-Zutaten verwenden)
  - Modus-Parameter-Integration in Algorithmus

- **Benutzereinstellungs-UI: 1-2 Tage**
  - Einstellungsseite mit Modus-Präferenz-Steuerung
  - Speichern/Laden der Benutzereinstellung
  - Einstellung auf alle Suchen anwenden

- **Testing und Validierung: 1-2 Tage**
  - Test beider Modi mit Vormischungen-enthaltenden Rezepturen
  - Validierung mit AVO-Team

**Hinweis:** Erfordert Klärung von AVO-Datenbank-Team zur Vormischungen-Identifizierung in Metadaten.

**Offene Frage:** In der flattened metadata file, wie werden Vormischungen vs. Basis-Zutaten identifiziert?

---

#### FR-07: Filterung nach Spezialattributen (2-3 Tage)

Automatische Attribut-Constraint-Validierung - System schließt Rezepturen aus, die Attribut-Anforderungen verletzen (z.B. Halal vs. non-Halal).

**Teilaufgaben:**
- **Constraint-Prüflogik: 1,5-2 Tage**
  - Attribut-Constraint-Validierung zum Ähnlichkeitsalgorithmus hinzufügen
  - Rezepturen ausschließen, die Constraints verletzen (VLOG, TK, Bio, Halal, Koscher)
  - Fehlende Attribut-Daten behandeln

- **Testing: 0,5-1 Tag**
  - Test verschiedener Attribut-Constraint-Szenarien
  - Verifizierung dass nicht-passende Rezepturen ausgeschlossen werden
  - Edge-Cases (fehlende Attribute)

**Hinweis:** Erfordert Verfügbarkeit von Attribut-Daten (VLOG, TK, Bio, Halal, Koscher) in Metadaten-Datei.

**Offene Frage:** Sind Spezialattribute (VLOG, TK, Bio, Halal, Koscher) in der Metadaten-Datei enthalten?

---

#### FR-10: Konfigurierbare Schwellenwerte (2-3 Tage)

Benutzer-konfigurierbare Schwellenwerte für Ähnlichkeitsberechnungen (Overlap-Ratio, Prozentuale-Differenz, Gesamt-Score).

**Teilaufgaben:**
- **Algorithmus-Parametrisierung: 1-1,5 Tage**
  - Hartcodierte Schwellenwerte ersetzen (Overlap, Prozentuale Differenz, Gesamt-Score)
  - Parameter an Ähnlichkeitsberechnung übergeben
  - Sicherstellen dass alle drei Schwellenwerte korrekt angewendet werden

- **Einstellungs-UI: 1-1,5 Tage**
  - Einstellungsseite mit drei Schwellenwert-Eingabe-Kontrollen
  - Standardwerte für jeden Schwellenwert
  - Speichern/Laden der Benutzereinstellungen

- **Testing: 0,5 Tag**
  - Test verschiedener Schwellenwert-Kombinationen
  - Verifizierung der Auswirkung auf Ergebnisse

---

### 2.2 Intelligente Assistenzfunktionen (16-24 Tage)

#### FR-12: Chat-Interface für interaktive Anfragen (8-13 Tage)

Conversational Interface über vorberechnete Ähnlichkeitsergebnisse mit lokalem Open-Source LLM.

**Teilaufgaben:**
- **Lokales LLM-Deployment: 2-3 Tage**
  - Auswahl und Deployment eines Open-Source-Modells (Llama, Mistral, etc.) auf IBM Power
  - Modell-Konfiguration und Optimierung
  - API-Endpunkt-Setup

- **Conversational Result-Abruf: 1-2 Tage**
  - Artikelnummer aus Benutzer-Nachricht extrahieren
  - Vorberechnete Ergebnisse aus Cache/Datenbank abrufen
  - Formatierung für Chat-Präsentation

- **Ergebnis-Erklärung und Reasoning: 2-3 Tage**
  - LLM erklärt warum Rezepturen ähnlich sind
  - Hervorhebung wichtiger Unterschiede/Übereinstimmungen
  - Beantwortung von Folgefragen zu Ergebnissen

- **Chat-UI: 2-3 Tage**
  - Chat-Widget mit persistenter Nachrichten-Historie
  - Multi-Turn-Konversations-Anzeige
  - Ladezustände und Tipp-Indikatoren

- **Testing: 1-2 Tage**
  - Test von Konversations-Flows
  - Prompt-Verfeinerung für Genauigkeit
  - Performance-Testing

**Hinweis:** Verwendet Open-Source LLM (lokal deployed) mit Multi-Turn-Dialog. Erfordert Infrastruktur-Koordination mit Thomas Erhard.

**Offene Frage für Thomas:** Welches spezifische Open-Source-Modell (Llama 3, Mistral, etc.)? Deployment-Ansatz auf IBM Power?

---

#### FR-23: Lernfähigkeit für Substitutionen (3-4 Tage)

System merkt sich akzeptierte Zutaten-Substitutionen für zukünftige Vorschläge.

**Teilaufgaben:**
- **Substitutions-Speicherung: 1-1,5 Tage**
  - Datenbank-Tabelle für bestätigte Substitutionen
  - Speicherung von Zutat_A ↔ Zutat_B Paaren (bidirektional)
  - Validierung dass beide Zutaten in derselben Rohstoffkategorie sind

- **Algorithmus-Integration: 1-1,5 Tage**
  - Bestätigte Substitutionen laden
  - Auf Kategorie-Matching (FR-08) anwenden
  - Benutzer-bestätigte Substitutionen als gültige Matches behandeln

- **UI für Substitutions-Akzeptierung: 1 Tag**
  - "Substitution akzeptieren"-Button wenn System Kategorie-Match vorschlägt
  - Ansicht/Verwaltung gespeicherter Substitutionen

- **Testing: 0,5-1 Tag**
  - Verifizierung dass Substitutionen persistieren
  - Test des Einflusses auf zukünftige Vergleiche

**Hinweis:** Substitutionen nur gültig innerhalb derselben Rohstoffkategorie (bidirektional).

---

#### FR-24: Visuelle Hervorhebung (5-7 Tage)

Visuelle Hervorhebung von prozentualen Unterschieden mit konfigurierbarem Farbcodierung und Slider-Controls (Web + Excel).

**Teilaufgaben:**
- **Prozentuale Differenz-Berechnung: 1 Tag**
  - Berechnung von Zutaten-Level-Differenzen
  - Aggregation für Rezeptur-Level-Übersicht

- **Dual-View-Hervorhebung: 1,5-2 Tage**
  - Zutaten-Level farbcodierte Anzeige
  - Rezeptur-Level Zusammenfassungs-Indikator
  - Farbschema-Design

- **Dual-Slider-Controls: 1,5-2 Tage**
  - Schwellenwert-Slider (filtert was angezeigt wird)
  - Farbintensitäts-Slider (passt Hervorhebungsstärke an)
  - Echtzeit-Updates für beide
  - Einstellungen persistieren

- **Excel Conditional Formatting: 1-1,5 Tage**
  - Conditional-Formatting-Regeln zum Excel-Export hinzufügen
  - Farbcodierung prozentualer Unterschiede in Excel-Zellen
  - Feste Schwellenwert-Regeln (kein Slider in Excel)

- **Testing: 0,5-1 Tag**
  - Test von Web-Hervorhebung + Slidern
  - Test von Excel-Export mit Conditional Formatting

**Hinweis:** Dual-Slider (Schwellenwert + Farbintensität), Dual-Views (Zutaten + Rezeptur), Excel Conditional Formatting.

---

### 2.3 Erweiterte Vergleichsansichten (3-4 Tage)

#### FR-25: Zutaten- und Rezeptur-Level-Ansichten (3-4 Tage)

Dual-View-Modi mit Tab-UI: Zutaten-Level-Detail + Rezeptur-Level-Übersicht (gruppiert).

**Teilaufgaben:**
- **Zutaten-Level-Ansicht: 1-1,5 Tage**
  - Flache Tabelle mit allen Zutaten
  - Prozent-Spalten pro Rezeptur
  - Differenz-Berechnungen

- **Rezeptur-Level-Ansicht: 1-1,5 Tage**
  - Dieselben Zutaten-Daten, andere Gruppierung
  - Ähnlichkeits-Scores-Anzeige hinzufügen
  - Zusammenfassungs-Statistiken hinzufügen
  - Gruppiertes Layout (nach Kategorie/Match-Typ)

- **Tab-UI: 0,5-1 Tag**
  - Tab-Interface zum Wechseln der Ansichten
  - Tab-Präferenz persistieren

- **Testing: 0,5 Tag**
  - Test beider Ansichten
  - Verifizierung der Berechnungs-Genauigkeit

**Hinweis:** Beide Views zeigen ähnliches Detail, nur unterschiedlich gruppiert.

---

### 2.4 Custom Frontend (4-7 Tage)

#### FR-28: Custom Comparison Frontend Interface (4-7 Tage) **[NEU]**

Benutzerdefiniertes Side-by-Side-Layout (OpenWebUI Chat + Vergleichs-Panel) - Desktop-optimiert.

**Teilaufgaben:**
- **OpenWebUI + LLM-Server-Setup: 1-2 Tage**
  - OpenWebUI konfigurieren um mit lokalem Inference-Server zu verbinden
  - Chat-Funktionalität mit LLM testen

- **Layout + Koordinations-Logik: 2-4 Tage**
  - Side-by-Side-Layout erstellen (OpenWebUI-Panel + Vergleichs-Panel)
  - Chat → Vergleichs-Datenfluss implementieren
  - Gecachte Ergebnisse abrufen und anzeigen
  - Desktop-optimiertes Layout

- **Testing: 1 Tag**
  - Chat-zu-Vergleich-Flow
  - Cross-Browser-Testing (Desktop)

**Hinweis:** Ersetzt POC-UI - wird Produktions-Interface. Desktop-only (kein responsive Design erforderlich).

---

### 2.5 Dateninfrastruktur (TBD - Thomas Erhard)

#### FR-26: JDBC-Datenbankintegration

**Status:** Zu schätzen durch Thomas Erhard (Infrastruktur-Spezialist)

Direkte JDBC-Abfrage der Rezepturdatenbank (IBM AS/400 DB2).

**Vorgeschlagene Teilaufgaben (zur Referenz):**
- JDBC-Treiber-Setup und Verbindungskonfiguration (1-2 Tage)
- Query-Entwicklung und Optimierung (2-3 Tage)
- Daten-Mapping und Transformation (2-3 Tage)
- Connection-Management und Error-Handling (1-2 Tage)
- Testing mit Produktions-Datenbank (1-2 Tage)

**Offene Fragen für Thomas:**
- Ersetzt JDBC die Metadaten-Datei vollständig oder komplementiert sie?
- Performance-Anforderungen für Datenbank-Queries?
- Network/VPN-Setup-Timeline und Koordination?

---

#### FR-27: Automatische Metadaten-Batch-Verarbeitung

**Status:** Zu schätzen durch Thomas Erhard (Infrastruktur-Spezialist)

Automatisches System auf IBM i LPAR zur Metadaten-Generierung.

**Vorgeschlagene Teilaufgaben (zur Referenz):**
- IBM i Batch-Job-Entwicklung für Datenextraktion (3-4 Tage)
- Daten-Transformationslogik (Hierarchie-Flattening) (2-3 Tage)
- Scheduling und Automatisierung (1-2 Tage)
- MindsDB/JDBC-Integration für Datentransfer (2-3 Tage)
- Error-Handling und Monitoring (1-2 Tage)
- Testing und Validierung mit AVO (1-2 Tage)

**Offene Fragen für Thomas:**
- Implementierungs-Ansatz für IBM i Batch-Verarbeitung
- Daten-Transfer-Mechanismus (MindsDB/JDBC vs. File-Transfer)
- Batch-Zyklus-Frequenz-Anforderungen

**Hinweis:** Erfordert IBM i Expertise (RPG/CL Programmierung) und Koordination mit AVO-Infrastruktur-Team.

---

## 3. Offene Fragen

### Für AVO/Datenbank-Team:
1. **Vormischungen-Identifizierung (FR-03):** In der flattened Metadata-Datei, wie werden Vormischungen vs. Basis-Zutaten identifiziert?
2. **Attribut-Daten (FR-07):** Sind Spezialattribute (VLOG, TK, Bio, Halal, Koscher) in der Metadaten-Datei enthalten?

### Für Thomas Erhard (Infrastruktur):
3. **FR-26 JDBC-Integration:** Vollständige Schätzung erforderlich
4. **FR-27 Batch-Verarbeitung:** Vollständige Schätzung erforderlich
5. **LLM-Deployment (FR-12):** Welches Open-Source-Modell? Deployment-Ansatz auf IBM Power?

---

## 4. Risikohinweise

### Technische Abhängigkeiten

**FR-27 (Batch-Verarbeitung):**
- Erfordert IBM i Programmierung (RPG oder ähnlich)
- Abhängig von AVO-Infrastruktur-Team-Koordination
- Höhere Unsicherheit in Aufwandsschätzung

**FR-26 (JDBC-Integration):**
- Netzwerk-/VPN-Konfiguration erforderlich
- Datenbank-Performance-Optimierung möglicherweise iterativ

**FR-12 (Chat-Interface):**
- Open-Source LLM-Deployment auf IBM Power
- Infrastruktur-Koordination mit Thomas Erhard
- Iterative Prompt-Verfeinerung erforderlich

### Daten-Abhängigkeiten

**FR-03 (Hierarchische Strukturen):**
- Abhängig von Vormischungen-Identifizierungs-Methode in Metadaten
- Fallback-Strategie erforderlich falls Identifizierung nicht möglich

**FR-07 (Attribut-Filterung):**
- Abhängig von Verfügbarkeit der Spezialattribute in Metadaten

### Komplexitätsfaktoren

**Custom Frontend (FR-28):**
- OpenWebUI-Integration
- Side-by-Side-Layout-Koordination
- Chat-zu-Vergleich-Datenfluss

**Dual-View-Implementierungen (FR-24, FR-25):**
- Mehrere Slider-Controls
- Zutaten + Rezeptur Level Views
- Excel + Web Conditional Formatting

---

## 5. Nächste Schritte

1. **POC-Abschluss und Validierung**
2. **Klärung offener Fragen** mit AVO-Datenbank-Team und Thomas Erhard
3. **Thomas Erhard Infrastruktur-Schätzung** für FR-26 und FR-27
4. **Festpreisangebot** nach Fragen-Klärung und Infrastruktur-Schätzung

---

## 6. Aufwandsübersicht

| Funktionsbereich | Geschätzter Aufwand |
|------------------|---------------------|
| Erweiterte Vergleichsfunktionen | 9-13 Tage |
| Intelligente Assistenzfunktionen | 16-24 Tage |
| Erweiterte Vergleichsansichten | 3-4 Tage |
| Custom Frontend | 4-7 Tage |
| Dateninfrastruktur (FR-26, FR-27) | **TBD - Thomas Erhard** |
| **GESAMT (exkl. Infrastruktur)** | **32-51 Tage** |

---

**Hinweis:** Diese Schätzungen sind Richtwerte für initiale Budgetplanung. FR-26 und FR-27 erfordern separate Schätzung durch Thomas Erhard (Infrastruktur-Spezialist). Präzise Aufwandsschätzungen erfordern detaillierte technische Spezifikation nach POC-Validierung und Klärung offener Fragen.
