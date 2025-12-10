# Section 2: Zielbestimmung

## Must (POC Scope)

RAG-System beantwortet DS-Kit Navigationsfragen wie "Wo finde ich X?"

Streaming-Antworten in Echtzeit via Typesense native RAG.

Verarbeitung aller Materialien:
- PDF-Leitfaden März 2025: Direkte Textextraktion
- Excel Q&A: Frage-Antwort-Paare als Trainingsdaten
- ZIP-Vorlagen 56 Dateien: Vision-basierte Zusammenfassungen als Preprocessing

Text-only Ausgabe, sprachfähig, keine URLs, Bilder oder Anhänge.

Ausgabeformat entspricht Excel Antwort-Spalte.

Evaluation: über 90 Prozent korrekte Antworten auf Testfragen.xlsx.

Deployment auf IITR-STAGING Server.

## Deferred (Post-POC)

Konversationsverlauf und Follow-up Fragen.

Integration mit bestehendem Urteile RAG System.

Erweiterte Prompt-Optimierung via Langfuse.

## Out of Scope

Bilder oder Screenshots in Antworten.

Dokument-Verlinkung oder URL-Referenzen.

OCR für gescannte Dokumente.

Keycloak-Authentifizierung.

Navigationspfad-Visualisierung.
