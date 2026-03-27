# C7 Modellverhalten, Ausgabe-Steuerung & Sicherheitsgarantie

## Kontrollziel

Diese Kontrollkategorie stellt sicher, dass Modelloutputs technisch eingeschränkt, validiert und überwacht werden, sodass unsichere, fehlerhafte oder risikoreiche Antworten nicht zu Nutzern oder nachgelagerten Systemen gelangen können.

---

## C7.1 Durchsetzung des Ausgabeformats

Stellen Sie sicher, dass das Modell Daten auf eine Weise ausgibt, die zur Verhinderung von Injection beiträgt.

|   #   | Beschreibung                                                                                                                                                                                                  | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 7.1.1 | Vergewissern Sie sich, dass die Anwendung alle Modellausgaben gegen ein strenges Schema (wie JSON Schema) validiert und jede Ausgabe ablehnt, die nicht übereinstimmt.                                        |   1   |  D/V  |
| 7.1.2 | Überprüfen Sie, ob das System „Stoppsequenzen“ oder Token-Limits verwendet, um die Generierung strikt abzubrechen, bevor es zu einem Überlauf von Puffern oder zur Ausführung unbeabsichtigter Befehle kommt. |   1   |  D/V  |
| 7.1.3 | Verifizieren Sie, dass Komponenten, die das Modelloutput verarbeiten, es als nicht vertrauenswürdige Eingabe behandeln (z. B. durch Verwendung von parametrisierten Abfragen oder sicheren Deserialisierern). |   1   |  D/V  |
| 7.1.4 | Überprüfen Sie, dass das System den spezifischen Fehlertyp protokolliert, wenn eine Ausgabe aufgrund schlechter Formatierung abgelehnt wird.                                                                  |   2   |  D/V  |

---

## C7.2 Halluzinations­erkennung und -minderung

Erkennen, wenn das Modell potenziell ungenaue oder erfundene Inhalte produziert, und verhindern, dass unzuverlässige Ausgaben Benutzer oder nachgelagerte Systeme erreichen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 7.2.1 | Stellen Sie sicher, dass das System die Zuverlässigkeit der generierten Antworten mithilfe einer Methode zur Abschätzung der Vertrauenswürdigkeit oder Unsicherheit bewertet (z. B. Vertrauensbewertung, retrieval-basierte Überprüfung oder Abschätzung der Modellunsicherheit).                                                                                                                                                                           |   1   |  D/V  |
| 7.2.2 | Überprüfen Sie, ob die Anwendung Antworten automatisch blockiert oder auf eine Fallback-Nachricht umschaltet, wenn der Vertrauenswert unter einen definierten Schwellenwert fällt.                                                                                                                                                                                                                                                                          |   2   |  D/V  |
| 7.2.3 | Verifizieren Sie, dass Halluzinationsereignisse (Antworten mit geringer Zuverlässigkeit) mit Ein- und Ausgabe-Metadaten zur Analyse protokolliert werden.                                                                                                                                                                                                                                                                                                   |   2   |  D/V  |
| 7.2.4 | Stellen Sie sicher, dass das System für Antworten, die gemäß der Richtlinie als risikoreich oder mit hoher Auswirkung eingestuft werden, einen zusätzlichen Verifikationsschritt mittels eines unabhängigen Mechanismus durchführt, wie beispielsweise abrufbasierte Verankerung gegen autoritative Quellen, deterministische regelbasierte Validierung, werkzeuggestützte Faktenprüfung oder Konsensüberprüfung durch ein separat bereitgestelltes Modell. |   3   |  D/V  |

---

## C7.3 Ausgabesicherheits- und Datenschutzfilterung

Technische Kontrollen zur Erkennung und Bereinigung von schädlichen Inhalten, bevor sie dem Benutzer angezeigt werden.

|   #   | Beschreibung                                                                                                                                                                                      | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 7.3.1 | Überprüfen Sie, dass automatisierte Klassifizierer jede Antwort scannen und Inhalte blockieren, die den Kategorien Hass, Belästigung oder sexueller Gewalt entsprechen.                           |   1   |  D/V  |
| 7.3.2 | Stellen Sie sicher, dass das System jede Antwort auf personenbezogene Daten (wie Kreditkartennummern oder E-Mail-Adressen) überprüft und diese vor der Anzeige automatisch unkenntlich macht.     |   1   |  D/V  |
| 7.3.3 | Überprüfen Sie, ob Daten, die im System als "vertraulich" gekennzeichnet sind, weiterhin blockiert oder geschwärzt bleiben.                                                                       |   2   |   D   |
| 7.3.4 | Stellen Sie sicher, dass Sicherheitsfilter je nach Benutzerrolle oder Standort unterschiedlich konfiguriert werden können (z. B. strengere Filter für Minderjährige), sofern dies angebracht ist. |   2   |  D/V  |
| 7.3.5 | Überprüfen Sie, ob das System einen menschlichen Genehmigungsschritt oder eine erneute Authentifizierung erfordert, wenn das Modell risikoreiche Inhalte erzeugt.                                 |   3   |  D/V  |

---

## C7.4 Ausgabe- und Aktionsbegrenzung

Verhindern Sie, dass das Modell zu viel, zu schnell macht oder auf Dinge zugreift, auf die es nicht zugreifen sollte.

|   #   | Beschreibung                                                                                                                                                                                                                  | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 7.4.1 | Überprüfen Sie, ob das System strenge Grenzwerte für Anfragen und Token pro Benutzer durchsetzt, um Kostenanstiege und Dienstverweigerungen zu verhindern.                                                                    |   1   |   D   |
| 7.4.2 | Überprüfen Sie, dass das Modell keine weitreichenden Aktionen (wie das Schreiben von Dateien, das Senden von E-Mails oder das Ausführen von Code) ohne ausdrückliche Benutzerbestätigung ausführen kann.                      |   1   |  D/V  |
| 7.4.3 | Stellen Sie sicher, dass die Anwendung oder das Orchestrierungs-Framework die maximale Tiefe von rekursiven Aufrufen, Delegationsgrenzen und die Liste der erlaubten externen Werkzeuge explizit konfiguriert und durchsetzt. |   2   |   D   |

---

## C7.5 Erklärbarkeit & Transparenz

Stellen Sie sicher, dass der Nutzer versteht, warum eine Entscheidung getroffen wurde.

|   #   | Beschreibung                                                                                                                                                                                               | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 7.5.1 | Verifizieren Sie, dass den Benutzern bereitgestellte Erklärungen bereinigt wurden, um Systemaufforderungen oder Backend-Daten zu entfernen.                                                                |   1   |  D/V  |
| 7.5.2 | Stellen Sie sicher, dass die Benutzeroberfläche für kritische Entscheidungen eine Vertrauensbewertung oder eine „Begründungszusammenfassung“ für den Benutzer anzeigt.                                     |   2   |  D/V  |
| 7.5.3 | Stellen Sie sicher, dass technische Nachweise für die Entscheidung des Modells, wie Artefakte zur Modellinterpretierbarkeit (z. B. Aufmerksamkeitskarten, Merkmalsattributierungen), protokolliert werden. |   3   |   D   |

---

## C7.6 Überwachungsintegration

Stellen Sie sicher, dass die Anwendung die richtigen Signale für die Sicherheitsteams sendet, auf die sie achten müssen.

|   #   | Beschreibung                                                                                                                                                                     | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 7.6.1 | Überprüfen Sie, ob das System Echtzeitmetriken für Sicherheitsverletzungen protokolliert (z. B. "Halluzination erkannt", "PII blockiert").                                       |   1   |   D   |
| 7.6.2 | Überprüfen Sie, ob das System einen Alarm auslöst, wenn die Sicherheitsverletzungsraten innerhalb eines definierten Zeitfensters einen festgelegten Schwellenwert überschreiten. |   2   |  D/V  |
| 7.6.3 | Stellen Sie sicher, dass die Protokolle die spezifische Modellversion und andere Details enthalten, die notwendig sind, um potenziellen Missbrauch zu untersuchen.               |   2   |   V   |

---

## C7.7 Schutzmaßnahmen für generative Medien

Verhindern Sie die Erstellung illegaler oder gefälschter Medien.

|   #   | Beschreibung                                                                                                                                                                 | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 7.7.1 | Überprüfen Sie, ob Eingabefilter Aufforderungen blockieren, die explizite oder nicht einvernehmliche synthetische Inhalte anfordern, bevor das Modell diese verarbeitet.     |   1   |  D/V  |
| 7.7.2 | Stellen Sie sicher, dass das System die Erstellung von Medien (Bilder/Audio) ablehnt, die reale Personen ohne verifizierte Zustimmung darstellen.                            |   2   |  D/V  |
| 7.7.3 | Stellen Sie sicher, dass das System generierte Inhalte vor der Veröffentlichung auf Urheberrechtsverletzungen überprüft.                                                     |   2   |   V   |
| 7.7.4 | Überprüfen Sie, dass Versuche, Filter zu umgehen, als Sicherheitsereignisse erkannt und protokolliert werden.                                                                |   2   |  D/V  |
| 7.7.5 | Stellen Sie sicher, dass alle generierten Medien ein unsichtbares Wasserzeichen oder eine kryptografische Signatur enthalten, um nachzuweisen, dass sie KI-generiert wurden. |   3   |  D/V  |

## Literaturverzeichnis

* [OWASP LLM05:2025 Improper Output Handling](https://genai.owasp.org/llmrisk/llm052025-improper-output-handling/)
* [OWASP LLM06:2025 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)

