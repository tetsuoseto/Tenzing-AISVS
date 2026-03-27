# C2 Benutzereingabevalidierung

## Kontrollziel

Robuste Validierung von Benutzereingaben ist eine erste Verteidigungslinie gegen einige der schädlichsten Angriffe auf KI-Systeme. Prompt-Injektion-Angriffe können Systemanweisungen außer Kraft setzen, sensible Daten preisgeben oder das Modell auf unerlaubtes Verhalten lenken. Sofern keine speziellen Filter und andere Validierungen vorhanden sind, zeigen Untersuchungen, dass Jailbreaks, die Kontextfenster ausnutzen, weiterhin wirksam sein werden.

---

## C2.1 Schutz gegen Prompt-Injektion

Prompt Injection ist eines der größten Risiken für KI-Systeme. Abwehrmaßnahmen gegen diese Taktik setzen eine Kombination aus Musterfiltern, Datenklassifikatoren und Durchsetzung der Anweisunghierarchie ein.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 2.1.1 | Stellen Sie sicher, dass jegliche externe oder abgeleitete Eingabe, die das Verhalten steuern könnte, einschließlich Benutzeraufforderungen, RAG-Ergebnissen, Tool-Integrationen oder MCP-Ausgaben, Agent-zu-Agent-Nachrichten, API- oder Webhook-Antworten, Konfigurations- oder Richtliniendateien, Speicherlesungen und Speicherbeschreibungen, als nicht vertrauenswürdig behandelt wird, durch Anführungszeichen oder Markierungen und Entfernung aktiver Inhalte unschädlich gemacht wird und vor der Verkettung in Eingabeaufforderungen oder der Ausführung von Aktionen durch ein gepflegtes Regelwerk oder einen Dienst zur Erkennung von Prompt-Injektionen geprüft wird. |   1   |  D/V  |
| 2.1.2 | Überprüfen Sie, dass das System eine Anweisungshierarchie durchsetzt, in der System- und Entwicklernachrichten Benutzeranweisungen und andere nicht vertrauenswürdige Eingaben übersteuern, auch nach der Verarbeitung von Benutzeranweisungen.                                                                                                                                                                                                                                                                                                                                                                                                                                      |   1   |  D/V  |
| 2.1.3 | Stellen Sie sicher, dass Aufforderungen, die aus Inhalten Dritter stammen (Webseiten, PDFs, E-Mails), isoliert bereinigt werden (zum Beispiel durch Entfernen von anweisungsähnlichen Direktiven und Neutralisieren von HTML-, Markdown- und Skriptinhalten), bevor sie in die Hauptaufforderung eingearbeitet werden.                                                                                                                                                                                                                                                                                                                                                               |   2   |   D   |

---

## C2.2 Widerstandsfähigkeit gegen adversariale Beispiele

KI-Modelle sind anfällig für subtile Eingabeperturbationen, die Menschen oft übersehen, aber von Modellen häufig falsch klassifiziert werden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                    | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 2.2.1 | Verifizieren Sie, dass grundlegende Schritte der Eingabenormalisierung (Unicode NFC, Homoglyphen-Mapping, Trimmen von Leerzeichen, Entfernung von Steuer- und unsichtbaren Unicode-Zeichen) vor der Tokenisierung oder Einbettung sowie vor dem Parsen in Werkzeug- oder MCP-Argumente durchgeführt werden.                                                                     |   1   |   D   |
| 2.2.2 | Stellen Sie sicher, dass verdächtige feindliche Eingaben isoliert und mit Payload-Ausschnitten sowie Trace-Metadaten (Quelle, Werkzeug oder MCP-Server, Agenten-ID, Sitzung) protokolliert werden.                                                                                                                                                                              |   1   |   V   |
| 2.2.3 | Stellen Sie sicher, dass die statistische Anomalieerkennung Eingaben mit ungewöhnlich hoher Editierdistanz zu sprachlichen Normen oder abnormen Einbettungsdistanzen erkennt und dass markierte Eingaben vor der Verkettung in Eingabeaufforderungen oder der Ausführung von Aktionen kontrolliert werden.                                                                      |   2   |  D/V  |
| 2.2.4 | Überprüfen Sie, ob die Inferenz-Pipeline adversarial-trainierte Modellvarianten oder Verteidigungsschichten (z. B. Randomisierung, defensive Distillation, Abstimmungsprüfungen) für risikoreiche Endpunkte unterstützt.                                                                                                                                                        |   2   |   D   |
| 2.2.5 | Stellen Sie sicher, dass Codierungs- und Darstellungsschmuggel sowohl bei Eingaben als auch bei Ausgaben (z. B. unsichtbare Unicode-/Steuerzeichen, Homoglyphenvertauschungen oder Mischschriftrichtungen) erkannt und abgewehrt werden. Zugelassene Gegenmaßnahmen umfassen Kanonisierung, strenge Schemaüberprüfung, richtlinienbasierte Ablehnung oder explizite Markierung. |   3   |  D/V  |

---

## C2.3 Eingabeaufforderungs-Zeichensatz

Die Einschränkung des Zeichensatzes von Benutzereingaben auf nur die für die Geschäftsanforderungen erforderlichen Zeichen kann dazu beitragen, verschiedene Arten von Angriffen zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                     | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 2.3.1 | Überprüfen Sie, ob das System eine Zeichensatzbeschränkung für Benutzereingaben implementiert, die nur Zeichen zulässt, die ausdrücklich für geschäftliche Zwecke erforderlich sind, unter Verwendung eines Allow-List-Ansatzes. |   1   |   D   |
| 2.3.2 | Überprüfen Sie, dass Eingaben, die Zeichen außerhalb des erlaubten Sets enthalten, abgelehnt und mit Trace-Metadaten (Quelle, Werkzeug oder MCP-Server, Agenten-ID, Sitzung) protokolliert werden.                               |   1   |  D/V  |

---

## C2.4 Schema-, Typ- und Längenvalidierung

KI-Angriffe mit fehlerhaften oder zu großen Eingaben können Parsing-Fehler, Prompt-Überlauf über verschiedene Felder hinweg und Ressourcenerschöpfung verursachen. Eine strenge Schema-Validierung ist zudem eine Voraussetzung für die Durchführung deterministischer Toolaufrufe.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                      | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 2.4.1 | Verifizieren Sie, dass jede API, jedes Tool oder jeder MCP-Endpunkt ein explizites Eingabeschema definiert (z. B. JSON Schema, Protocol Buffers oder ein multimodales Äquivalent), zusätzliche oder unbekannte Felder sowie implizite Typumwandlungen ablehnt und Eingaben serverseitig vor der Aufforderungszusammenstellung oder der Tool-Ausführung validiert. |   1   |   D   |
| 2.4.2 | Stellen Sie sicher, dass Eingaben, die die maximalen Token- oder Byte-Grenzen überschreiten, mit einer sicheren Fehlermeldung abgelehnt werden und niemals stillschweigend abgeschnitten werden.                                                                                                                                                                  |   1   |  D/V  |
| 2.4.3 | Stellen Sie sicher, dass Typprüfungen (z. B. numerische Bereiche, Enumerationswerte, MIME-Typen für Bilder/Audio) serverseitig durchgesetzt werden, einschließlich bei Werkzeug- oder MCP-Argumenten.                                                                                                                                                             |   1   |  D/V  |
| 2.4.4 | Stellen Sie sicher, dass semantische Validatoren in konstanter Zeit laufen und externe Netzwerkaufrufe vermeiden, um algorithmische DoS zu verhindern.                                                                                                                                                                                                            |   2   |   D   |
| 2.4.5 | Stellen Sie sicher, dass Validierungsfehler mit redigierten Nutzlastausschnitten und eindeutigen Fehlercodes protokolliert werden und Trace-Metadaten (Quelle, Werkzeug oder MCP-Server, Agent-ID, Sitzung) enthalten, um die Sicherheitsanalyse zu unterstützen.                                                                                                 |   3   |   V   |

---

## C2.5 Inhalts- und Richtlinienprüfung

Entwickler sollten in der Lage sein, syntaktisch gültige Eingabeaufforderungen zu erkennen, die nicht erlaubte Inhalte anfordern (wie z.B. richtlinienwidrige Anweisungen, schädliche Inhalte oder eingeschränktes Material), und dann verhindern, dass diese weiterverbreitet werden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                      | Ebene | Rolle |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 2.5.1 | Stellen Sie sicher, dass ein Inhaltsklassifikator jede Eingabe und Ausgabe hinsichtlich Gewalt, Selbstverletzung, Hass, sexuellen Inhalten und illegalen Anfragen bewertet, mit konfigurierbaren Schwellenwerten.                                                                                                                 |   1   |   D   |
| 2.5.2 | Stellen Sie sicher, dass Eingaben, die gegen Richtlinien verstoßen, abgelehnt werden, damit sie nicht an nachgelagerte Modelle oder Werkzeug-/MCP-Aufrufe weitergegeben werden.                                                                                                                                                   |   1   |  D/V  |
| 2.5.3 | Überprüfen Sie, ob das Screening benutzerspezifische Richtlinien (Alters- und regionale gesetzliche Beschränkungen) mittels attributbasierter Regeln einhält, die zur Anforderungszeit aufgelöst werden, einschließlich Agenten-Rollenattributen.                                                                                 |   2   |   D   |
| 2.5.4 | Stellen Sie sicher, dass die Screening-Protokolle Klassifikator-Vertrauenswerte und Richtlinienkategorie-Tags mit angewendeter Stufe (Pre-Prompt oder Post-Response) sowie Nachverfolgungsmetadaten (Quelle, Tool oder MCP-Server, Agenten-ID, Sitzung) für die SOC-Korrelation und zukünftige Red-Team-Wiederholungen enthalten. |   3   |   V   |

---

## C2.6 Eingangsratengrenze und Missbrauchsvermeidung

Entwickler sollten Missbrauch, Ressourcenerschöpfung und automatisierte Angriffe auf KI-Systeme verhindern, indem sie Eingaberaten begrenzen und anomale Nutzungsmuster erkennen.

|   #   | Beschreibung                                                                                                                                                                                                                                                 | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 2.6.1 | Überprüfen Sie, dass pro Benutzer, pro IP, pro API-Schlüssel, pro Agent und pro Sitzung/Aufgabe festgelegte Ratenbegrenzungen für alle Eingabe- und Tool-/MCP-Endpunkte durchgesetzt werden.                                                                 |   1   |  D/V  |
| 2.6.2 | Überprüfen Sie, ob Burst- und Dauer-Rate-Limits so eingestellt sind, dass DoS- und Brute-Force-Angriffe verhindert werden, und ob pro Aufgabe Budgets (zum Beispiel Tokens, Tool-/MCP-Aufrufe und Kosten) für Agenten-Planungsschleifen durchgesetzt werden. |   2   |  D/V  |
| 2.6.3 | Überprüfen Sie, ob anomale Nutzungsmuster (z. B. schnelle Anfragen, Eingabeflut, sich wiederholende fehlerhafte Tool-/MCP-Aufrufe oder rekursive Agentenschleifen) automatische Sperren oder Eskalationen auslösen.                                          |   2   |  D/V  |
| 2.6.4 | Überprüfen Sie, dass Missbrauchspräventionsprotokolle gespeichert und auf aufkommende Angriffsmuster mit Nachverfolgungs-Metadaten (Quelle, Werkzeug oder MCP-Server, Agenten-ID, Sitzung) überprüft werden.                                                 |   3   |   V   |

---

## C2.7 Multi-Modale Eingabevalidierung

KI-Systeme sollten eine robuste Validierung für nicht-textuelle Eingaben (Bilder, Audio, Dateien) beinhalten, um Injektion, Umgehung oder Ressourcenmissbrauch zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                           | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 2.7.1 | Stellen Sie sicher, dass alle nicht-textbasierten Eingaben (Bilder, Audio, Dateien) vor der Verarbeitung auf Typ, Größe und Format validiert werden und dass jeglicher extrahierter Text (Bild-zu-Text oder Sprache-zu-Text) sowie alle versteckten oder eingebetteten Anweisungen (Metadaten, Ebenen, Alternativtexte, Kommentare) gemäß Abschnitt 2.1.1 als nicht vertrauenswürdig behandelt werden. |   1   |   D   |
| 2.7.2 | Stellen Sie sicher, dass Dateien vor der Übernahme auf Malware und steganographische Nutzlasten gescannt werden und dass aktiver Inhalt (wie Skripte oder Makros) entfernt oder die Datei unter Quarantäne gestellt wird.                                                                                                                                                                              |   2   |  D/V  |
| 2.7.3 | Verifizieren Sie, dass Bild-/Audioeingaben auf adversarielle Störungen oder bekannte Angriffsmuster überprüft werden und dass Erkennungen eine Sperrung (Blockieren oder Einschränken von Funktionen) vor der Nutzung des Modells auslösen.                                                                                                                                                            |   2   |  D/V  |
| 2.7.4 | Überprüfen Sie, ob Validierungsfehler bei multimodalen Eingaben eine detaillierte Protokollierung auslösen, die alle Eingabemodalitäten, Validierungsergebnisse, Bedrohungsbewertungen und Trace-Metadaten (Quelle, Werkzeug oder MCP-Server, Agenten-ID, Sitzung falls zutreffend) enthält, und generieren Sie Warnmeldungen zur Untersuchung.                                                        |   3   |  D/V  |
| 2.7.5 | Überprüfen Sie, dass die Erkennung von Cross-Modal-Angriffen koordinierte Angriffe über mehrere Eingabetypen hinweg (z. B. steganografische Nutzlasten in Bildern kombiniert mit Prompt-Injektionen im Text) durch Korrelationsregeln und Alarmgenerierung identifiziert und dass bestätigte Erkennungen blockiert werden oder eine HITL-(Human-in-the-Loop)-Genehmigung erfordern.                    |   3   |  D/V  |

---

## C2.8 Echtzeit-Adaptive Bedrohungserkennung

Entwickler sollten fortschrittliche Bedrohungserkennungssysteme für KI einsetzen, die sich an neue Angriffsmuster anpassen und Echtzeitschutz bieten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                  | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 2.8.1 | Überprüfen Sie, dass das Musterabgleichen (z. B. kompilierte reguläre Ausdrücke) auf allen Eingaben und Ausgaben (einschließlich Tool-/MCP-Oberflächen) ausgeführt wird.                                                                                                                                      |   1   |  D/V  |
| 2.8.2 | Stellen Sie sicher, dass adaptive Erkennungsmodelle die Empfindlichkeit basierend auf kürzlicher Angriffstätigkeit anpassen, in Echtzeit mit neuen Mustern aktualisiert werden und risikoadaptive Reaktionen auslösen (zum Beispiel Tools deaktivieren, Kontext verkleinern oder HITL-Genehmigung verlangen). |   2   |  D/V  |
| 2.8.3 | Überprüfen Sie, ob die Erkennungsgenauigkeit durch kontextuelle Analyse der Benutzerhistorie, der Quelle und des Sitzungsverhaltens verbessert wird, einschließlich Trace-Metadaten (Quelle, Tool oder MCP-Server, Agenten-ID, Sitzung).                                                                      |   3   |  D/V  |
| 2.8.4 | Stellen Sie sicher, dass die Leistungskennzahlen der Erkennung (Erkennungsrate, Falsch-Positiv-Rate, Verarbeitungsverzögerung) kontinuierlich überwacht und optimiert werden, einschließlich der Zeit bis zur Sperrung und der Phase (vor dem Prompt/nach der Antwort).                                       |   3   |  D/V  |

## Literaturverzeichnis

* [OWASP LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
* [LLM Prompt Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html)
* [MITRE ATLAS : Adversarial Input Detection](https://atlas.mitre.org/mitigations/AML.M00150)
* [Mitigate jailbreaks and prompt injections](https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks)

