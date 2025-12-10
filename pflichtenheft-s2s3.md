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

---

# Section 3: Funktionale Anforderungen

## Must (POC Scope)

### RAG-System beantwortet DS-Kit Navigationsfragen

FR-01: System nimmt Benutzerfragen in natürlicher Sprache entgegen und liefert relevante Antworten aus dem DS-Kit Korpus.

FR-02: Antworten werden in Echtzeit gestreamt, Token für Token, nicht als vollständige Antwort nach Verarbeitung.

### Verarbeitung aller Materialien

FR-03: PDF-Leitfaden März 2025 wird vollständig extrahiert und für semantische Suche indexiert.

FR-04: Excel Q&A-Paare werden als Referenz-Antworten integriert.

FR-05: ZIP-Vorlagen, 56 Dateien, werden via Vision-Modell zusammengefasst und als Dokumenten-Index indexiert.

### Text-only Ausgabe

FR-06: Antworten enthalten ausschließlich Text. Keine URLs, Bilder, oder Dokumentenanhänge.

FR-07: Antwortformat orientiert sich am Stil der Excel Antwort-Spalte. Zum Beispiel: finden Sie in Kapitel X.

### Qualitätssicherung

FR-08: System erreicht über 90 Prozent korrekte Antworten auf Testfragen.xlsx Evaluationsdatensatz.

## Deferred (Post-POC)

FR-09: System speichert Konversationsverlauf und ermöglicht Follow-up Fragen mit Kontextbezug.

FR-10: Integration mit bestehendem Urteile RAG System für kombinierte Suche.
