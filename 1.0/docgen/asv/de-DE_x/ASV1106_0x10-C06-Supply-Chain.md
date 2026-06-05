# C6 Supply Chain Security für Modelle, Frameworks & Daten

## Kontrollziel

KI-Lieferkettenangriffe nutzen Drittanbieter-Modelle, Frameworks oder Datensätze aus, um Hintertüren, Verzerrungen oder ausnutzbaren Code einzubetten. Diese Kontrollen gewährleisten Nachverfolgbarkeit, Prüfung und Überwachung von KI-spezifischen Lieferkettenartefakten während des gesamten Modelllebenszyklus. Dieses Kapitel behandelt die für KI einzigartigen Lieferkettenrisiken: Integrität von Modellartefakten, Erkennung von Hintertüren in vortrainierten Gewichten, Datenvergiftung, KI-spezifische Bills of Materials sowie Vertrauen in den Modell-Publisher.

---

## C6.1 Überprüfung vorab trainierter Modelle & Integrität der Herkunft

Bewerten und verifizieren Sie die Herkunft von Modellen Dritter und deren verborgene Verhaltensweisen, bevor Sie eine Feinabstimmung oder Bereitstellung durchführen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.1.1 | Stellen Sie sicher, dass jedes Drittanbieter-Modell-Artifact einen signierten Herkunfts- und Integritätsnachweis enthält, der seine Quelle, Version und den Integritäts-Checksum identifiziert.                                                                                                                                             |   1   |
| 6.1.2 | Stellen Sie sicher, dass Modelle vor dem Import mithilfe automatisierter Tools auf bösartige Schichten oder Trojaner-Auslöser überprüft werden.                                                                                                                                                                                             |   1   |
| 6.1.3 | Stellen Sie sicher, dass Hochrisiko-Modelle (z.B. öffentlich hochgeladene Gewichte, nicht verifizierte Ersteller) unter Quarantäne bleiben, bis eine menschliche Prüfung und die Freigabe erfolgt sind.                                                                                                                                     |   2   |
| 6.1.4 | Stellen Sie sicher, dass Dritthersteller- oder Open-Source-Modelle eine definierte Verhaltenstestsuite zur Verhaltensakzeptanz bestehen (die Sicherheit, Ausrichtung und Kompetenzgrenzen abdeckt, die für den Bereitstellungskontext relevant sind), bevor sie importiert oder in irgendeine Nicht-Entwicklungsumgebung übernommen werden. |   2   |
| 6.1.5 | Überprüfen Sie, dass Transfer-Learning-Feinabstimmungen die adversarialen Evaluierungen bestehen, um verborgene Verhaltensweisen zu erkennen.                                                                                                                                                                                               |   3   |

---

## C6.2 Erzwingung vertrauenswürdiger Quellen für KI-Artefakte

Erlaube KI-Artifact-Downloads nur von von der Organisation genehmigten Quellen und überprüfe die Identität des Modell-Publishers.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                              | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.2.1 | Überprüfen Sie, dass Modellgewichte, Datensätze und Fine-Tuning-Adapter nur von genehmigten Quellen oder internen Registries heruntergeladen werden.                                                                                                                                                      |   1   |
| 6.2.2 | Prüfen Sie, dass kryptografische Signaturschlüssel, die zur Authentifizierung von Modelleanbieter(n) verwendet werden, pro Quell-Registry gepinnt sind, und dass Key-Rotation-Ereignisse eine explizite erneute Freigabe erfordern, bevor aktualisierte Schlüssel als vertrauenswürdig eingestuft werden. |   3   |

---

## C6.3 Risikoanalyse für Datensätze von Drittanbietern

Bewerten Sie externe Datensätze auf Vergiftung und rechtliche Einhaltung und überwachen Sie sie während ihres gesamten Lebenszyklus.

|   #   | Beschreibung                                                                                                                                                                                      | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.3.1 | Stellen Sie sicher, dass nicht zulässige Inhalte (z.B. urheberrechtlich geschütztes Material, personenbezogene Daten) vor dem Training durch automatisches Scrubbing erkannt und entfernt werden. |   1   |
| 6.3.2 | Stellen Sie sicher, dass externe Datensätze einer Bewertung des Vergiftungsrisikos unterzogen werden (z.B. Daten-Fingerprinting, Outlier-Erkennung).                                              |   2   |
| 6.3.3 | Stellen Sie sicher, dass Ursprung, Herkunft und Lizenzbedingungen für Datensätze in AI-BOM-Einträgen erfasst werden.                                                                              |   2   |
| 6.3.4 | Überprüfen Sie, dass die regelmäßige Überwachung Drift oder Beschädigung in gehosteten Datensätzen erkennt.                                                                                       |   3   |

---

## C6.4 Überwachung von Supply-Chain-Angriffen

Erkennen Sie KI-spezifische Supply-Chain-Bedrohungen durch Threat-Intelligence-Anreicherung und Einsatzbereitschaft für Vorfallsreaktionen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                       | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 6.4.1 | Stellen Sie sicher, dass Incident-Response-Playbooks Verfahren enthalten, die speziell für kompromittierte KI-Artefakte gelten, wie das Zurücksetzen von vergifteten Modellen, die Sperrung von Modellsignaturen und die erneute Bewertung nachgelagerter Systeme, die die betroffenen Artefakte konsumiert haben. |   2   |
| 6.4.2 | Überprüfen Sie, dass Threat-Intelligence-Enrichment-Tags AI-spezifische Indikatoren (z. B. Indicators of Compromise für Model-Poisoning) im Alert-Triage ergänzen.                                                                                                                                                 |   3   |

---

## C6.5 AI BOM für Model Artifacts

Generieren und signieren Sie detaillierte KI-spezifische Stücklisten (KI-BOMs), damit nachgelagerte Verbraucher die Integrität der Komponenten beim Deployment-Zeitpunkt überprüfen können.

|   #   | Beschreibung                                                                                                                                                                                                                                             | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 6.5.1 | Stellen Sie sicher, dass jedes Modellartefakt ein versioniertes, maschinenlesbares AI-BOM (z.B. CycloneDX oder SPDX) veröffentlicht, das Datensätze, Gewichte, Hyperparameter, Lizenzen, Exportkontroll-Tags sowie Aussagen zur Datenherkunft auflistet. |   1   |
| 6.5.2 | Verifizieren Sie, dass AI-BOMs vor der Bereitstellung kryptografisch signiert sind.                                                                                                                                                                      |   2   |
| 6.5.3 | Überprüfen Sie, dass die AI-BOM-Vollständigkeitsprüfungen den Build fehlschlagen lassen, wenn Metadaten zu einer Komponente fehlen (Hash und Lizenz).                                                                                                    |   2   |
| 6.5.4 | Stellen Sie sicher, dass nachgelagerte Konsumenten über eine API auf AI BOMs zugreifen können, um importierte Modelle zur Laufzeit der Bereitstellung zu validieren.                                                                                     |   2   |

---

## Referenzen

* [OWASP LLM03:2025 Supply Chain](https://genai.owasp.org/llmrisk/llm032025-supply-chain/)
* [MITRE ATLAS: Supply Chain Compromise](https://atlas.mitre.org/techniques/AML.T0010)
* [SBOM Overview: CISA](https://www.cisa.gov/sbom)
* [CycloneDX: Machine Learning Bill of Materials](https://cyclonedx.org/capabilities/mlbom/)
* [OWASP AIBOM](https://genai.owasp.org/owasp-aibom/)

