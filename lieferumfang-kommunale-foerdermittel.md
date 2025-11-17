# SECTION 4: Lieferumfang - DRAFT

### 4.1 Landing Page für Gemeinden

Öffentlich zugängliche Website mit responsivem Design (Desktop/Tablet/Mobile), die Gemeinden über den Klimafolgenschutzverein und die Fördermittelsuche informiert. Umfasst Hero-Section mit Wertversprechen, "So funktioniert's"-Ablauf, und "Über uns"-Bereich. Die Seite leitet Gemeinden nahtlos zum Fragebogen und positioniert den Verein als kompetenten Partner für Fördermittelerschließung.

### 4.2 Interaktiver Projekt-Fragebogen

Strukturiertes Formular zur Erfassung von Gemeindeprojekten: Projekttyp (Digitalisierung, Klimaschutz, Infrastruktur), Umfang, Budget, und Gemeindeinformationen. Der Fragebogen konvertiert qualitative Projektbeschreibungen in maschinenlesbare Parameter für präzise KI-Suche. Eingebettet als benutzerfreundliches Interface ohne Registrierungsanforderung.

### 4.3 KI-gestützte Förderprogramm-Suchmaschine

Semantische Such-Engine, die eine konsolidierte Förderdatenbank (initialer Fokus auf eine Primärquelle, in Workshop 2 definiert) durchsucht. Das System versteht Projektintentionen über Schlagwortsuche hinaus und bewertet Förderprogramme anhand inhaltlicher Passung, Budgetkompatibilität, und Gemeinde-Eignung. Automatisierte Aktualisierung hält Förderinformationen aktuell.

### 4.4 Ergebnisanzeige & Lead-Erfassung

Übersichtliche Darstellung der 2-3 relevantesten Förderprogramme mit geschätzten Beträgen, Förderquoten, und Programmbeschreibungen. Das System speichert Fragebogen-Eingaben und angezeigte Ergebnisse für Folgeberatung, sodass der Klimafolgenschutzverein kontextbezogene Gespräche mit interessierten Gemeinden führen kann.

### 4.5 Produktions-Infrastruktur

Vollständig deploytes System auf produktionsreifer Infrastruktur: FastAPI-Backend auf Hetzner-Server (Frankfurt), React-Frontend auf Vercel, Supabase-Datenbank für Lead-Daten, und Typesense-Instanz für Vektorsuche. Alle Komponenten konfiguriert, gesichert, und für öffentlichen Zugriff bereit.

### 4.6 Technische & Benutzerdokumentation

Umfassende Dokumentation für technisches Handoff und Plattform-Nutzung: API-Spezifikationen, Deployment-Prozess, Datenbankschema, Troubleshooting-Guide, und Benutzeranleitung für Gemeinden. Ermöglicht zukünftige Wartung und Erweiterung des Systems.

### 4.7 Workshop 2: Definierte Requirements-Spezifikation

Vollständig dokumentierte Spezifikation aller offenen Requirements aus Workshop 2: finalisierte Fragebogen-Struktur mit Feldern und Validierung, Paket-Kategorisierungsregeln, ausgewählte Förderdatenbank mit Integrationsplan, und Evaluationskriterien. Diese Spezifikation bildet die Grundlage für POC-Entwicklung und zukünftige Erweiterungen.
