# Pflichtenheft

## Kommunale Fördermittel-Suchplattform

---

## Section 1: Cover Page (Deckblatt)

|  |  |
| :---- | :---- |
| **Project** | Kommunale Fördermittel-Suchplattform |
| **Client** | Casa Curata UG GmbH |
| **Contractor** | Wilsch AI Services OÜ |

---

## Section 2: Goal Determination (Zielbestimmung)

### Muss (POC-Umfang)

- Website mit Landing Page für Klimafolgenschutzverein mit Zielgruppe Gemeinden
- Interaktiver Fragebogen zur Erfassung von Projektdetails (Typ, Umfang, Budget, Gemeindeinformationen)
- KI-gestützte semantische Suche in Förderdatenbanken (beginnend mit einer Datenbank)
- Anzeige relevanter Förderprogramme mit geschätzten Beträgen und Prozentsätzen (2-3 Ergebnisse)
- Paketbasierte Kategorisierung für standardisierte Projekte (Digitalisierung, Klimaschutz, Infrastruktur)
- Lead-Generierung mit Weiterleitung zur Vereinsmitgliedschaft
- Datenerfassung für Folgeberatung

### Zurückgestellt (Nach POC)

- Dokumenten-Upload-Funktion (Kostenvoranschläge, Planungsdokumente von Architekten)
- Direkte Förderantragstellung über Plattform-Schnittstelle
- Browser-Automation zum Ausfüllen externer Förderformulare
- Detaillierte personalisierte Beratungs- und Betreuungsleistungen
- Integration mit EE-Mann (Energieeffizienz-Experte) Workflow

---

## Section 3: Functional Requirements (Funktionale Anforderungen)

### Muss (POC-Umfang)

**Website mit Landing Page für Klimafolgenschutzverein mit Zielgruppe Gemeinden**

- **FR-07:** System stellt Informationsinhalte über Mission und Leistungen des Klimafolgenschutzvereins bereit.

**Interaktiver Fragebogen zur Erfassung von Projektdetails**

- **FR-01:** System stellt interaktiven Fragebogen bereit zur Erfassung von Projektdetails einschließlich Typ (Digitalisierung, Klimaschutz, Infrastruktur), Umfang, Budget und Gemeindeinformationen.

**KI-gestützte semantische Suche in Förderdatenbanken**

- **FR-02:** System durchsucht eine Förderdatenbank (spezifische Quelle in Workshop 2 festzulegen) mittels semantischer Übereinstimmung basierend auf Fragebogen-Eingaben.

**Anzeige relevanter Förderprogramme mit geschätzten Beträgen und Prozentsätzen**

- **FR-03:** System zeigt 2-3 relevante Förderprogramme mit geschätzten Beträgen, Prozentbereichen und Programmbeschreibungen an.

**Paketbasierte Kategorisierung für standardisierte Projekte**

- **FR-04:** System kategorisiert Projekte in vordefinierte Pakete (z.B. Digitalisierung klein/mittel/groß, Infrastruktur, Klimaschutzmaßnahmen).

**Lead-Generierung mit Weiterleitung zur Vereinsmitgliedschaft**

- **FR-05:** System leitet Benutzer nach Anzeige der Fördermöglichkeiten zum Mitgliedsantrag des Vereins weiter.

**Datenerfassung für Folgeberatung**

- **FR-06:** System erfasst und speichert Kontaktinformationen der Gemeinde und identifizierte Förderinteressen für Folgeberatung.

### 

### Zurückgestellt (Nach POC)

**Dokumenten-Upload-Funktion**

- **FR-08:** System akzeptiert Dokumenten-Uploads (Kostenvoranschläge, Planungsdokumente) für präzisere Fördermittelsuche.

**Direkte Förderantragstellung über Plattform-Schnittstelle**

- **FR-09:** System ermöglicht direkte Einreichung von Förderanträgen an BAFA/KfW-Portale im Namen der Gemeinden.

**Integration mit EE-Mann (Energieeffizienz-Experte) Workflow**

- **FR-10:** System integriert mit EE-Mann-Workflow für Projekte die Expertenvalidierung erfordern.

### Funktionale Anforderungsabhängigkeiten

**FR-02 hängt ab von FR-01**

- Fragebogen (FR-01) erfasst strukturierte Projektparameter, die die KI-semantische Suche (FR-02) verwendet, um Förderdatenbanken effektiv abzufragen.

**FR-03 hängt ab von FR-02**

- Suche muss abgeschlossen sein (FR-02) und Ergebnisse zurückgeben, bevor System Förderprogramme (FR-03) dem Benutzer anzeigen kann.

**FR-04 hängt ab von FR-01**

- Paketkategorisierung (FR-04) verwendet Projektdetails aus Fragebogen (FR-01), um Projekt in vordefinierte standardisierte Angebote zu klassifizieren.

**FR-05 hängt ab von FR-03**

- Benutzer muss zuerst Fördermöglichkeiten sehen (FR-03), bevor er zum Mitgliedsantrag weitergeleitet wird (FR-05) im Rahmen der Lead-Generierung.

**FR-06 hängt ab von FR-01, FR-03**

- Datenerfassung (FR-06) speichert sowohl Fragebogen-Eingaben (FR-01) als auch welche Förderergebnisse (FR-03) der Benutzer ansah für Folgeberatungszwecke.

**FR-09 hängt ab von FR-08** (Zurückgestellt)

- Dokumenten-Uploads (FR-08) liefern die detaillierten Kostendaten, die zum Vorausfüllen direkter Antragseinreichungen (FR-09) an Förderportale benötigt werden.

---

## Section 4: Liste der nicht-funktionalen Anforderungen (Non-Functional Requirements)

Non-functional requirements (performance, security, compatibility, and usability specifications) will be defined during Workshop 2.

---

## Section 5: Abnahmekriterien (Acceptance Criteria)

| Anforderungs-ID | Abnahmetest | Erwartetes Ergebnis |
| :---- | :---- | :---- |
| FR-01 | Wenn Benutzer Website aufruft und Fragebogen lädt | Dann werden alle erforderlichen Eingabefelder angezeigt und sind funktionsfähig |
| FR-02 | Wenn Fragebogen eingereicht wird und Suche ausgeführt wird | Dann werden Förderprogramme aus angegebener Datenbank zurückgegeben |
| FR-03 | Wenn Suche abgeschlossen ist und Ergebnisse angezeigt werden | Dann werden 2-3 relevante Förderprogramme mit Prozentbereichen und Beträgen angezeigt |
| FR-04 | Wenn Projektdetails eingereicht werden und Kategorisierung ausgeführt wird | Dann wird Projekt der entsprechenden Paketkategorie zugewiesen |
| FR-05 | Wenn Ergebnisse angezeigt werden und Benutzer Seite ansieht | Dann ist Mitgliedsantrags-CTA sichtbar und funktionsfähig |
| FR-06 | Wenn Benutzerinteraktionen abgeschlossen sind und Datenerfassung ausgeführt wird | Dann werden Gemeinde-Kontaktinformationen und Förderinteressen gespeichert |
| FR-07 | Wenn Benutzer Landing Page aufruft und Seite lädt | Dann werden Klimafolgenschutzverein-Informationsinhalte angezeigt |

### Zurückgestellte Abnahmekriterien (Nach POC)

| Anforderungs-ID | Abnahmetest | Erwartetes Ergebnis |
| :---- | :---- | :---- |
| FR-08 | Wenn Benutzer Dokument hochlädt und Dateiverarbeitung abgeschlossen ist | Dann wird Dokumentinhalt extrahiert und zur Suchverbesserung verwendet |
| FR-09 | Wenn Förderprogramm ausgewählt wird und Einreichung initiiert wird | Dann werden Antragsdaten an entsprechendes Portal übermittelt (BAFA/KfW) |
| FR-10 | Wenn Projekt EE-Mann erfordert und Workflow ausgelöst wird | Dann wird Expertenvalidierungsprozess initiiert |

---

## Section 6: Technische Rahmen- oder Randbedingungen (Technical Constraints)

### Deployment-Umgebung

- **Backend:** Hetzner Server (Rechenzentrum Frankfurt)
- **Frontend:** Vercel Plattform
- Cloud-basierte Architektur mit Trennung der Zuständigkeiten

### Erforderliche Integrationen

- Initiale Integration mit einer Förderdatenbank (spezifische Quelle in Workshop 2 festzulegen: Förderdatenbank, KfW oder BAFA)
- Integrationsmethode in Workshop 2 festzulegen (API-Zugriff vs. Web Scraping)
- Zusätzliche Datenbanken auf Nach-POC verschoben

### Technologie-Stack-Entscheidungen

- **Backend Framework:** FastAPI (Python)
- **Frontend Framework:** React
- **Datenbank:** Supabase (für Gemeinde-Kontaktdaten und Suchergebnisspeicherung)
- **Deployment:** Backend auf Hetzner, Frontend auf Vercel
- **API-Kommunikation:** REST API zwischen React Frontend und FastAPI Backend
- **Authentifizierung:** Keine Benutzerauthentifizierung für POC erforderlich (öffentlicher Zugriff für Gemeinden)

---

## Section 7: Data Model (Datenmodell) \- SKIPPED

---

## Section 8: Domain Glossary (Glossar / Fachglossar)

### Schlüsselbegriffe

**Fördermittel**

- Staatliche Zuschüsse oder Beihilfen für Gemeinden für öffentliche Projekte.

**Förderdatenbank**

- Zentrale deutsche Datenbank mit Informationen über verfügbare Förderprogramme aus verschiedenen Quellen.

**Gemeinde**

- Kommune oder lokale Regierungseinheit in Deutschland.

**KfW (Kreditanstalt für Wiederaufbau)**

- Staatliche deutsche Förderbank, die subventionierte Darlehen und Zuschüsse für Infrastruktur- und Klimaprojekte bereitstellt.

**BAFA (Bundesamt für Wirtschaft und Ausfuhrkontrolle)**

- Bundesamt für Wirtschaft und Ausfuhrkontrolle, verwaltet verschiedene Förderprogramme.

**EE-Mann (Energieeffizienz-Experte)**

- Energieeffizienz-Experte, der zur Validierung und Genehmigung bestimmter Klima-/Bauprojekte für Förderberechtigung erforderlich ist.

**Klimafolgenschutzverein**

- Klimafolgenschutzverein (Kundenorganisation), unterstützt Gemeinden beim Zugang zu klimabezogenen Förderungen.

**Bürgermeister**

- Bürgermeister einer Gemeinde, wichtigster Entscheidungsträger für Projektgenehmigungen.

**Kämmerer**

- Gemeindekämmerer, verantwortlich für Finanzplanung und Budgetverwaltung.

**Digitalisierung**

- Digitalisierung kommunaler Verwaltungsprozesse und -dienstleistungen.

---

## Section 9: Evaluationsinfrastruktur (KI-Spezifisches Testen)

### Test-Datensätze

-
### Erfolgsmetriken

-
### Eingabe/Ausgabe-Spezifikationen

- **Eingabe:** Fragebogen-Antworten (Struktur in Workshop 2 festzulegen)
- **Ausgabe:** 2-3 Förderprogramme mit Prozentsätzen und Beträgen (Format in Workshop 2 festzulegen)

### Validierungsprozess

- **Validierer:** Casa Curata UG (Kunde) validiert KI-Empfehlungen während POC
- **Methode:** Kunde prüft Suchergebnisse basierend auf Förderprogramm-Kenntnissen


