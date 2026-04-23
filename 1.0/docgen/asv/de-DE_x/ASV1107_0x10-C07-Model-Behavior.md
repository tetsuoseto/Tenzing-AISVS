# C7 Modelverhalten, Output-Steuerung & Sicherheitsabsicherung

## Kontrollziel

Diese Kontrollkategorie stellt sicher, dass Modell-Ausgaben technisch eingeschränkt, validiert und überwacht werden, sodass unsichere, fehlerhafte oder risikoreiche Antworten nicht zu Nutzern oder nachgelagerten Systemen gelangen können. Das Kapitel behandelt spezifische Bedenken hinsichtlich der Ausgabebehandlung für KI und vermeidet bewusst das Duplizieren von Kontrollen, die bereits in OWASP ASVS v5 oder in anderen AISVS-Kapiteln vorhanden sind.

Allgemeine Anwendungs-Ausgabe-Steuerungen wie Ausgabe-Codierung und -Escaping, parametrisierte Abfragen, sichere Deserialisierung, Anti-Automatisierung, Protokollierung von Sicherheitsereignissen sowie Fehlerbehandlung werden durch ASVS v5 Kapitel V1, V2, V14 und V16 adressiert.

---

## C7.1 Ausgabeformatdurchsetzung

Stellen Sie sicher, dass das Modell Daten so ausgibt, dass das Eindringen (Injection) erschwert wird.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                 | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.1.1 | Stellen Sie sicher, dass die Anwendung alle Modell-Ausgaben anhand eines strengen Schemas (wie JSON Schema) validiert und jede Ausgabe ablehnt, die nicht übereinstimmt.                                                                                                                                                                                                     |   1   |
| 7.1.2 | Überprüfen Sie, dass das System entweder "Stop-Sequenzen" oder Token-Limits verwendet, um die Generierung strikt zu beenden, bevor es zu Pufferüberläufen kommen oder unbeabsichtigte Befehle ausgeführt werden können.                                                                                                                                                      |   1   |
| 7.1.3 | Stellen Sie sicher, dass Modell-Ausgaben, die über eine Vertrauensgrenze in nachgelagerte Interpretersysteme gelangen (z.B. Datenbanken, Shells, Deserialisierer, Template-Engines, Browser), als nicht vertrauenswürdige Eingaben behandelt und mithilfe der entsprechenden sicheren APIs verarbeitet werden, wie in OWASP ASVS v5 in den Kapiteln V1.2 und V1.5 definiert. |   1   |

---

## C7.2 Erkennung und Eindämmung von Halluzinationen

Erkennen, wenn das Modell potenziell ungenaue oder erfundene Inhalte erzeugt, und verhindern, dass unzuverlässige Ausgaben die Nutzer oder nachgelagerte Systeme erreichen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                        | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.2.1 | Überprüfen Sie, dass das System die Zuverlässigkeit generierter Antworten mithilfe einer Konfidenz- oder Unsicherheitsschätzmethode bewertet (z.B. Konfidenzbewertung, verifizierungsbasierte Suche oder Schätzung der Modellunsicherheit).                                                                                                                                                                                                         |   1   |
| 7.2.2 | Überprüfen Sie, dass die Anwendung automatisch Antworten blockiert oder auf eine Fallback-Nachricht umschaltet, wenn der Konfidenzwert unter einen definierten Schwellenwert fällt.                                                                                                                                                                                                                                                                 |   2   |
| 7.2.3 | Stellen Sie sicher, dass Halluzinationsereignisse (Antworten mit geringer Konfidenz) mit Eingabe-/Ausgabe-Metadaten zur Analyse protokolliert werden.                                                                                                                                                                                                                                                                                               |   2   |
| 7.2.4 | Stellen Sie sicher, dass das System für Antworten, die gemäß Richtlinie als „High-Risk“ oder „High-Impact“ eingestuft werden, einen zusätzlichen Verifizierungsschritt über einen unabhängigen Mechanismus durchführt, z. B. eine retrieval-basierte Absicherung gegen autoritative Quellen, eine deterministische regelbasierte Validierung, eine toolbasierte Faktprüfung oder eine Konsensüberprüfung durch ein separat bereitgestelltes Modell. |   3   |
| 7.2.5 | Stellen Sie sicher, dass das System die Historie der Tool- und Funktionsaufrufe innerhalb einer Request-Kette nachverfolgt und hochgradig wahrscheinliche faktische Behauptungen kennzeichnet, die nicht von einer relevanten Nutzung von Verifikations-Tools eingeleitet wurden, als praktisches Signal zur Erkennung von Halluzinationen unabhängig von der Konfidenzbewertung.                                                                   |   2   |

---

## C7.3 Ausgabe-Sicherheits- & Datenschutzfilterung

Technische Kontrollen zum Erkennen und Bereinigen von schädlichem Inhalt, bevor er dem Nutzer angezeigt wird.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                           | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.3.1 | Verifizieren Sie, dass automatische Klassifizierer jede Antwort scannen und Inhalte blockieren, die mit den Kategorien Hass, Belästigung oder sexueller Gewalt übereinstimmen.                                                                                                                                                                                                                                         |   1   |
| 7.3.2 | Stellen Sie sicher, dass Ausgabefilter Antworten erkennen und blockieren, die wortgetreue Abschnitte des Systemprompts reproduzieren.                                                                                                                                                                                                                                                                                  |   2   |
| 7.3.3 | Überprüfen Sie, dass LLM-Clientanwendungen verhindern, dass vom Modell generierte Ausgaben automatische ausgehende Anfragen auslösen (z. B. automatisch gerenderte Bilder, iframes oder Link-Prefetching) an von Angreifern gesteuerte Endpunkte, zum Beispiel indem das automatische Laden externer Ressourcen deaktiviert wird oder es auf explizit erlaubte (allowlist) Origins beschränkt wird, sofern angemessen. |   2   |
| 7.3.4 | Stellen Sie sicher, dass die generierten Ausgaben auf statistische steganografische geheime Kanäle untersucht werden (z.B. verzerrte Token-Auswahlmuster oder Anomalien in der Ausgabeverteilung), die dazu dienen könnten, versteckte Daten über den gültigen Ausgabebereich des Modells zu kodieren, und dass Erkennungen zur Überprüfung markiert werden.                                                           |   3   |

---

## C7.4 Erklärbarkeit & Transparenz

Stellen Sie sicher, dass der Nutzer versteht, warum eine Entscheidung getroffen wurde.

|   #   | Beschreibung                                                                                                                                                                                                 | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 7.4.1 | Stellen Sie sicher, dass die dem Benutzer bereitgestellten Erklärungen so bereinigt sind, dass System-Prompts oder Backend-Daten entfernt werden.                                                            |   1   |
| 7.4.2 | Stellen Sie sicher, dass technische Nachweise für die Entscheidung des Modells protokolliert werden, wie z. B. Artefakte zur Interpretierbarkeit des Modells (z. B. Attention-Maps, Feature-Zuschreibungen). |   3   |

---

## C7.5 Schutzmaßnahmen für generatives Medienwesen

Stellen Sie eine kryptografische Herkunftsnachverfolgbarkeit für synthetische Medien bereit, damit nachgelagerte Konsumenten KI-generierten Inhalt von authentischem Inhalt unterscheiden können.

|   #   | Beschreibung                                                                                                                                                               | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.5.1 | Verifizieren Sie, dass alle generierten Medien eine unsichtbare Wasserzeichen- oder kryptografische Signatur enthalten, um nachzuweisen, dass sie von KI generiert wurden. |   3   |

---

## C7.6 Quellenzuordnung & Zitierintegrität

Stellen Sie sicher, dass RAG-gestützte Ergebnisse auf ihre Quellendokumente zurückverfolgbar sind und dass die zitierten Aussagen nachweislich durch den abgerufenen Inhalt unterstützt werden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                              | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 7.6.1 | Verifizieren Sie, dass Antworten, die mithilfe von Retrieval-Augmented Generation (RAG) generiert werden, eine Quellenangabe zu den Quelldokumenten enthalten, die die Antwort untermauert haben.                                                                                                                         |   1   |
| 7.6.2 | Verifizieren Sie, dass jede in einer RAG-gestützten Antwort angeführte Aussage auf einen bestimmten abgerufenen Ausschnitt zurückverfolgt werden kann, und dass das System Antworten erkennt und kennzeichnet, bei denen Aussagen durch keinen abgerufenen Inhalt gestützt werden, bevor die Antwort bereitgestellt wird. |   3   |
| 7.6.3 | Verifizieren Sie, dass RAG-Attributionen aus Abrufmetadaten abgeleitet werden und nicht vom Modell generiert werden, sodass die Herkunft nicht frei erfunden werden kann.                                                                                                                                                 |   1   |

---

## References

* [OWASP LLM05:2025 Improper Output Handling](https://genai.owasp.org/llmrisk/llm052025-improper-output-handling/)
* [OWASP LLM06:2025 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)

