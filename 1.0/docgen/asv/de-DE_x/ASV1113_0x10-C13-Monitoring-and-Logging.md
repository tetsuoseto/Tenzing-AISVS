# C13 Monitoring, Logging & Anomalieerkennung

## Kontrollziel

Dieser Abschnitt enthält Anforderungen für die Bereitstellung einer Echtzeit- und forensischen Transparenz darüber, was das Modell und andere KI-Komponenten sehen, tun und zurückgeben, damit Bedrohungen erkannt, priorisiert (triagiert) und daraus gelernt werden kann.

## C13.1 Anfrage- und Antwortprotokollierung

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                  | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 13.1.1 | Stellen Sie sicher, dass AI-Interaktionen mit sicherheitsrelevanten Metadaten protokolliert werden (z. B. Zeitstempel, Benutzer-ID, Sitzungs-ID, Modellversion, Tokenanzahl, Eingabe-Hash, Version des Systemprompts, Konfidenzscore, Ergebnis des Sicherheitsfilters und Sicherheitsfilterentscheidungen), ohne standardmäßig Prompt- oder Antwortinhalte zu protokollieren. |   1   |
| 13.1.2 | Stellen Sie sicher, dass Protokolle in sicheren, zugangskontrollierten Repositories gespeichert werden, mit geeigneten Aufbewahrungsrichtlinien und Backup-Verfahren.                                                                                                                                                                                                         |   1   |
| 13.1.3 | Stellen Sie sicher, dass Log-Speichersysteme eine Verschlüsselung im Ruhezustand und während der Übertragung implementieren, um sensible Informationen zu schützen, die in Logs enthalten sind.                                                                                                                                                                               |   1   |
| 13.1.4 | Stellen Sie sicher, dass sensible Daten in Prompts und Ausgaben automatisch bereinigt oder maskiert werden, bevor sie protokolliert werden, mit konfigurierbaren Bereinigungsregeln für personenbezogene Daten (PII), Zugangsdaten und vertrauliche Informationen.                                                                                                            |   1   |
| 13.1.5 | Stellen Sie sicher, dass Richtlinienentscheidungen und sicherheitsrelevante Filtermaßnahmen mit ausreichenden Details protokolliert werden, um Audits und das Debugging von Content-Moderationssystemen zu ermöglichen.                                                                                                                                                       |   2   |
| 13.1.6 | Stellen Sie sicher, dass die Protokollintegrität durch z. B. kryptografische Signaturen oder schreibgeschützten Speicher geschützt wird.                                                                                                                                                                                                                                      |   2   |
| 13.1.7 | Stellen Sie sicher, dass Protokolleinträge für KI-Inferenzereignisse ein strukturiertes, interoperables Schema erfassen, das mindestens Modellkennung, Token-Nutzung (Eingabe und Ausgabe), Anbietername und Vorgangstyp umfasst, um eine konsistente KI-Beobachtbarkeit über Tools und Plattformen hinweg zu ermöglichen.                                                    |   2   |
| 13.1.8 | Stellen Sie sicher, dass der vollständige Prompt- und Antwortinhalt nur dann protokolliert wird, wenn ein sicherheitsrelevantes Ereignis erkannt wird (z.B. Auslösung eines Sicherheitsfilters, Prompt-Injection-Erkennung, Anomalie-Flag), oder wenn dies durch eine ausdrückliche Einwilligung des Benutzers und eine dokumentierte Rechtsgrundlage erforderlich ist.       |   2   |

---

## C13.2 Missbrauchserkennung und Benachrichtigung

>Anmerkung zum Geltungsbereich: Die Überwachung unter C13.2.10 sollte Zugriffs-Muster für Metadaten auf Token-Ebene einschließen (z. B. hochfrequente Logprob-API-Anfragen, systematische Aufzählung von Token-Wahrscheinlichkeiten) als Indikator für Datenexfiltration über Timing- oder Token-Wahrscheinlichkeits-Side-Channels. Auffällige Logprob-Zugriffsmuster fallen unter den Indikator „strukturierte nicht-menschliche Abfrage-Muster“. C4.2.8 umfasst Telemetrie auf Accelerator-Ebene für Side-Channels; C13.2.4 umfasst Verhaltens-Anomalieerkennung für systematisches Sondieren.

|    #    | Beschreibung                                                                                                                                                                                                                                                                                                          | Ebene |
| :-----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 13.2.1  | Überprüfen Sie, dass das System bekannte Jailbreak-Muster, Prompt-Injection-Versuche und adversariale Eingaben anhand einer signaturbasierten Erkennung erkennt und meldet.                                                                                                                                           |   1   |
| 13.2.2  | Stellen Sie sicher, dass das System sich in vorhandene Security Information and Event Management (SIEM)-Plattformen integriert, indem es standardisierte Protokolle und Log-Formate verwendet.                                                                                                                        |   1   |
| 13.2.3  | Stellen Sie sicher, dass angereicherte Sicherheitsereignisse KI-spezifischen Kontext enthalten, wie z.B. Modellkennungen, Konfidenzwerte und Entscheidungen zu Sicherheitsfiltern.                                                                                                                                    |   2   |
| 13.2.4  | Stellen Sie sicher, dass die Erkennung von Verhaltensanomalien ungewöhnliche Gesprächsmuster, übermäßige Wiederholungsversuche oder systematisches Sondierungsverhalten identifiziert.                                                                                                                                |   2   |
| 13.2.5  | Stellen Sie sicher, dass Mechanismen für die Echtzeit-Benachrichtigung die Sicherheitsteams benachrichtigen, wenn potenzielle Richtlinienverstöße oder Angriffversuche erkannt werden.                                                                                                                                |   2   |
| 13.2.6  | Stellen Sie sicher, dass benutzerdefinierte Regeln enthalten sind, um AI-spezifische Bedrohungsmuster zu erkennen, einschließlich koordinierter Jailbreak-Versuche, Prompt-Injection-Kampagnen und Modellextraktionsangriffen.                                                                                        |   2   |
| 13.2.7  | Überprüfen Sie, dass automatisierte Workflows zur Reaktion auf Sicherheitsvorfälle kompromittierte Modelle isolieren und bösartige Benutzer blockieren können.                                                                                                                                                        |   3   |
| 13.2.8  | Verifizieren, dass die Analyse von Gesprächstrajektorien auf Sitzungs-Ebene mehrturnige Jailbreak-Muster erkennt, bei denen in einzelnen Beiträgen für sich genommen keine eindeutig bösartige Absicht erkennbar ist, aber in der Gesamtheit des Gesprächs Angriffshinweise auftreten.                                |   3   |
| 13.2.9  | Überprüfen Sie, dass die tokenbasierte Verbrauchsmessung pro Benutzer und pro Sitzung einen Alarm auslöst, wenn der Verbrauch die definierten Schwellenwerte überschreitet.                                                                                                                                           |   2   |
| 13.2.10 | Verifizieren Sie, dass der LLM-API-Verkehr auf Indikatoren für verdeckte Kanäle überwacht wird, einschließlich Base64-kodierter Nutzlasten, strukturierter nicht-menschlicher Abfragemuster und Kommunikationssignaturen, die mit Malware-Befehl-und-Steuerungs-Aktivitäten übereinstimmen, die LLM-Endpunkte nutzen. |   3   |

---

## C13.3 Erkennung von Modell-, Daten- und Leistungsdrift

Überwachen und Erkennen von Drift und Degradation über Modellausgaben, Eingabeverteilungen und Datenschemas hinweg, um Qualitätsregressionen und sicherheitsrelevante Verhaltensänderungen zu identifizieren.

|    #    | Beschreibung                                                                                                                                                                                                                                              | Ebene |
| :-----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 13.3.1  | Stellen Sie sicher, dass Modellleistungsmetriken (Genauigkeit, Präzision, Recall, F1-Score, Konfidenzwerte, Latenz und Fehlerraten) fortlaufend über Modellversionen und Zeiträume hinweg überwacht und gegen dokumentierte Basiswerte verglichen werden. |   1   |
| 13.3.2  | Überprüfen Sie, dass die Basisleistungsprofile formal dokumentiert und versionkontrolliert sind und in einem definierten Rhythmus oder nach jeder Änderung eines Modells oder einer Datenpipeline überprüft werden.                                       |   2   |
| 13.3.3  | Stellen Sie sicher, dass die automatische Benachrichtigung ausgelöst wird, wenn Leistungsmetriken vordefinierte Verschlechterungsschwellen überschreiten oder sich deutlich von den Baselines unterscheiden.                                              |   2   |
| 13.3.4  | Stellen Sie sicher, dass Halluzinations-Erkennungsmonitore Instanzen identifizieren und markieren, wenn Modellausgaben faktisch falsche, inkonsistente oder erfundene Informationen enthalten.                                                            |   2   |
| 13.3.5  | Überprüfen Sie, dass Data-Drift-Erkennung die Änderungen der Eingabeverteilung überwacht, die die Modellleistung beeinträchtigen können, und nutzen Sie statistisch validierte Methoden, die für den jeweiligen Datentyp geeignet sind.                   |   1   |
| 13.3.6  | Stellen Sie sicher, dass Schema-Drift in eingehenden Daten (unerwartete Feld-Ergänzungen, -Entfernungen, Typänderungen oder Formatabweichungen) erkannt wird und eine Alarmierung auslöst.                                                                |   2   |
| 13.3.7  | Stellen Sie sicher, dass die Erkennung von Concept Drift Änderungen in der Beziehung zwischen Eingaben und erwarteten Ausgaben identifiziert.                                                                                                             |   2   |
| 13.3.8  | Verifizieren Sie, dass die Analyse der Abbau-Ursachen die Leistungseinbrüche mit Datenänderungen, Infrastrukturproblemen oder externen Faktoren in Zusammenhang bringt.                                                                                   |   3   |
| 13.3.9  | Stellen Sie sicher, dass plötzliche unerklärliche Verhaltensänderungen von allmählichem erwarteten betrieblichem Drift unterschieden werden, und definieren Sie einen Security-Eskalationspfad für unerklärlichen plötzlichen Drift.                      |   3   |
| 13.3.10 | Stellen Sie sicher, dass Performance-Degradationsalarme einen definierten Remediations-Workflow auslösen (z. B. manuelle Prüfung, Retraining oder Austausch).                                                                                             |   2   |
| 13.3.11 | Stellen Sie sicher, dass Halluzinationsraten als kontinuierliche Zeitreihen-Metriken erfasst werden, um Trendanalysen und die Erkennung einer anhaltenden Modellverschlechterung zu ermöglichen.                                                          |   2   |

---

## C13.4 Leistungs- und Verhaltens-Telemetrie

|   #    | Beschreibung                                                                                                                                                                                                              | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 13.4.1 | Stellen Sie sicher, dass Betriebsmetriken einschließlich Request-Latenz, Token-Verbrauch, Speicherverbrauch und Durchsatz kontinuierlich erfasst und überwacht werden.                                                    |   1   |
| 13.4.2 | Stellen Sie sicher, dass Erfolgs- und Misserfolgsraten mithilfe einer Kategorisierung von Fehlerarten und deren Ursachen im Ursprung verfolgt werden.                                                                     |   1   |
| 13.4.3 | Stellen Sie sicher, dass die Überwachung der Ressourcennutzung die Überwachung der GPU/CPU-Auslastung, des Speicherkonsums und der Speicheranforderungen umfasst, mit Alarmierung bei Überschreitung von Schwellenwerten. |   2   |
| 13.4.4 | Stellen Sie sicher, dass die Token-Nutzung auf granularen Zuweisungsebenen erfasst wird, einschließlich pro Benutzer, pro Sitzung, pro Feature-Endpunkt und pro Team oder Workspace.                                      |   2   |
| 13.4.5 | Überprüfen Sie, dass Anomalien im Verhältnis von Output-zu-Input-Token erkannt und gemeldet werden.                                                                                                                       |   2   |

---

## C13.5 KI-Notfallplanung & Durchführung

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                    | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 13.5.1 | Stellen Sie sicher, dass Notfallpläne zur Incident Response speziell Sicherheitsereignisse im Zusammenhang mit KI abdecken, einschließlich Modellkompromittierung, Data Poisoning, adversarialen Angriffen, Model Inversion, Prompt-Injection-Kampagnen und Model Extraction, jeweils mit konkreten Eindämmungs- und Untersuchungsmaßnahmen für jedes Szenario. |   1   |
| 13.5.2 | Stellen Sie sicher, dass Incident-Response-Teams Zugriff auf forensische KI-spezifische Tools und Fachwissen haben, um das Modellverhalten und Angriffsvektoren zu untersuchen.                                                                                                                                                                                 |   2   |
| 13.5.3 | Stellen Sie sicher, dass die Post-Incident-Analyse Überlegungen zum Modell-Neutraining, Aktualisierungen der Sicherheitsfilter und die Integration der gewonnenen Erkenntnisse in Sicherheitskontrollen umfasst.                                                                                                                                                |   3   |

---

## C13.6 DAG-Visualisierung & Workflowsicherheit

Schützen Sie Workflow-Visualisierungssysteme vor Informationsleckage- und Manipulationsangriffen.

|   #    | Beschreibung                                                                                                                                                                       | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 13.6.1 | Stellen Sie sicher, dass die DAG-Visualisierungsdaten bereinigt werden, um sensible Informationen vor Speicherung oder Übertragung zu entfernen.                                   |   1   |
| 13.6.2 | Stellen Sie sicher, dass Workflow-Visualisierungszugriffskontrollen gewährleisten, dass nur autorisierte Benutzer Agent-Entscheidungspfade und Begründungsspuren einsehen können.  |   1   |
| 13.6.3 | Überprüfen Sie, dass die DAG-Datenintegrität durch kryptografische Signaturen und manipulationssichere Speichermethoden geschützt wird.                                            |   2   |
| 13.6.4 | Stellen Sie sicher, dass Workflows-Visualisierungssysteme eine Eingabevalidierung implementieren, um Injektionsangriffe durch konstruierte Knoten- oder Kantendaten zu verhindern. |   2   |
| 13.6.5 | Überprüfen Sie, dass Echtzeit-DAG-Updates rate-limitiert und validiert werden, um Denial-of-Service-Angriffe auf Visualisierungssysteme zu verhindern.                             |   3   |

---

## C13.7 Proaktives Security-Verhaltensmonitoring

Erkennung und Prävention von Sicherheitsbedrohungen durch Analyse proaktiven Agentenverhaltens.

>Geltungsbereich: C13.7 befasst sich mit der Überwachung und Protokollierung proaktiver Agentenverhalten. 13.7.4 verlangt eine Abdeckung der Prüfbarkeit (Audit-Trail) für Genehmigungsereignisse bei sicherheitskritischen Aktionen. Die Anforderung, vor der Ausführung solcher Aktionen eine Genehmigung einzuholen, wird durch C9.2 (Runtime-Ausführungsfreigabe) und C14.2 (Aufsichtsrichtlinie) geregelt. Die Erfüllung von 13.7.4 erfordert den Nachweis, dass Genehmigungsereignisse mit ausreichender Detailtiefe protokolliert werden — nicht nur, dass Genehmigungen erfolgen.

|   #    | Beschreibung                                                                                                                                                                                                                                 | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 13.7.1 | Stellen Sie sicher, dass proaktive Agentenverhalten sicherheitsgeprüft ist, bevor es mit integrierter Risikobewertung ausgeführt wird.                                                                                                       |   1   |
| 13.7.2 | Stellen Sie sicher, dass autonome Initiativen-Trigger die Sicherheitskontextbewertung und die Bewertung der Bedrohungslandschaft umfassen.                                                                                                   |   2   |
| 13.7.3 | Überprüfen Sie, dass proaktive Verhaltensmuster auf mögliche Sicherheitsauswirkungen und unbeabsichtigte Folgen analysiert werden.                                                                                                           |   2   |
| 13.7.4 | Stellen Sie sicher, dass Prüfprotokolle die vollständige Genehmigungskette für sicherheitskritische proaktive Aktionen erfassen, einschließlich Identität der genehmigenden Person, Zeitstempel, Aktionsparameter und Entscheidungsergebnis. |   3   |
| 13.7.5 | Stellen Sie sicher, dass die Erkennung von Verhaltensauffälligkeiten Abweichungen in proaktiven Agentenmuster identifiziert, die auf eine Kompromittierung hindeuten können.                                                                 |   3   |

---

## References

* [OWASP Top 10 for LLM Applications 2025](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
* [MITRE ATLAS - Adversarial Threat Landscape for AI Systems](https://atlas.mitre.org/)
* [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf)
* [NIST AI 100-1 - Artificial Intelligence Risk Management Framework](https://doi.org/10.6028/NIST.AI.100-1)

