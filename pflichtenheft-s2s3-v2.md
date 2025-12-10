# Section 2: Zielbestimmung

## Must (POC Scope)

RAG-System beantwortet DS-Kit Navigationsfragen wie "Wo finde ich X?"

Streaming-Antworten in Echtzeit via Typesense native RAG.

Konversationsverlauf mit Follow-up Fragen. Das kommt kostenlos mit Typesense native RAG.

Chat-Interface via OpenWebUI.

Verarbeitung aller Materialien:
- PDF-Leitfaden März 2025: Direkte Textextraktion
- Excel Q&A: Frage-Antwort-Paare als Trainingsdaten
- ZIP-Vorlagen 56 Dateien: Vision-basierte Zusammenfassungen als Preprocessing

Text-only Ausgabe, sprachfähig, keine URLs, Bilder oder Anhänge.

Ausgabeformat entspricht Excel Antwort-Spalte.

Evaluation: über 90 Prozent korrekte Antworten auf Testfragen.xlsx.

Deployment auf IITR-STAGING Server.

## Deferred (Post-POC)

Integration mit bestehendem Urteile RAG System.

Erweiterte Prompt-Optimierung via Langfuse.

## Out of Scope

Bilder oder Screenshots in Antworten.

Dokument-Verlinkung oder URL-Referenzen.

OCR für gescannte Dokumente.

Keycloak-Authentifizierung.

Navigationspfad-Visualisierung.

---

# Section 3: Funktionale Anforderungen

## Must (POC Scope)

### RAG-System beantwortet DS-Kit Navigationsfragen

FR-01: System nimmt Benutzerfragen in natürlicher Sprache entgegen und liefert relevante Antworten aus dem DS-Kit Korpus.

FR-02: Antworten werden in Echtzeit gestreamt, Token für Token, nicht als vollständige Antwort nach Verarbeitung.

FR-03: System speichert Konversationsverlauf und ermöglicht Follow-up Fragen mit Kontextbezug.

### Chat-Interface

FR-04: OpenWebUI dient als Chat-Interface für Benutzerinteraktion.

### Verarbeitung aller Materialien

FR-05: PDF-Leitfaden März 2025 wird vollständig extrahiert und für semantische Suche indexiert.

FR-06: Excel Q&A-Paare werden als Referenz-Antworten integriert.

FR-07: ZIP-Vorlagen, 56 Dateien, werden via Vision-Modell zusammengefasst und als Dokumenten-Index indexiert.

### Text-only Ausgabe

FR-08: Antworten enthalten ausschließlich Text. Keine URLs, Bilder, oder Dokumentenanhänge.

FR-09: Antwortformat orientiert sich am Stil der Excel Antwort-Spalte. Zum Beispiel: finden Sie in Kapitel X.

### Qualitätssicherung

FR-10: System erreicht über 90 Prozent korrekte Antworten auf Testfragen.xlsx Evaluationsdatensatz.

## Deferred (Post-POC)

FR-11: Integration mit bestehendem Urteile RAG System für kombinierte Suche.
