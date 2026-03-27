# Anhang D: KI-gestützte Steuerung und Verifikation sicherer Programmierung

## Zielsetzung

Dieses Kapitel definiert grundlegende organisatorische Kontrollen für die sichere und effektive Nutzung KI-gestützter Programmierwerkzeuge während der Softwareentwicklung und gewährleistet Sicherheit und Rückverfolgbarkeit über den gesamten SDLC hinweg.

---

## AD.1 KI-gestützter sicherer Programmier-Workflow

Integrieren Sie KI-Werkzeuge in den sicheren Softwareentwicklungslebenszyklus (SSDLC) der Organisation, ohne die bestehenden Sicherheitsschranken zu schwächen.

|   #    | Beschreibung                                                                                                                                                                        | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AD.1.1 | Überprüfen Sie, ob ein dokumentierter Workflow beschreibt, wann und wie KI-Tools Code erstellen, umstrukturieren oder überprüfen dürfen.                                            |   1   |  D/V  |
| AD.1.2 | Überprüfen Sie, ob der Workflow jeder SSDLC-Phase (Design, Implementierung, Code-Review, Testen, Bereitstellung) zugeordnet ist.                                                    |   2   |   D   |
| AD.1.3 | Stellen Sie sicher, dass Metriken (z. B. Verwundbarkeitsdichte, mittlere Erkennungszeit) an AI-erzeugtem Code erfasst und mit rein menschlichen Vergleichswerten verglichen werden. |   3   |  D/V  |

---

## AD.2 KI-Werkzeugqualifikation & Bedrohungsmodellierung

Stellen Sie sicher, dass KI-Codierungswerkzeuge vor der Einführung auf Sicherheitsfunktionen, Risiken und Auswirkungen auf die Lieferkette bewertet werden.

|   #    | Beschreibung                                                                                                                                                                                             | Ebene | Rolle |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AD.2.1 | Stellen Sie sicher, dass ein Bedrohungsmodell für jedes KI-Tool Missbrauch, Modellinversion, Datenlecks und Risiken in der Abhängigkeitskette identifiziert.                                             |   1   |  D/V  |
| AD.2.2 | Überprüfen Sie, ob die Toolbewertungen statische/dynamische Analysen aller lokalen Komponenten sowie die Bewertung von SaaS-Endpunkten (TLS, Authentifizierung/Autorisierung, Protokollierung) umfassen. |   2   |   D   |
| AD.2.3 | Überprüfen Sie, ob die Bewertungen einem anerkannten Rahmenwerk folgen und nach wesentlichen Versionsänderungen erneut durchgeführt werden.                                                              |   3   |  D/V  |

---

## AD.3 Sichere Verwaltung von Eingabeaufforderungen und Kontext

Verhindern Sie das Leaken von Geheimnissen, proprietärem Code und persönlichen Daten beim Erstellen von Eingabeaufforderungen oder Kontexten für KI-Modelle.

|   #    | Beschreibung                                                                                                                                                                                                          | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AD.3.1 | Stellen Sie sicher, dass die schriftlichen Richtlinien das Senden von Geheimnissen, Anmeldeinformationen oder klassifizierten Daten in Eingabeaufforderungen verbieten.                                               |   1   |  D/V  |
| AD.3.2 | Überprüfen Sie, ob technische Kontrollen (Client-seitige Schwärzung, genehmigte Kontextfilter) automatisch vertrauliche Artefakte entfernen.                                                                          |   2   |   D   |
| AD.3.3 | Stellen Sie sicher, dass Eingabeaufforderungen und Antworten tokenisiert, während der Übertragung und im Ruhezustand verschlüsselt sind und die Aufbewahrungsfristen der Datenklassifizierungsrichtlinie entsprechen. |   3   |  D/V  |

---

## AD.4 Validierung von KI-generiertem Code

Erkennen und Beheben von durch KI-Ausgabe eingeführten Schwachstellen, bevor der Code zusammengeführt oder bereitgestellt wird.

|   #    | Beschreibung                                                                                                                                                                                | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AD.4.1 | Stellen Sie sicher, dass KI-generierter Code stets einer menschlichen Codeprüfung unterzogen wird.                                                                                          |   1   |  D/V  |
| AD.4.2 | Stellen Sie sicher, dass automatisierte Scanner (SAST/IAST/DAST) bei jedem Pull Request mit KI-generiertem Code ausgeführt werden und Zusammenführungen bei kritischen Befunden blockieren. |   2   |   D   |
| AD.4.3 | Überprüfen Sie, ob differentielles Fuzz-Testing oder eigenschaftsbasierte Tests sicherheitskritische Verhaltensweisen (z. B. Eingabevalidierung, Autorisierungslogik) nachweisen.           |   3   |  D/V  |

---

## AD.5 Erklärbarkeit & Rückverfolgbarkeit von Code-Vorschlägen

Bieten Sie Prüfern und Entwicklern Einblick darin, warum ein Vorschlag gemacht wurde und wie er sich entwickelt hat.

|   #    | Beschreibung                                                                                                                                                                                                        | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AD.5.1 | Überprüfen Sie, ob Prompt/Antwort-Paare mit Commit-IDs protokolliert werden.                                                                                                                                        |   1   |  D/V  |
| AD.5.2 | Überprüfen Sie, ob Entwickler Modellzitate (Trainingsausschnitte, Dokumentation) anzeigen können, die eine Vorschlag unterstützen.                                                                                  |   2   |   D   |
| AD.5.3 | Stellen Sie sicher, dass Erklärbarkeitsberichte zusammen mit Design-Artefakten gespeichert und in Sicherheitsüberprüfungen referenziert werden, um die Rückverfolgbarkeitsprinzipien der ISO/IEC 42001 zu erfüllen. |   3   |  D/V  |

---

## AD.6 Kontinuierliches Feedback & Modellspezifisches Feintuning

Verbessern Sie die Sicherheitsleistung des Modells im Laufe der Zeit, während Sie gleichzeitig eine negative Drift verhindern.

|   #    | Beschreibung                                                                                                                                                                                                                                 | Ebene | Rolle |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AD.6.1 | Verifizieren Sie, dass Entwickler unsichere oder nicht konforme Vorschläge kennzeichnen können und dass diese Kennzeichnungen nachverfolgt werden.                                                                                           |   1   |  D/V  |
| AD.6.2 | Stellen Sie sicher, dass aggregiertes Feedback die periodische Feinabstimmung oder die Retrieval-unterstützte Generierung mit überprüften sicheren Kodierkorpora (z. B. OWASP Cheat Sheets) informiert.                                      |   2   |   D   |
| AD.6.3 | Stellen Sie sicher, dass ein Closed-Loop-Bewertungsharness nach jeder Feinabstimmung Regressions tests durchführt; Sicherheitsmetriken müssen vor der Bereitstellung mindestens den vorherigen Baselines entsprechen oder diese übertreffen. |   3   |  D/V  |

---

### Literaturverzeichnis

* [NIST AI Risk Management Framework 1.0](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)
* [ISO/IEC 42001:2023 — AI Management Systems Requirements](https://www.iso.org/standard/81230.html)
* [OWASP Secure Coding Practices — Quick Reference Guide](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)

