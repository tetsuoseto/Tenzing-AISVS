# C7 Modellverhalten, Ausgabe-Steuerung & Sicherheitsgewährleistung

## Kontrollziel

Diese Kontrollkategorie stellt sicher, dass die Modellausgaben technisch eingeschränkt, validiert und überwacht werden, sodass unsichere, fehlerhafte oder risikoreiche Antworten nicht zu den Nutzern oder nachgelagerten Systemen gelangen. Das Kapitel behandelt AI-spezifische Anforderungen an die Ausgabehandhabung: Format- und Schemaerzwingung für die Modellausgabe, Umgang mit Vertrauen und Unsicherheit, sicherheitsbezogene Filterung der Ausgabe sowie Explainability-Artefakte. Die Validierung der Schema-Ausgabe (7.1.1) gilt nur für Anwendungen, die strukturierte Ausgaben erwarten (z. B. JSON, XML, typisierte function-call-Antworten); frei formulierte Texteingaben fallen nicht in den Anwendungsbereich der Schema-Validierung.

---

## C7.1 Formatdurchsetzung der Ausgabe

Stellen Sie sicher, dass das Modell Daten so ausgibt, dass dadurch das Risiko von Injection-Angriffen verringert wird.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                       | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 7.1.1 | Stellen Sie sicher, dass die Anwendung alle Modelloutputs gegen ein striktes Schema (z. B. JSON Schema) validiert und Ausgaben zurückweist, die nicht übereinstimmen.                                                                                                                                                                                              |   1   |
| 7.1.2 | Stellen Sie sicher, dass das System entweder „Stop-Sequenzen“ oder Token-Limits verwendet, um die Generierung strikt vor dem Überlaufen von Puffern oder der Ausführung unbeabsichtigter Befehle abzubrechen.                                                                                                                                                      |   1   |
| 7.1.3 | Stellen Sie sicher, dass Modell-Ausgaben, die eine Vertrauensgrenze in nachgelagerte Interpreter überschreiten (z.B. Datenbanken, Shells, Deserialisierer, Template-Engines, Browser), als nicht vertrauenswürdige Eingaben behandelt und mithilfe der entsprechenden sicheren APIs verarbeitet werden, wie in den OWASP ASVS v5 Kapiteln V1.2 und V1.5 definiert. |   1   |

---

## C7.2 Halluzinationsdetektion & -minderung

Erkennen, wenn das Modell möglicherweise ungenaue oder erfundene Inhalte erzeugt, und verhindern, dass unzuverlässige Ausgaben Nutzer oder nachgelagerte Systeme erreichen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.2.1 | Stellen Sie sicher, dass das System die Zuverlässigkeit generierter Antworten mithilfe einer Konfidenz- oder Unsicherheitsschätzungsmethode bewertet (z.B. Konfidenzbewertung, verifizierungsbasiert auf Abrufen oder Schätzung der Modellunsicherheit).                                                                                                                                                                                                        |   1   |
| 7.2.2 | Überprüfen Sie, dass die Anwendung automatisch Antworten blockiert oder auf eine Fallback-Nachricht umschaltet, wenn der Konfidenzwert unter eine definierte Schwelle fällt.                                                                                                                                                                                                                                                                                    |   2   |
| 7.2.3 | Überprüfen Sie, dass Halluzinationsereignisse (antworten mit geringer Konfidenz) mit Eingabe-/Ausgabe-Metadaten zur Analyse protokolliert werden. (Für die aggregierte Überwachung der Halluzinationsrate im Zeitverlauf siehe C13.3.5.)                                                                                                                                                                                                                        |   2   |
| 7.2.4 | Stellen Sie sicher, dass das System den Verlauf von Tool- und Funktionsaufrufen innerhalb einer Anfragekette nachverfolgt und hochkonfidente faktische Behauptungen kennzeichnet, die nicht von relevantem Tool-Usage zur Verifikation vorausgegangen sind, als praktisches Halluzinations-Erkennungssignal unabhängig von der Konfidenzbewertung.                                                                                                              |   2   |
| 7.2.5 | Verifizieren Sie, dass das System für Antworten, die gemäß Richtlinie als hochriskant oder von hoher Auswirkung eingestuft werden, einen zusätzlichen Verifizierungsschritt über einen unabhängigen Mechanismus durchführt, z. B. eine an Retrieval gebundene Absicherung anhand maßgeblicher Quellen, eine deterministische regelbasierte Validierung, eine toolbasierte Faktenprüfung oder eine Konsensüberprüfung durch ein separat bereitgestelltes Modell. |   3   |

---

## C7.3 Ausgabesicherheit & Datenschutzfilterung

Technische Kontrollen zur Erkennung und Bereinigung problematischen Inhalts, bevor er dem Nutzer angezeigt wird.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                  | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.3.1 | Stellen Sie sicher, dass automatische Klassifizierer jede Antwort scannen und Inhalte blockieren, die mit den Kategorien Hass, Belästigung oder sexueller Gewalt übereinstimmen.                                                                                                                                                                                                                                              |   1   |
| 7.3.2 | Überprüfen Sie, dass Output-Filter Antworten erkennen und blockieren, die Systemprompt-Inhalte offenlegen, einschließlich wörtlicher Wiedergabe sowie semantisch äquivalenter Paraphrasen von Anweisungen, Rollenbezeichnungen oder Richtlinienvorgaben.                                                                                                                                                                      |   2   |
| 7.3.3 | Stellen Sie sicher, dass LLM-Client-Anwendungen verhindern, dass von Modellen generierte Ausgaben automatische ausgehende Anfragen auslösen (z. B. automatisch gerenderte Bilder, Iframes oder Link-Prefetching) an von Angreifern kontrollierte Endpunkte, zum Beispiel indem das automatische Laden externer Ressourcen deaktiviert wird oder indem es auf eine explizit erlaubte Liste zulässiger Origins beschränkt wird. |   2   |
| 7.3.4 | Verifizieren, dass generierte Ausgaben auf statistische steganografische verdeckte Kanäle analysiert werden (z.B. voreingenommene Token-Wahl-Muster oder Auffälligkeiten in der Ausgabeverteilung), die versteckte Daten über den zulässigen Ausgabebereich des Modells hinweg codieren könnten, und dass Erkennungen zur Überprüfung markiert werden.                                                                        |   3   |
| 7.3.5 | Prüfen Sie, dass modelgenerierte Ausgaben auf Encoding- und Representations-Smelgling-Artefakte (z.B. unsichtbare Unicode- oder Steuerzeichen, Homoglyph-Substitutionen, gemischt gerichteter Text) durchsucht werden, bevor sie an Aufrufer zurückgegeben oder an nachgelagerte Systeme weitergegeben werden, und dass Erkennungen zur Ablehnung oder zum Bereinigen führen.                                                 |   3   |

---

## C7.4 Erklärbarkeit & Transparenz

Stellen Sie sicher, dass der Nutzer versteht, warum eine Entscheidung getroffen wurde.

|   #   | Beschreibung                                                                                                                                                                                          | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.4.1 | Prüfen Sie, dass die dem Benutzer bereitgestellten Erklärungen bereinigt sind, um Systemaufforderungen oder Backend-Daten zu entfernen.                                                               |   1   |
| 7.4.2 | Stellen Sie sicher, dass technische Belege für die Entscheidung des Modells, z. B. Artefakte zur Modellinterpretierbarkeit (wie Aufmerksamkeitskarten, Feature-Zuschreibungen), protokolliert werden. |   3   |

---

## C7.5 Schutzmaßnahmen für generative Medien

Stellen Sie eine kryptografische Herkunftsbeurkundung für synthetische Medien bereit, damit nachgelagerte Verbraucher KI-generierte Inhalte von authentischen Inhalten unterscheiden können.

|   #   | Beschreibung                                                                                                                                                                     | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.5.1 | Stellen Sie sicher, dass alle generierten Medien über ein unsichtbares Wasserzeichen oder eine kryptografische Signatur verfügen, um nachzuweisen, dass sie KI-generiert wurden. |   3   |

---

## C7.6 Quellenzuordnung & Zitationsintegrität

Stellen Sie sicher, dass RAG-basierte Ausgaben auf ihre Quellendokumente zurückverfolgbar sind und dass zitierte Aussagen nachweislich durch abgerufenes Inhaltmaterial gestützt werden.

|   #   | Beschreibung                                                                                                                                                                                       | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.6.1 | Stellen Sie sicher, dass Antworten, die mithilfe von Retrieval-Augmented Generation (RAG) generiert werden, eine Quellenangabe zu den Quellendokumenten enthalten, auf denen die Antwort basierte. |   1   |
| 7.6.2 | Stellen Sie sicher, dass RAG-Zuschreibungen aus Abrufmetadaten abgeleitet werden und nicht vom Modell generiert sind, sodass die Herkunft (Provenienz) nicht erfunden werden kann.                 |   1   |
| 7.6.3 | Stellen Sie sicher, dass jede zitierte Behauptung in einer RAG-gestützten Antwort auf einen bestimmten abgerufenen Abschnitt zurückverfolgt werden kann.                                           |   3   |
| 7.6.4 | Überprüfen Sie, dass das System Antworten erkennt und kennzeichnet, bei denen Behauptungen nicht durch irgendeinen abgerufenen Inhalt gestützt werden, bevor die Antwort bereitgestellt wird.      |   3   |
| 7.6.5 | Überprüfen Sie, dass RAG-Antworten, bei denen nicht unterstützte Behauptungen erkannt werden, blockiert oder redigiert werden, bevor sie dem Benutzer bereitgestellt werden.                       |   3   |

---

## Referenzen

* [OWASP LLM05:2025 Improper Output Handling](https://genai.owasp.org/llmrisk/llm052025-improper-output-handling/)
* [OWASP LLM06:2025 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)

