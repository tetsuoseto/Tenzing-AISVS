# C3 Modelllebenszyklusmanagement & Änderungssteuerung

## Kontrollziel

KI-Systeme müssen Änderungssteuerungsprozesse implementieren, die verhindern, dass nicht autorisierte oder unsichere Modelländerungen in die Produktion gelangen. Diese Kontrollen gewährleisten die Modellintegrität über den gesamten Lebenszyklus hinweg – von der Entwicklung über die Bereitstellung bis hin zur Stilllegung – und ermöglichen eine schnelle Reaktion auf Vorfälle sowie die Aufrechterhaltung der Verantwortlichkeit für alle Änderungen.

Kernziel der Sicherheit: Nur autorisierte, validierte Modelle gelangen durch kontrollierte Prozesse, die Integrität, Rückverfolgbarkeit und Wiederherstellbarkeit gewährleisten, in die Produktivumgebung.

---

## C3.1 Modellautorisierung & Integrität

Nur autorisierte Modelle mit verifizierter Integrität gelangen in Produktionsumgebungen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                            | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 3.1.1 | Verifizieren Sie, dass ein Modell-Registry ein Inventar aller bereitgestellten Modellartefakte führt und eine maschinenlesbare Modell-/KI-Stückliste (MBOM/AIBOM) erstellt (z. B. SPDX oder CycloneDX).                                                                                                                                                                 |   1   |   V   |
| 3.1.2 | Stellen Sie sicher, dass alle Modellartefakte (Gewichte, Konfigurationen, Tokenizer, Basismodelle, Feinabstimmungen, Adapter und Sicherheits-/Richtlinienmodelle) kryptografisch von autorisierten Stellen signiert und bei der Bereitstellungsfreigabe (und beim Laden) verifiziert werden, wobei alle nicht signierten oder manipulierten Artefakte blockiert werden. |   1   |  D/V  |
| 3.1.3 | Verifizieren Sie, dass die Nachverfolgung von Abstammung und Abhängigkeiten einen Abhängigkeitsgraphen pflegt, der die Identifizierung aller konsumierenden Services und Agenten pro Umgebung ermöglicht (z. B. Dev, Staging, Prod).                                                                                                                                    |   3   |   V   |
| 3.1.4 | Überprüfen Sie, dass die Integrität der Modellentstehung und die Nachweisprotokolle die Identität einer autorisierenden Stelle, Prüfsummen der Trainingsdaten, Validierungstestergebnisse mit Bestehen/Nichtbestehen-Status, Signatur-Fingerprint/Zertifikatsketten-ID, einen Erstellungstimestamp und genehmigte Einsatzumgebungen enthalten.                          |   3   |  D/V  |

---

## C3.2 Modellvalidierung und -prüfung

Modelle müssen vor der Bereitstellung definierte Sicherheits- und Schutzvalidierungen bestehen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                    | Ebene | Rolle |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 3.2.1 | Stellen Sie sicher, dass Modelle automatisierten Sicherheitstests unterzogen werden, die Eingabevalidierung, Ausgabe-Sanitierung und Sicherheitsevaluierungen mit Bestehen/Nichtbestehen-Grenzwerten vor der Bereitstellung umfassen.                                                                                                                                                                           |   1   |  D/V  |
| 3.2.2 | Überprüfen Sie, dass die Sicherheitstests Agenten-Workflows, Tool- und MCP-Integrationen, RAG- und Speicherinteraktionen, multimodale Eingaben sowie Schutzmaßnahmen (Sicherheitsmodelle oder Erkennungsdienste) mithilfe eines versionierten Evaluierungsrahmens abdecken.                                                                                                                                     |   2   |  D/V  |
| 3.2.3 | Stellen Sie sicher, dass alle Modelländerungen (Bereitstellung, Konfiguration, Außerbetriebnahme) unveränderliche Prüfprotokolle erzeugen, die einen Zeitstempel, eine authentifizierte Akteursidentität, einen Änderungstyp sowie Vorher-/Nachher-Zustände enthalten, zusammen mit Verfolgungsmetadaten (Umgebung und konsumierende Dienste/Agenten) und einem Modellkennzeichen (Version/Prüfsumme/Signatur). |   2   |   V   |
| 3.2.4 | Stellen Sie sicher, dass Validierungsfehler die Modellbereitstellung automatisch blockieren, es sei denn, es liegt eine ausdrückliche Überschreibungsfreigabe von vorab festgelegtem autorisiertem Personal mit dokumentierten geschäftlichen Begründungen vor.                                                                                                                                                 |   3   |  D/V  |

---

## C3.3 Kontrollierte Bereitstellung & Rollback

Modellbereitstellungen müssen kontrolliert, überwacht und umkehrbar sein.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                             | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 3.3.1 | Stellen Sie sicher, dass die Bereitstellungsprozesse kryptografische Signaturen validieren und Integritätsprüfsummen vor der Aktivierung oder dem Laden des Modells berechnen, und dass die Bereitstellung bei jeder Abweichung fehlschlägt.                                                                             |   1   |  D/V  |
| 3.3.2 | Verifizieren Sie, dass Produktionsbereitstellungen schrittweise Rollout-Mechanismen implementieren (z. B. Canary- oder Blue-Green-Bereitstellungen) mit automatisierten Rücksetzungsmechanismen, die auf zuvor vereinbarten Fehlerquoten, Latenzgrenzen, Schutzschildwarnungen oder Ausfallraten von Tools/MCP basieren. |   2   |   D   |
| 3.3.3 | Überprüfen Sie, dass Rollback-Funktionen den vollständigen Modellzustand (Gewichte, Konfigurationen, Abhängigkeiten einschließlich Adapter und Sicherheits-/Richtlinienmodelle) atomar wiederherstellen.                                                                                                                 |   2   |  D/V  |
| 3.3.4 | Überprüfen Sie, ob die Notabschaltfunktion des Modells die Modellendpunkte innerhalb einer vordefinierten Reaktionszeit deaktivieren kann.                                                                                                                                                                               |   3   |  D/V  |
| 3.3.5 | Überprüfen Sie, dass der Not-Aus auf alle Teile des Systems übergreift, einschließlich z. B. der Deaktivierung des Agenten-Tools und des MCP-Zugriffs, der RAG-Connectoren, der Datenbank- und API-Zugangsdaten sowie der Memory-Store-Bindungen.                                                                        |   3   |  D/V  |

---

## C3.4 Sichere Entwicklungspraktiken

Model-Entwicklungs- und Trainingsprozesse müssen sichere Praktiken befolgen, um eine Kompromittierung zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                             | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 3.4.1 | Stellen Sie sicher, dass die Entwicklungs-, Test- und Produktionsumgebungen des Modells physisch oder logisch voneinander getrennt sind. Sie verfügen über keine gemeinsame Infrastruktur, unterschiedliche Zugriffskontrollen und isolierte Datenspeicher, und auch Agenten-Orchestrierung sowie Tool- oder MCP-Server sind ebenfalls isoliert.                                                         |   1   |  D/V  |
| 3.4.2 | Stellen Sie sicher, dass Artefakte der Modellentwicklung (wie Hyperparameter, Trainingsskripte, Konfigurationsdateien, Prompt-Vorlagen, Agentenrichtlinien/Leitungsgrafiken, Tool- oder MCP-Verträge/Schemata sowie Aktionskataloge oder Berechtigungsliste für Fähigkeiten) in der Versionskontrolle gespeichert werden und vor der Verwendung im Training eine Peer-Review-Zulassung erforderlich ist. |   1   |   D   |
| 3.4.3 | Stellen Sie sicher, dass das Modelltraining und die Feinabstimmung in isolierten Umgebungen mit kontrolliertem Netzwerkzugang durch Egress-Whitelist-Listen erfolgen und kein Zugriff auf Produktionstools oder MCP-Ressourcen besteht.                                                                                                                                                                  |   2   |  D/V  |
| 3.4.4 | Stellen Sie sicher, dass Trainingsdatenquellen vor der Verwendung in der Modellentwicklung, einschließlich RAG-Indizes, Werkzeugprotokollen und agentengenerierten Daten, die für das Fine-Tuning verwendet werden, durch Integritätsprüfungen validiert und über vertrauenswürdige Quellen mit dokumentierter Nachverfolgung authentifiziert werden.                                                    |   2   |   D   |

---

## C3.5 Modellausmusterung und Stilllegung

Modelle müssen sicher außer Betrieb genommen werden, wenn sie nicht mehr benötigt werden oder wenn Sicherheitsprobleme erkannt werden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                             | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 3.5.1 | Überprüfen Sie, dass zurückgezogene Modellartefakte (einschließlich Adapter sowie Sicherheits- und Richtlinienmodelle) sicher durch eine sichere kryptografische Löschung gelöscht werden.                                                                                                                                                                                                                                               |   1   |  D/V  |
| 3.5.2 | Stellen Sie sicher, dass Modell-Ruhestandsereignisse mit Zeitstempel und Akteur-Identität, Modellkennzeichner (Version/Digest/Signatur) sowie Trace-Metadaten (Umgebung und verwendende Dienste/Agenten) protokolliert werden. Modellsignaturen werden widerrufen, Registry-/Bereitstellungs-Deny-Listen werden aktualisiert und Modell-Loader-Caches werden invalidiert, um zu verhindern, dass Agenten zurückgezogene Artefakte laden. |   2   |   V   |

---

## Literaturverzeichnis

* [MITRE ATLAS](https://atlas.mitre.org/)
* [MLOps Principles](https://ml-ops.org/content/mlops-principles)
* [Reinforcement fine-tuning](https://platform.openai.com/docs/guides/reinforcement-fine-tuning)
* [What is AI adversarial robustness? – IBM Research](https://research.ibm.com/blog/securing-ai-workflows-with-adversarial-robustness)

