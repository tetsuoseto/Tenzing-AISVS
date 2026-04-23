# C6 Supply Chain Security für Modelle, Frameworks & Daten

## Kontrollziel

KI-Lieferkettenangriffe nutzen Drittanbieter-Modelle, -Frameworks oder -Datensätze aus, um Backdoors, Verzerrungen oder ausnutzbaren Code einzubetten. Diese Kontrollen stellen die Nachverfolgbarkeit, Prüfung und Überwachung von KI-spezifischen Lieferkettenartefakten während des gesamten Modell-Lebenszyklus sicher.

Allgemeine Software-Lieferketten-Controls (Dependency-Scanning, Version-Pinning, Lockfile-Durchsetzung, Container-Digest-Pinning, Build-Attestierung, reproduzierbare Builds, SBOM-Generierung, CI/CD-Audit-Logging usw.) werden durch ASVS v5 (V13, V15), OWASP SCVS, SLSA und CIS Controls abgedeckt und hier nicht wiederholt. Dieses Kapitel konzentriert sich auf Lieferkettenrisiken, die für KI einzigartig sind: Integrität von Modellartefakten, Backdoor-Erkennung in vortrainierten Gewichten, Datenvergiftung, AI-spezifische Bills of Materials sowie Vertrauen in den Modellherausgeber.

---

## C6.1 Überprüfung vorab trainierter Modelle & Integrität der Herkunft

Bewerten und authentifizieren Sie die Herkunft von Drittanbieter-Modellen und deren versteckte Verhaltensweisen, bevor Sie ein Fine-Tuning oder eine Bereitstellung durchführen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                    | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.1.1 | Überprüfen Sie, dass jedes Drittanbieter-Modellartefakt eine signierte Ursprungs- und Integritätsaufzeichnung enthält, die seine Quelle, Version und den Integritäts-Checksumme identifiziert.                                                                                                                                  |   1   |
| 6.1.2 | Stellen Sie sicher, dass Modelle vor dem Import mithilfe automatisierter Tools auf bösartige Layers oder Trojaner-Trigger überprüft werden.                                                                                                                                                                                     |   1   |
| 6.1.3 | Stellen Sie sicher, dass Hochrisikomodelle (z. B. öffentlich hochgeladene Gewichte, nicht verifizierte Ersteller) in Quarantäne bleiben, bis eine menschliche Überprüfung und Freigabe erfolgt.                                                                                                                                 |   2   |
| 6.1.4 | Stellen Sie sicher, dass Drittanbieter- oder Open-Source-Modelle eine definierte Verhaltens-Validierungstest-Suite bestehen (die Sicherheit, Ausrichtung und Fähigkeitsgrenzen abdeckt, die für den Bereitstellungskontext relevant sind), bevor sie importiert oder in irgendeine Nicht-Entwicklungsumgebung befördert werden. |   2   |
| 6.1.5 | Verifizieren Sie, dass Transfer-Learning-Feintuning den adversarialen Test zur Erkennung versteckter Verhaltensweisen besteht.                                                                                                                                                                                                  |   3   |

---

## C6.2 Durchsetzung einer vertrauenswürdigen Herkunft für KI-Artefakte

Erlaube KI-Artifact-Downloads nur von unternehmensweit genehmigten Quellen und verifiziere die Identität des Modell-Publishers.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                               | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.2.1 | Stellen Sie sicher, dass Modellgewichte, Datensätze und Fine-Tuning-Adapter nur von genehmigten Quellen oder internen Registern heruntergeladen werden.                                                                                                                                                    |   1   |
| 6.2.2 | Überprüfen Sie, dass kryptografische Signaturschlüssel, die zur Authentifizierung von Modellherausgebern verwendet werden, pro Quell-Registry gepinnt sind, und dass Schlüsselrotationsereignisse eine explizite erneute Genehmigung erfordern, bevor aktualisierte Schlüssel als vertrauenswürdig gelten. |   3   |

---

## C6.3 Risikobewertung für Datensätze von Dritten

Bewerten Sie externe Datensätze auf Vergiftung und rechtliche Compliance und überwachen Sie sie über ihren gesamten Lebenszyklus hinweg.

|   #   | Beschreibung                                                                                                                                                                  | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.3.1 | Stellen Sie sicher, dass nicht zulässiger Inhalt (z.B. urheberrechtlich geschütztes Material, PII) vor dem Training über automatisiertes Scrubbing erkannt und entfernt wird. |   1   |
| 6.3.2 | Überprüfen Sie, dass externe Datensätze eine Risikoabschätzung hinsichtlich Vergiftung durchlaufen (z.B. Daten-Fingerprinting, Outlier-Erkennung).                            |   2   |
| 6.3.3 | Stellen Sie sicher, dass Herkunft, Abstammung und Lizenzbedingungen für Datensätze in AI-BOM-Einträgen erfasst werden.                                                        |   2   |
| 6.3.4 | Verifizieren Sie, dass regelmäßiges Monitoring Drift oder Beschädigung in gehosteten Datensätzen erkennt.                                                                     |   3   |

---

## C6.4 Überwachung von Supply-Chain-Angriffen

Erkennen Sie KI-spezifische Supply-Chain-Bedrohungen durch Threat-Intelligence-Anreicherung und Einsatzbereitschaft im Incident Response.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                     | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.4.1 | Stellen Sie sicher, dass Incident-Response-Playbooks Verfahren enthalten, die spezifisch für kompromittierte AI-Artefakte sind, wie z.B. das Rollback vergifteter Modelle, die Widerrufung von Modellsignaturen und die erneute Bewertung nachgelagerter Systeme, die die betroffenen Artefakte verwendet haben. |   2   |
| 6.4.2 | Überprüfen Sie, dass Bedrohungsaufklärungs-Anreicherungs-Tags AI-spezifische Indikatoren (z.B. Indikatoren für Kompromittierung durch Modellvergiftung) im Alert-Triage-Prozess auswerten.                                                                                                                       |   3   |

---

## C6.5 AI BOM für Model Artifacts

Generieren und signieren Sie detaillierte AI-spezifische Stücklisten (AI-BOMs), damit nachgelagerte Verbraucher die Integrität der Komponenten zur Bereitstellungszeit überprüfen können.

|   #   | Beschreibung                                                                                                                                                                                           | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 6.5.1 | Verifizieren Sie, dass jedes Modellartefakt eine versionierte AI-BOM veröffentlicht, die Datensätze, Gewichte, Hyperparameter, Lizenzen, Exportkontroll-Tags und Aussagen zur Datenherkunft auflistet. |   1   |
| 6.5.2 | Überprüfen Sie, dass AI-BOMs vor der Bereitstellung kryptografisch signiert sind.                                                                                                                      |   2   |
| 6.5.3 | Überprüfen Sie, dass die AI-BOM-Vollständigkeitsprüfungen den Build fehlschlagen lassen, wenn für irgendeine Komponente Metadaten (Hash und Lizenz) fehlen.                                            |   2   |
| 6.5.4 | Stellen Sie sicher, dass nachgelagerte Verbraucher KI-BOMs über eine API abfragen können, um importierte Modelle zur Bereitstellungszeit zu validieren.                                                |   2   |

---

## References

* [OWASP LLM03:2025 Supply Chain](https://genai.owasp.org/llmrisk/llm032025-supply-chain/)
* [MITRE ATLAS: Supply Chain Compromise](https://atlas.mitre.org/techniques/AML.T0010)
* [SBOM Overview: CISA](https://www.cisa.gov/sbom)
* [CycloneDX: Machine Learning Bill of Materials](https://cyclonedx.org/capabilities/mlbom/)

