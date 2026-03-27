# C13 Überwachung, Protokollierung & Anomalieerkennung

## Kontrollziel

Dieser Abschnitt enthält Anforderungen für die Bereitstellung von Echtzeit- und forensischer Sichtbarkeit darüber, was das Modell und andere KI-Komponenten sehen, tun und zurückgeben, damit Bedrohungen erkannt, priorisiert und analysiert werden können.

## C13.1 Anforderungs- und Antwortprotokollierung

|   #    | Beschreibung                                                                                                                                                                                                                                                              | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 13.1.1 | Stellen Sie sicher, dass alle Benutzereingaben und Modellantworten mit den entsprechenden Metadaten (z. B. Zeitstempel, Benutzer-ID, Sitzungs-ID, Modellversion) protokolliert werden.                                                                                    |   1   |  D/V  |
| 13.1.2 | Stellen Sie sicher, dass Protokolle in sicheren, zugangskontrollierten Repositorien mit geeigneten Aufbewahrungsrichtlinien und Sicherungsverfahren gespeichert werden.                                                                                                   |   1   |  D/V  |
| 13.1.3 | Überprüfen Sie, ob Log-Speichersysteme eine Verschlüsselung im Ruhezustand und während der Übertragung implementieren, um sensible Informationen in Protokollen zu schützen.                                                                                              |   1   |  D/V  |
| 13.1.4 | Stellen Sie sicher, dass sensible Daten in Eingabeaufforderungen und Ausgaben vor der Protokollierung automatisch redigiert oder maskiert werden, mit konfigurierbaren Redigierungsregeln für personenbezogene Daten, Anmeldeinformationen und proprietäre Informationen. |   1   |  D/V  |
| 13.1.5 | Stellen Sie sicher, dass Richtlinienentscheidungen und Sicherheitsfiltermaßnahmen mit ausreichenden Details protokolliert werden, um eine Prüfung und Fehlersuche der Inhaltsmoderationssysteme zu ermöglichen.                                                           |   2   |  D/V  |
| 13.1.6 | Stellen Sie sicher, dass die Integrität der Protokolle durch z. B. kryptografische Signaturen oder schreibgeschützten Speicher geschützt ist.                                                                                                                             |   2   |  D/V  |

---

## C13.2 Missbrauchserkennung und Alarmierung

|   #    | Beschreibung                                                                                                                                                                                                                | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 13.2.1 | Überprüfen Sie, ob das System bekannte Jailbreak-Muster, Versuche zur Prompt-Injektion und adversariale Eingaben mithilfe einer signaturbasierten Erkennung erkennt und meldet.                                             |   1   |  D/V  |
| 13.2.2 | Überprüfen Sie, ob das System in bestehende Security Information and Event Management (SIEM)-Plattformen unter Verwendung standardisierter Protokollformate und -protokolle integriert ist.                                 |   1   |  D/V  |
| 13.2.3 | Überprüfen Sie, ob angereicherte Sicherheitsevents KI-spezifische Kontextinformationen wie Modellkennungen, Vertrauenswerte und Entscheidungen des Sicherheitsfilters enthalten.                                            |   2   |  D/V  |
| 13.2.4 | Überprüfen Sie, ob die Verhaltensanomalieerkennung ungewöhnliche Gesprächsmuster, übermäßige Wiederholungsversuche oder systematische Erkundungsverhalten erkennt.                                                          |   2   |  D/V  |
| 13.2.5 | Überprüfen Sie, dass Echtzeit-Benachrichtigungsmechanismen die Sicherheitsteams informieren, wenn potenzielle Richtlinienverletzungen oder Angriffsversuche erkannt werden.                                                 |   2   |  D/V  |
| 13.2.6 | Verifizieren Sie, dass benutzerdefinierte Regeln enthalten sind, um KI-spezifische Bedrohungsmuster zu erkennen, einschließlich koordinierter Jailbreak-Versuche, Prompt-Injektionskampagnen und Modellextraktionsangriffe. |   2   |  D/V  |
| 13.2.7 | Überprüfen Sie, dass automatisierte Arbeitsabläufe zur Vorfallreaktion kompromittierte Modelle isolieren, bösartige Benutzer blockieren und kritische Sicherheitsereignisse eskalieren können.                              |   3   |  D/V  |

---

## C13.3 Modell-Drift-Erkennung

|   #    | Beschreibung                                                                                                                                                                                           | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 13.3.1 | Überprüfen Sie, ob das System grundlegende Leistungskennzahlen wie Genauigkeit, Vertrauenswerte, Latenz und Fehlerraten über Modellversionen und Zeiträume hinweg verfolgt.                            |   1   |  D/V  |
| 13.3.2 | Überprüfen Sie, dass automatisierte Benachrichtigungen ausgelöst werden, wenn Leistungskennzahlen vordefinierte Verschlechterungsschwellen überschreiten oder signifikant von den Baselines abweichen. |   2   |  D/V  |
| 13.3.3 | Überprüfen Sie, ob die Überwachung der Halluzinationserkennung Instanzen erkennt und markiert, wenn Modelloutputs faktisch falsche, inkonsistente oder erfundene Informationen enthalten.              |   2   |  D/V  |

---

## C13.4 Leistungs- und Verhaltens-Telemetrie

|   #    | Beschreibung                                                                                                                                                                                                           | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 13.4.1 | Stellen Sie sicher, dass Betriebsmetriken wie Anforderungsverzögerung, Tokenverbrauch, Speichernutzung und Durchsatz kontinuierlich erfasst und überwacht werden.                                                      |   1   |  D/V  |
| 13.4.2 | Verifizieren Sie, dass Erfolgs- und Fehlerquoten mit Kategorisierung der Fehlertypen und deren Ursachen erfasst werden.                                                                                                |   1   |  D/V  |
| 13.4.3 | Stellen Sie sicher, dass die Überwachung der Ressourcenauslastung die Nutzung von GPU/CPU, den Speicherverbrauch und den Speicherbedarf umfasst, wobei bei Überschreitung von Schwellenwerten Alarme ausgelöst werden. |   2   |  D/V  |

---

## C13.5 Planung und Durchführung der KI-Zwischenfallreaktion

|   #    | Beschreibung                                                                                                                                                                                                          | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 13.5.1 | Überprüfen Sie, ob die Vorfallreaktionspläne speziell auf sicherheitsrelevante Ereignisse im Zusammenhang mit KI eingehen, einschließlich Modellkompromittierung, Datenvergiftung und adversarialen Angriffen.        |   1   |  D/V  |
| 13.5.2 | Überprüfen Sie, ob Incident-Response-Teams Zugang zu KI-spezifischen forensischen Tools und Fachwissen haben, um das Modellverhalten und Angriffsvektoren zu untersuchen.                                             |   2   |  D/V  |
| 13.5.3 | Überprüfen Sie, dass die Analyse nach dem Vorfall Überlegungen zur Modellneutrainierung, Aktualisierungen der Sicherheitsfilter und die Integration der gewonnenen Erkenntnisse in die Sicherheitskontrollen umfasst. |   3   |  D/V  |

---

## C13.6 Erkennung der Leistungsverschlechterung von KI

Überwachen und Erkennen von Verschlechterungen in der Leistung und Qualität von KI-Modellen im Zeitverlauf.

|   #    | Beschreibung                                                                                                                                                 | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 13.6.1 | Stellen Sie sicher, dass Modellgenauigkeit, Präzision, Recall und F1-Werte kontinuierlich überwacht und mit Basisliniengrenzwerten verglichen werden.        |   1   |  D/V  |
| 13.6.2 | Überprüfen Sie, ob die Datendrift-Erkennung Änderungen der Eingabeverteilung überwacht, die die Modellleistung beeinträchtigen können.                       |   1   |  D/V  |
| 13.6.3 | Überprüfen Sie, ob die Erkennung von Konzeptdrift Änderungen in der Beziehung zwischen Eingaben und erwarteten Ausgaben identifiziert.                       |   2   |  D/V  |
| 13.6.4 | Überprüfen Sie, dass Leistungsabfälle automatisierte Warnungen auslösen und Workflows zur Modell-Neuschulung oder -Ersetzung einleiten.                      |   2   |  D/V  |
| 13.6.5 | Überprüfen Sie, ob die Ursachenanalyse für Leistungseinbußen Leistungsabfälle mit Datenänderungen, Infrastrukturproblemen oder externen Faktoren korreliert. |   3   |   V   |

---

## C13.7 DAG-Visualisierung & Workflow-Sicherheit

Schützen Sie Workflow-Visualisierungssysteme vor Informationslecks und Manipulationsangriffen.

|   #    | Beschreibung                                                                                                                                                                                                   | Ebene | Rolle |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 13.7.1 | Verifizieren Sie, dass die DAG-Visualisierungsdaten bereinigt werden, um sensible Informationen vor der Speicherung oder Übertragung zu entfernen.                                                             |   1   |  D/V  |
| 13.7.2 | Überprüfen Sie, dass die Zugriffskontrollen für die Workflow-Visualisierung sicherstellen, dass nur autorisierte Benutzer die Entscheidungswege des Agenten und die Nachverfolgung der Gründe einsehen können. |   1   |  D/V  |
| 13.7.3 | Stellen Sie sicher, dass die Datenintegrität des DAG durch kryptografische Signaturen und manipulationssichere Speichermechanismen geschützt ist.                                                              |   2   |  D/V  |
| 13.7.4 | Überprüfen Sie, ob Workflow-Visualisierungssysteme eine Eingabevalidierung implementieren, um Injektionsangriffe durch manipulierte Knoten- oder Kantendaten zu verhindern.                                    |   2   |  D/V  |
| 13.7.5 | Überprüfen Sie, ob Echtzeit-DAG-Aktualisierungen durch Rate-Limiting beschränkt und validiert werden, um Denial-of-Service-Angriffe auf Visualisierungssysteme zu verhindern.                                  |   3   |  D/V  |

---

## C13.8 Proaktives Überwachen sicherheitsrelevanten Verhaltens

Erkennung und Verhinderung von Sicherheitsbedrohungen durch proaktive Analyse des Agentenverhaltens.

|   #    | Beschreibung                                                                                                                                                      | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 13.8.1 | Stellen Sie sicher, dass proaktive Agentenverhalten vor der Ausführung mit einer Risikoabschätzungsintegration sicherheitsvalidiert werden.                       |   1   |  D/V  |
| 13.8.2 | Stellen Sie sicher, dass autonome Initiativ-Auslöser die Bewertung des Sicherheitskontexts und die Analyse der Bedrohungslandschaft umfassen.                     |   2   |  D/V  |
| 13.8.3 | Überprüfen Sie, ob proaktive Verhaltensmuster auf potenzielle Sicherheitsimplikationen und unerwünschte Folgen analysiert werden.                                 |   2   |  D/V  |
| 13.8.4 | Stellen Sie sicher, dass sicherheitskritische proaktive Maßnahmen explizite Genehmigungsketten mit Prüfprotokollen erfordern.                                     |   3   |  D/V  |
| 13.8.5 | Überprüfen Sie, ob die Verhaltensanomalieerkennung Abweichungen in den Mustern proaktiver Agenten identifiziert, die auf eine Kompromittierung hinweisen könnten. |   3   |  D/V  |

---

## Literaturverzeichnis

