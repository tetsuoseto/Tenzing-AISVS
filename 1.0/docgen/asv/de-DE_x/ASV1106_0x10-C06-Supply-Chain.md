# C6 Lieferkettensicherheit für Modelle, Frameworks & Daten

## Kontrollziel

Angriffe auf die KI-Lieferkette nutzen Modelle, Frameworks oder Datensätze von Drittanbietern aus, um Hintertüren, Verzerrungen oder ausnutzbaren Code einzubetten. Diese Kontrollen bieten eine durchgängige Rückverfolgbarkeit, Schwachstellenmanagement und Überwachung, um den gesamten Modellentwicklungszyklus zu schützen.

---

## C6.1 Überprüfung vortrainierter Modelle & Integrität der Herkunft

Bewerten und authentifizieren Sie Herkunft, Lizenzen und versteckte Verhaltensweisen von Drittanbietermodellen vor jeglichem Feintuning oder Einsatz.

|   #   | Beschreibung                                                                                                                                                                                         | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 6.1.1 | Stellen Sie sicher, dass jedes Drittanbieter‑Modellartefakt einen signierten Provenienz‑Datensatz enthält, der seine Quelle, Version und Integritätsprüfsumme identifiziert.                         |   1   |  D/V  |
| 6.1.2 | Stellen Sie sicher, dass Modelle vor dem Import mithilfe automatisierter Werkzeuge auf bösartige Schichten oder Trojaner-Trigger gescannt werden.                                                    |   1   |  D/V  |
| 6.1.3 | Überprüfen Sie, ob Modelllizenzen, Exportkontrollkennzeichnungen und Angaben zur Datenherkunft in einem AI-BOM-Eintrag aufgezeichnet sind.                                                           |   2   |   V   |
| 6.1.4 | Stellen Sie sicher, dass hochriskante Modelle (z. B. öffentlich hochgeladene Gewichte, nicht verifizierte Ersteller) bis zur Überprüfung und Freigabe durch einen Menschen unter Quarantäne bleiben. |   2   |  D/V  |
| 6.1.5 | Überprüfen Sie, ob das Transfer-Learning-Feinabstimmung eine adversariale Bewertung besteht, um versteckte Verhaltensweisen zu erkennen.                                                             |   3   |   D   |

---

## C6.2 Framework- und Bibliotheks-Scanning

Scannen Sie kontinuierlich AI-Frameworks und -Bibliotheken auf Schwachstellen und bösartigen Code, um den Laufzeit-Stack sicher zu halten.

|   #   | Beschreibung                                                                                                                                                               | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 6.2.1 | Verifizieren Sie, dass CI-Pipelines Abhängigkeits-Scanner für KI-Frameworks und kritische Bibliotheken ausführen.                                                          |   1   |  D/V  |
| 6.2.2 | Stellen Sie sicher, dass kritische und hoch schwerwiegende Schwachstellen die Freigabe zu Produktionsabbildungen blockieren.                                               |   2   |  D/V  |
| 6.2.3 | Stellen Sie sicher, dass die statische Codeanalyse bei geforkten oder eingebundenen KI-Bibliotheken ausgeführt wird.                                                       |   2   |   D   |
| 6.2.4 | Stellen Sie sicher, dass Vorschläge zur Aktualisierung des Frameworks eine Sicherheitsfolgenabschätzung enthalten, die sich auf öffentliche Schwachstellenquellen bezieht. |   2   |   V   |
| 6.2.5 | Überprüfen Sie, ob Laufzeitsensoren bei unerwarteten dynamischen Bibliotheksladungen, die von der signierten SBOM abweichen, Alarm schlagen.                               |   3   |   V   |

---

## C6.3 Abhängigkeitsfestlegung und -überprüfung

Fixieren Sie jede Abhängigkeit auf unveränderliche Digests und verifizieren Sie Builds, um manipulationsfreie Artefakte zu garantieren.

|   #   | Beschreibung                                                                                                                                                               | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 6.3.1 | Überprüfen Sie, ob alle Paketmanager Versionsfestlegung über Sperrdateien (Lockfiles) durchsetzen.                                                                         |   1   |  D/V  |
| 6.3.2 | Überprüfen Sie, ob unveränderliche Digests anstelle von veränderlichen Tags in Container-Verweisen verwendet werden.                                                       |   1   |  D/V  |
| 6.3.3 | Überprüfen Sie, ob abgelaufene oder nicht gewartete Abhängigkeiten automatisierte Benachrichtigungen auslösen, um festgelegte Versionen zu aktualisieren oder zu ersetzen. |   2   |   D   |
| 6.3.4 | Stellen Sie sicher, dass Build-Bescheinigungen für einen Zeitraum aufbewahrt werden, der durch die organisatorische Richtlinie für die Prüfspurigkeit definiert ist.       |   3   |   V   |
| 6.3.5 | Stellen Sie sicher, dass die Überprüfungen der reproduzierbaren Builds Hashes über CI-Durchläufe hinweg vergleichen, um identische Ausgaben zu gewährleisten.              |   3   |   D   |

---

## C6.4 Durchsetzung vertrauenswürdiger Quellen

Erlauben Sie den Download von Artefakten nur von kryptographisch verifizierten, von der Organisation genehmigten Quellen und blockieren Sie alles andere.

|   #   | Beschreibung                                                                                                                                               | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 6.4.1 | Stellen Sie sicher, dass Modellgewichte, Datensätze und Container nur von genehmigten Quellen oder internen Registern heruntergeladen werden.              |   1   |  D/V  |
| 6.4.2 | Stellen Sie sicher, dass kryptografische Signaturen die Identität des Herausgebers überprüfen, bevor Artefakte lokal zwischengespeichert werden.           |   1   |  D/V  |
| 6.4.3 | Überprüfen Sie, dass Ausgehkontrollen nicht authentifizierte Artefakt-Downloads blockieren, um die Richtlinie für vertrauenswürdige Quellen durchzusetzen. |   2   |   D   |
| 6.4.4 | Überprüfen Sie, ob Repository-Whitelisteneinträge regelmäßig überprüft werden und Nachweise für die geschäftliche Rechtfertigung jedes Eintrags vorliegen. |   3   |   V   |
| 6.4.5 | Überprüfen Sie, ob Policy-Verstöße die Quarantäne von Artefakten auslösen und die Rücksetzung abhängiger Pipeline-Ausführungen bewirken.                   |   3   |   V   |

---

## C6.5 Bewertung der Risiken bei Datensätzen von Drittanbietern

Bewerten Sie externe Datensätze auf Vergiftung, Voreingenommenheit und rechtliche Konformität und überwachen Sie diese während ihres gesamten Lebenszyklus.

|   #   | Beschreibung                                                                                                                                                                                     | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 6.5.1 | Stellen Sie sicher, dass externe Datensätze einer Risikoanalyse auf Vergiftung unterzogen werden (z. B. Daten-Fingerprinting, Ausreißererkennung).                                               |   1   |  D/V  |
| 6.5.2 | Stellen Sie sicher, dass unerlaubte Inhalte (z. B. urheberrechtlich geschütztes Material, personenbezogene Daten) vor dem Training durch automatisierte Bereinigung erkannt und entfernt werden. |   1   |   D   |
| 6.5.3 | Überprüfen Sie, ob Ursprung, Abstammung und Lizenzbedingungen für Datensätze in AI BOM-Einträgen erfasst sind.                                                                                   |   2   |   V   |
| 6.5.4 | Stellen Sie sicher, dass Bias-Metriken (z. B. demografische Parität, Chancengleichheit) vor der Genehmigung des Datensatzes berechnet werden.                                                    |   2   |   D   |
| 6.5.5 | Überprüfen Sie, ob die periodische Überwachung Drift oder Korruption in gehosteten Datensätzen erkennt.                                                                                          |   3   |   V   |

---

## C6.6 Überwachung von Supply-Chain-Angriffen

Erkennen Sie Bedrohungen in der Lieferkette frühzeitig durch Schwachstellen-Feeds, Audit-Log-Analysen und Bereitschaft zur Vorfallreaktion.

|   #   | Beschreibung                                                                                                                                                                                  | Ebene | Rolle |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 6.6.1 | Stellen Sie sicher, dass Vorfallreaktions-Handbücher Rücksetzverfahren für kompromittierte Modelle oder Bibliotheken enthalten.                                                               |   2   |   D   |
| 6.6.2 | Stellen Sie sicher, dass CI/CD-Auditprotokolle an ein zentrales Sicherheitsmonitoring gestreamt werden, mit Erkennungen für anomale Paketabrufe oder manipulierte Build-Schritte.             |   2   |   V   |
| 6.6.3 | Überprüfen Sie, ob die Bedrohungsintelligenz-Anreicherungen KI-spezifische Indikatoren (z. B. Indikatoren für Modellvergiftung als Kompromittierungsanzeichen) bei der Alarmbewertung taggen. |   3   |   V   |

---

## C6.7 KI-Stückliste für Modellartefakte

Erstellen und signieren Sie detaillierte, KI-spezifische Stücklisten (AI BOMs), damit nachgelagerte Verbraucher die Komponentenintegrität zum Zeitpunkt der Bereitstellung überprüfen können.

|   #   | Beschreibung                                                                                                                                                      | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 6.7.1 | Stellen Sie sicher, dass jedes Modellartefakt eine AI BOM veröffentlicht, die Datensätze, Gewichte, Hyperparameter und Lizenzen auflistet.                        |   1   |  D/V  |
| 6.7.2 | Stellen Sie sicher, dass die AI-BOM-Erstellung und die kryptografische Signierung im CI automatisiert sind und für den Merge erforderlich sind.                   |   2   |  D/V  |
| 6.7.3 | Überprüfen Sie, dass die AI BOM-Vollständigkeitsprüfungen den Build abbrechen, wenn Metadaten zu Komponenten (Hash und Lizenz) fehlen.                            |   2   |   D   |
| 6.7.4 | Überprüfen Sie, ob nachgelagerte Verbraucher KI-Stücklisten (AI BOMs) über die API abfragen können, um importierte Modelle zur Bereitstellungszeit zu validieren. |   2   |   V   |
| 6.7.5 | Überprüfen Sie, ob AI-Stücklisten versionskontrolliert sind und differenziert werden, um unautorisierte Änderungen zu erkennen.                                   |   3   |   V   |

---

## Literaturverzeichnis

* [OWASP LLM03:2025 Supply Chain](https://genai.owasp.org/llmrisk/llm032025-supply-chain/)
* [MITRE ATLAS : Supply Chain Compromise](https://atlas.mitre.org/techniques/AML.T0010)
* [SBOM Overview – CISA](https://www.cisa.gov/sbom)
* [CycloneDX – Machine Learning Bill of Materials](https://cyclonedx.org/capabilities/mlbom/)

