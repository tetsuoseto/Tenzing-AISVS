# Anhang C: KI-Sicherheitsgovernance & Dokumentation (Neu organisiert)

## Zielsetzung

Dieser Anhang enthält grundlegende Anforderungen für die Einrichtung von Organisationsstrukturen, Richtlinien, Dokumentationen und Prozessen zur Steuerung der KI-Sicherheit während des gesamten Systemlebenszyklus.

---

## AC.1 Übernahme des KI-Risikomanagementrahmens

|   #    | Beschreibung                                                                                                                             | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.1.1 | Überprüfen Sie, ob eine speziell für KI entwickelte Risikobewertungsmethodik dokumentiert und implementiert ist.                         |   1   |  D/V  |
| AC.1.2 | Stellen Sie sicher, dass Risikoanalysen zu wichtigen Zeitpunkten im KI-Lebenszyklus und vor wesentlichen Änderungen durchgeführt werden. |   2   |   D   |
| AC.1.3 | Überprüfen Sie, ob der Risikomanagementrahmen mit etablierten Standards (z. B. NIST AI RMF) übereinstimmt.                               |   3   |  D/V  |

---

## AC.2 KI-Sicherheitsrichtlinie und -verfahren

|   #    | Beschreibung                                                                                                                                   | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.2.1 | Überprüfen Sie, ob dokumentierte AI-Sicherheitsrichtlinien vorhanden sind.                                                                     |   1   |  D/V  |
| AC.2.2 | Stellen Sie sicher, dass Richtlinien mindestens jährlich und nach erheblichen Änderungen der Bedrohungslage überprüft und aktualisiert werden. |   2   |   D   |
| AC.2.3 | Überprüfen Sie, ob die Richtlinien alle AISVS-Kategorien und anwendbaren regulatorischen Anforderungen abdecken.                               |   3   |  D/V  |

---

## AC.3 Rollen und Verantwortlichkeiten für AI-Sicherheit

|   #    | Beschreibung                                                                                                             | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.3.1 | Stellen Sie sicher, dass KI-Sicherheitsrollen und -verantwortlichkeiten dokumentiert sind.                               |   1   |  D/V  |
| AC.3.2 | Überprüfen Sie, ob verantwortliche Personen über angemessene Sicherheitskenntnisse verfügen.                             |   2   |   D   |
| AC.3.3 | Verifizieren Sie, dass ein KI-Ethikkomitee oder ein Governance-Gremium für KI-Systeme mit hohem Risiko eingerichtet ist. |   3   |  D/V  |

---

## AC.4 Durchsetzung ethischer KI-Richtlinien

|   #    | Beschreibung                                                                                                 | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.4.1 | Überprüfen Sie, ob ethische Richtlinien für die Entwicklung und den Einsatz von KI existieren.               |   1   |  D/V  |
| AC.4.2 | Überprüfen Sie, ob Mechanismen vorhanden sind, um ethische Verstöße zu erkennen und zu melden.               |   2   |   D   |
| AC.4.3 | Stellen Sie sicher, dass regelmäßige ethische Überprüfungen der eingesetzten KI-Systeme durchgeführt werden. |   3   |  D/V  |

---

## AC.5 Überwachung der Einhaltung von KI-Vorschriften

|   #    | Beschreibung                                                                                                                 | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.5.1 | Stellen Sie sicher, dass Prozesse vorhanden sind, um anwendbare KI-Vorschriften zu identifizieren.                           |   1   |  D/V  |
| AC.5.2 | Stellen Sie sicher, dass die Einhaltung aller gesetzlichen Vorschriften bewertet wird.                                       |   2   |   D   |
| AC.5.3 | Stellen Sie sicher, dass regulatorische Änderungen rechtzeitige Überprüfungen und Aktualisierungen von KI-Systemen auslösen. |   3   |  D/V  |

---

## AC.6 Schulung für Datenverwaltung, Dokumentation & Prozess

### AC.6.1 Datenbeschaffung und sorgfältige Prüfung

|    #     | Beschreibung                                                                                                                                                                                                                                                                                                                                                                | Ebene | Rolle |
| :------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.1.1 | Stellen Sie sicher, dass nur Datensätze verwendet werden, die auf Qualität, Repräsentativität, ethische Beschaffung und Lizenzkonformität überprüft wurden, um Risiken wie Manipulation, eingebettete Vorurteile und Verletzung von geistigem Eigentum zu minimieren.                                                                                                       |   1   |  D/V  |
| AC.6.1.2 | Stellen Sie sicher, dass Drittanbieterdatenlieferanten, einschließlich Anbieter von vortrainierten Modellen und externen Datensätzen, vor der Integration ihrer Daten oder Modelle eine Sicherheits-, Datenschutz-, ethische Beschaffung- und Datenqualitätsprüfung durchlaufen.                                                                                            |   2   |  D/V  |
| AC.6.1.3 | Stellen Sie sicher, dass externe Übertragungen TLS/Authentifizierung und Integritätsprüfungen verwenden.                                                                                                                                                                                                                                                                    |   1   |   D   |
| AC.6.1.4 | Stellen Sie sicher, dass Datenquellen mit hohem Risiko (z. B. Open-Source-Datensätze mit unbekannter Herkunft, nicht überprüfte Anbieter) vor der Verwendung in sensiblen Anwendungen einer verstärkten Prüfung unterzogen werden, wie z. B. Analyse in isolierter Umgebung, umfangreiche Qualitäts- und Bias-Überprüfungen sowie gezielte Erkennung von Datenmanipulation. |   2   |  D/V  |
| AC.6.1.5 | Stellen Sie sicher, dass vor der Feinabstimmung oder dem Einsatz vortrainierte Modelle, die von Dritten bezogen wurden, auf eingebettete Verzerrungen, potenzielle Hintertüren, die Integrität ihrer Architektur und die Herkunft ihrer ursprünglichen Trainingsdaten bewertet werden.                                                                                      |   3   |  D/V  |

### AC.6.2 Verwaltung von Verzerrungen und Fairness

|    #     | Beschreibung                                                                                                                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.2.1 | Stellen Sie sicher, dass Datensätze auf repräsentative Ungleichgewichte und potenzielle Verzerrungen hinsichtlich gesetzlich geschützter Merkmale (z. B. Rasse, Geschlecht, Alter) sowie anderer ethisch sensibler Eigenschaften, die für den Anwendungsbereich des Modells relevant sind (z. B. sozioökonomischer Status, Standort), analysiert werden.                              |   1   |  D/V  |
| AC.6.2.2 | Stellen Sie sicher, dass erkannte Verzerrungen durch dokumentierte Strategien wie Neuausgleich, gezielte Datenaugmentation, algorithmische Anpassungen (z. B. Vorverarbeitung, In-Processing, Nachverarbeitungstechniken) oder Neugewichtung gemindert werden und die Auswirkungen der Minderung sowohl auf die Fairness als auch auf die Gesamtleistung des Modells bewertet werden. |   2   |  D/V  |
| AC.6.2.3 | Überprüfen Sie, ob die Fairness-Metriken nach dem Training bewertet und dokumentiert werden.                                                                                                                                                                                                                                                                                          |   2   |  D/V  |
| AC.6.2.4 | Überprüfen Sie, ob eine Richtlinie zur Verwaltung von Lebenszyklusvorurteilen Eigentümer und Überprüfungstermine zuweist.                                                                                                                                                                                                                                                             |   3   |  D/V  |

### AC.6.3 Kennzeichnungs- und Annotationsverwaltung

|     #     | Beschreibung                                                                                                                                                                                                                                                                                         | Ebene | Rolle |
| :-------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.3.1  | Stellen Sie sicher, dass die Qualität der Kennzeichnung/Annotation durch Überprüfungen von Gutachtern oder Konsens gewährleistet ist.                                                                                                                                                                |   2   |  D/V  |
| AC.6.3.2  | Stellen Sie sicher, dass für bedeutende Trainingsdatensätze Datenkarten gepflegt werden, welche die Merkmale, Motivation, Zusammensetzung, Erfassungsprozesse, Vorverarbeitung, Lizenzen sowie empfohlene und abgeratene Verwendungszwecke detailliert beschreiben.                                  |   2   |  D/V  |
| AC.6.3.3  | Stellen Sie sicher, dass Datenblätter Verzerrungsrisiken, demografische Verzerrungen und ethische Überlegungen im Zusammenhang mit dem Datensatz dokumentieren.                                                                                                                                      |   2   |  D/V  |
| AC.6.3.4  | Überprüfen Sie, ob Datenblätter zusammen mit den Datensätzen versioniert werden und bei jeder Änderung des Datensatzes aktualisiert werden.                                                                                                                                                          |   2   |  D/V  |
| AC.6.3.5  | Stellen Sie sicher, dass Datenblätter sowohl von technischen als auch von nicht-technischen Interessengruppen (z. B. Compliance, Ethik, Fachexperten) überprüft und genehmigt werden.                                                                                                                |   2   |  D/V  |
| AC.6.3.6  | Stellen Sie sicher, dass die Qualität der Kennzeichnung/Annotation durch klare Richtlinien, gegenseitige Überprüfungen durch Gutachter, Konsensmechanismen (z. B. Überwachung der Übereinstimmung zwischen den Annotatoren) und definierte Prozesse zur Behebung von Abweichungen gewährleistet ist. |   2   |  D/V  |
| AC.6.3.7  | Stellen Sie sicher, dass für Labels, die kritisch für Sicherheit, Schutz oder Fairness sind (z. B. Identifizierung toxischer Inhalte, kritische medizinische Befunde), eine verpflichtende unabhängige doppelte Überprüfung oder eine gleichwertig robuste Verifikation erfolgt.                     |   3   |  D/V  |
| AC.6.3.8  | Stellen Sie sicher, dass Beschriftungsrichtlinien und Anweisungen umfassend, versioniert und von Kollegen überprüft sind.                                                                                                                                                                            |   2   |  D/V  |
| AC.6.3.9  | Stellen Sie sicher, dass Datenschemata für Labels klar definiert und versioniert sind.                                                                                                                                                                                                               |   2   |  D/V  |
| AC.6.3.10 | Stellen Sie sicher, dass ausgelagerte oder Crowdsourcing-Labeling-Arbeitsabläufe technische und verfahrensbezogene Schutzmaßnahmen enthalten, um die Vertraulichkeit und Integrität der Daten, die Qualität der Labels sowie die Verhinderung von Datenlecks zu gewährleisten.                       |   2   |  D/V  |
| AC.6.3.11 | Stellen Sie sicher, dass alle an der Datenannotation beteiligten Personen einer Hintergrundüberprüfung unterzogen wurden und in Datensicherheit und Datenschutz geschult sind.                                                                                                                       |   2   |  D/V  |
| AC.6.3.12 | Stellen Sie sicher, dass alle Mitarbeiter für Annotationen Vertraulichkeits- und Geheimhaltungsvereinbarungen unterzeichnen.                                                                                                                                                                         |   2   |  D/V  |
| AC.6.3.13 | Überprüfen Sie, ob Annotationsplattformen Zugangskontrollen durchsetzen und Insiderbedrohungen überwachen.                                                                                                                                                                                           |   2   |  D/V  |

### AC.6.4 Qualitätskontrollen und Quarantäne für Datensätze

|    #     | Beschreibung                                                                                                                                                                                                                                                                                                                                | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.4.1 | Überprüfen Sie, ob fehlgeschlagene Datensätze mit Prüfprotokollen unter Quarantäne gestellt werden.                                                                                                                                                                                                                                         |   2   |  D/V  |
| AC.6.4.2 | Überprüfen Sie, dass Qualitätskontrollen minderwertige Datensätze blockieren, es sei denn, Ausnahmen werden genehmigt.                                                                                                                                                                                                                      |   2   |  D/V  |
| AC.6.4.3 | Stellen Sie sicher, dass manuelle Stichprobenprüfungen durch Fachexperten eine statistisch signifikante Stichprobe abdecken (z. B. ≥1 % oder 1.000 Proben, je nachdem, welcher Wert größer ist, oder wie durch die Risikobewertung festgelegt), um subtile Qualitätsprobleme zu erkennen, die von der Automatisierung nicht erfasst werden. |   2   |   V   |

### AC.6.5 Bedrohungs-/Vergiftungs-Detektion und Drift

|    #     | Beschreibung                                                                                                                            | Ebene | Rolle |
| :------: | --------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.5.1 | Überprüfen Sie, dass markierte Proben vor dem Training eine manuelle Überprüfung auslösen.                                              |   2   |  D/V  |
| AC.6.5.2 | Verifizieren Sie, dass die Ergebnisse das Sicherheitsdossier des Modells speisen und die fortlaufende Bedrohungsaufklärung informieren. |   2   |   V   |
| AC.6.5.3 | Überprüfen Sie, ob die Erkennung logisch mit neuen Bedrohungsinformationen aktualisiert wird.                                           |   3   |  D/V  |
| AC.6.5.4 | Überprüfen Sie, ob Online-Lernpipelines die Verteilungsschwankungen überwachen.                                                         |   3   |  D/V  |

### AC.6.6 Löschung, Einwilligung, Rechte, Aufbewahrung & Compliance

|     #     | Beschreibung                                                                                                                                                                                                                                                                                                                                               | Ebene | Rolle |
| :-------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.6.1  | Verifizieren Sie, dass Workflows zum Löschen von Trainingsdaten sowohl primäre als auch abgeleitete Daten löschen und die Auswirkungen auf das Modell bewerten, und dass die Auswirkungen auf betroffene Modelle bewertet und gegebenenfalls behoben werden (z. B. durch erneutes Training oder Neukalibrierung).                                          |   1   |  D/V  |
| AC.6.6.2  | Stellen Sie sicher, dass Mechanismen vorhanden sind, um den Umfang und den Status der Einwilligung der Nutzer (einschließlich Widerrufe) für die bei der Schulung verwendeten Daten zu verfolgen und zu respektieren, und dass die Einwilligung validiert wird, bevor Daten in neue Schulungsprozesse oder signifikante Modell-Updates aufgenommen werden. |   2   |   D   |
| AC.6.6.3  | Stellen Sie sicher, dass Workflows jährlich getestet und protokolliert werden.                                                                                                                                                                                                                                                                             |   2   |   V   |
| AC.6.6.4  | Stellen Sie sicher, dass für alle Trainingsdatensätze explizite Aufbewahrungsfristen definiert sind.                                                                                                                                                                                                                                                       |   1   |  D/V  |
| AC.6.6.5  | Überprüfen Sie, ob Datensätze am Ende ihres Lebenszyklus automatisch ablaufen, gelöscht oder zur Löschung überprüft werden.                                                                                                                                                                                                                                |   2   |  D/V  |
| AC.6.6.6  | Stellen Sie sicher, dass Aufbewahrungs- und Löschvorgänge protokolliert und auditierbar sind.                                                                                                                                                                                                                                                              |   2   |  D/V  |
| AC.6.6.7  | Stellen Sie sicher, dass Anforderungen an den Datenstandort und an grenzüberschreitende Datenübertragungen für alle Datensätze identifiziert und durchgesetzt werden.                                                                                                                                                                                      |   2   |  D/V  |
| AC.6.6.8  | Stellen Sie sicher, dass sektorspezifische Vorschriften (z. B. Gesundheitswesen, Finanzen) bei der Datenverarbeitung identifiziert und berücksichtigt werden.                                                                                                                                                                                              |   2   |  D/V  |
| AC.6.6.9  | Stellen Sie sicher, dass die Einhaltung der relevanten Datenschutzgesetze (z. B. DSGVO, CCPA) dokumentiert und regelmäßig überprüft wird.                                                                                                                                                                                                                  |   2   |  D/V  |
| AC.6.6.10 | Überprüfen Sie, ob Mechanismen vorhanden sind, um auf Anfragen von betroffenen Personen bezüglich Zugang, Berichtigung, Einschränkung oder Widerspruch zu reagieren.                                                                                                                                                                                       |   2   |  D/V  |
| AC.6.6.11 | Stellen Sie sicher, dass Anfragen innerhalb gesetzlich vorgeschriebener Fristen protokolliert, nachverfolgt und erfüllt werden.                                                                                                                                                                                                                            |   2   |  D/V  |
| AC.6.6.12 | Stellen Sie sicher, dass die Prozesse zur Wahrung der Rechte der betroffenen Personen regelmäßig auf ihre Wirksamkeit getestet und überprüft werden.                                                                                                                                                                                                       |   2   |  D/V  |

### AC.6.7 Versionsverwaltung & Änderungsmanagement

|    #     | Beschreibung                                                                                                                                                                         | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.6.7.1 | Stellen Sie sicher, dass eine Auswirkungsanalyse durchgeführt wird, bevor eine Datensatzversion aktualisiert oder ersetzt wird, die Modellleistung, Fairness und Compliance umfasst. |   2   |  D/V  |
| AC.6.7.2 | Verifizieren Sie, dass die Ergebnisse der Auswirkungsanalyse dokumentiert und von den relevanten Beteiligten überprüft werden.                                                       |   2   |  D/V  |
| AC.6.7.3 | Verifizieren Sie, dass Rücksetzpläne vorhanden sind, falls neue Versionen unakzeptable Risiken oder Rückschritte einführen.                                                          |   2   |  D/V  |

### AC.6.8 Governance für synthetische Daten

|    #     | Beschreibung                                                                                                                                                    | Ebene | Rolle |
| :------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.8.1 | Überprüfen Sie, ob der Generierungsprozess, die Parameter und der beabsichtigte Verwendungszweck synthetischer Daten dokumentiert sind.                         |   2   |  D/V  |
| AC.6.8.2 | Stellen Sie sicher, dass synthetische Daten vor der Verwendung im Training auf Bias, Datenschutzverletzungen und Repräsentationsprobleme risikobewertet werden. |   2   |  D/V  |

### AC.6.9 Zugriffsüberwachung

|    #     | Beschreibung                                                                                                                                                 | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.6.9.1 | Stellen Sie sicher, dass Zugriffprotokolle regelmäßig auf ungewöhnliche Muster überprüft werden, wie z. B. große Exporte oder Zugriffe von neuen Standorten. |   2   |  D/V  |
| AC.6.9.2 | Überprüfen Sie, dass Warnungen für verdächtige Zugriffsereignisse generiert und umgehend untersucht werden.                                                  |   2   |  D/V  |

### AC.6.10 Governance für adversariales Training

|     #     | Beschreibung                                                                                                                                                                                                                             | Ebene | Rolle |
| :-------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.6.10.1 | Überprüfen Sie, ob bei Verwendung von adversarialem Training die Erstellung, Verwaltung und Versionierung von adversarialen Datensätzen dokumentiert und kontrolliert wird.                                                              |   2   |  D/V  |
| AC.6.10.2 | Überprüfen Sie, ob die Auswirkungen des Trainings zur adversarialen Robustheit auf die Modellleistung (gegenüber sowohl sauberen als auch adversarialen Eingaben) und auf Fairness-Metriken bewertet, dokumentiert und überwacht werden. |   3   |  D/V  |
| AC.6.10.3 | Stellen Sie sicher, dass Strategien für adversariales Training und Robustheit regelmäßig überprüft und aktualisiert werden, um sich gegen sich entwickelnde Techniken von adversarialen Angriffen zu wappnen.                            |   3   |  D/V  |

---

## AC.7 Modelllebenszyklus-Governance & Dokumentation

|   #    | Beschreibung                                                                                                                                                                                                  | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.7.1 | Stellen Sie sicher, dass alle Modell-Artefakte semantische Versionierung (MAJOR.MINOR.PATCH) verwenden, mit dokumentierten Kriterien, die festlegen, wann jede Versionskomponente erhöht wird.                |   2   |  D/V  |
| AC.7.2 | Stellen Sie sicher, dass Notfalleinsätze eine dokumentierte Sicherheitsrisikobewertung und die Genehmigung durch eine vorab festgelegte Sicherheitsbehörde innerhalb vorab vereinbarter Zeitrahmen erfordern. |   2   |  D/V  |
| AC.7.3 | Stellen Sie sicher, dass Rollback-Artefakte (frühere Modellversionen, Konfigurationen, Abhängigkeiten) gemäß den organisatorischen Richtlinien aufbewahrt werden.                                             |   2   |   V   |
| AC.7.4 | Überprüfen Sie, ob der Zugriff auf das Prüfprotokoll eine entsprechende Autorisierung erfordert und ob alle Zugriffsversuche mit Benutzeridentität und Zeitstempel protokolliert werden.                      |   2   |  D/V  |
| AC.7.5 | Überprüfen Sie, ob die Artefakte von ausgemusterten Modellen gemäß den Datenaufbewahrungsrichtlinien aufbewahrt werden.                                                                                       |   1   |  D/V  |

---

## AC.8 Eingabe-, Ausgabe- und Aufforderungssicherheitsverwaltung

### AC.8.1 Schutz gegen Prompt-Injektion

|    #     | Beschreibung                                                                                                                                                                                                                                    | Ebene | Rolle |
| :------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.8.1.1 | Stellen Sie sicher, dass adversariale Evaluierungstests (z. B. Red Team „Many-Shot“-Prompts) vor jeder Modell- oder Prompt-Vorlagenfreigabe durchgeführt werden, mit Erfolgsraten-Schwellenwerten und automatisierten Sperren für Rückschritte. |   2   |  D/V  |
| AC.8.1.2 | Stellen Sie sicher, dass alle Aktualisierungen der Prompt-Filter-Regeln, Versionen der Klassifizierermodelle und Änderungen der Sperrlisten versionskontrolliert und prüfbar sind.                                                              |   3   |  D/V  |

### AC.8.2 Widerstandsfähigkeit gegen adversariale Beispiele

|    #     | Beschreibung                                                                                                                                                            | Ebene | Rolle |
| :------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.8.2.1 | Stellen Sie sicher, dass Robustheitsmetriken (Erfolgsquote bekannter Angriffssuiten) im Zeitverlauf automatisiert erfasst werden und Regressionen einen Alarm auslösen. |   3   |  D/V  |

### AC.8.3 Inhalts- und Richtlinienprüfung

|    #     | Beschreibung                                                                                                                                                                                                 | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.8.3.1 | Stellen Sie sicher, dass das Screening-Modell oder Regelwerk mindestens vierteljährlich neu trainiert/aktualisiert wird, wobei neu beobachtete Jailbreak- oder Richtlinienumgehungsmuster einbezogen werden. |   2   |   D   |

### AC.8.4 Eingabebegrenzung & Missbrauchsprävention

|    #     | Beschreibung                                                                                                                  | Ebene | Rolle |
| :------: | ----------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.8.4.1 | Stellen Sie sicher, dass Protokolle zur Missbrauchsprävention aufbewahrt und auf aufkommende Angriffsmuster überprüft werden. |   3   |   V   |

### AC.8.5 Eingabeherkunft und Attribution

|    #     | Beschreibung                                                                                                                                                      | Ebene | Rolle |
| :------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.8.5.1 | Verifizieren Sie, dass alle Benutzereingaben bei der Erfassung mit Metadaten (Benutzer-ID, Sitzung, Quelle, Zeitstempel, IP-Adresse) gekennzeichnet sind.         |   1   |  D/V  |
| AC.8.5.2 | Stellen Sie sicher, dass Herkunftsmetadaten für alle verarbeiteten Eingaben erhalten bleiben und überprüfbar sind.                                                |   2   |  D/V  |
| AC.8.5.3 | Stellen Sie sicher, dass anomale oder nicht vertrauenswürdige Eingabequellen gekennzeichnet und einer verstärkten Überprüfung oder Blockierung unterzogen werden. |   2   |  D/V  |

---

## AC.9 Multimodale Validierung, MLOps & Infrastruktur-Governance

### AC.9.1 Multimodale Sicherheitsvalidierungspipeline

|    #     | Beschreibung                                                                                                                                                                                                                                                                   | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.9.1.1 | Überprüfen Sie, ob modalitätsspezifische Inhaltsklassifikatoren gemäß den dokumentierten Zeitplänen (mindestens vierteljährlich) mit neuen Bedrohungsmustern, adversarialen Beispielen und Leistungsbenchmarks, die über den Basisschwellenwerten liegen, aktualisiert werden. |   3   |  D/V  |

### AC.9.2 CI/CD- und Build-Sicherheit

|    #     | Beschreibung                                                                                                                                                       | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.9.2.1 | Stellen Sie sicher, dass Infrastructure-as-Code bei jedem Commit gescannt wird und dass Zusammenführungen bei kritischen oder Hochrisikobefunden blockiert werden. |   1   |  D/V  |
| AC.9.2.2 | Stellen Sie sicher, dass CI/CD-Pipelines kurzlebige, eingeschränkte Identitäten für den Zugriff auf Geheimnisse und die Infrastruktur verwenden.                   |   2   |  D/V  |
| AC.9.2.3 | Überprüfen Sie, dass Build-Umgebungen von Produktionsnetzwerken und -daten isoliert sind.                                                                          |   2   |  D/V  |

### AC.9.3 Container- und Bildsicherheit

|    #     | Beschreibung                                                                                                                                                                                                       | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.9.3.1 | Überprüfen Sie, ob Container-Images gescannt werden, um das Vorhandensein von fest codierten Geheimnissen (z. B. API-Schlüssel, Anmeldeinformationen, Zertifikate) zu blockieren.                                  |   2   |  D/V  |
| AC.9.3.2 | Stellen Sie sicher, dass Container-Images gemäß den organisatorischen Zeitplänen gescannt werden, wobei CRITICAL Schwachstellen die Bereitstellung basierend auf den organisatorischen Risikoschwellen blockieren. |   1   |  D/V  |

### AC.9.4 Überwachung, Alarmierung & SIEM

|    #     | Beschreibung                                                                                                                                                                                        | Ebene | Rolle |
| :------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.4.1 | Überprüfen Sie, dass Sicherheitswarnungen mit SIEM-Plattformen (Splunk, Elastic oder Sentinel) unter Verwendung von CEF- oder STIX/TAXII-Formaten mit automatischer Anreicherung integriert werden. |   2   |   V   |

### AC.9.5 Schwachstellenmanagement

|    #     | Beschreibung                                                                                                                                                                                             | Ebene | Rolle |
| :------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.5.1 | Überprüfen Sie, dass Schwachstellen mit HOHER Schwere gemäß den zeitlichen Vorgaben des organisatorischen Risikomanagements gepatcht werden, einschließlich Notfallverfahren für aktiv ausgenutzte CVEs. |   2   |  D/V  |

### AC.9.6 Konfigurations- und Driftkontrolle

|    #     | Beschreibung                                                                                                                                                                                                                            | Ebene | Rolle |
| :------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.6.1 | Stellen Sie sicher, dass Konfigurationsabweichungen mithilfe von Tools (Chef InSpec, AWS Config) gemäß den Überwachungsanforderungen der Organisation erkannt werden, mit automatischer Rücksetzung bei nicht autorisierten Änderungen. |   2   |  D/V  |

### AC.9.7 Härtung der Produktionsumgebung

|    #     | Beschreibung                                                                                                                                                                                                | Ebene | Rolle |
| :------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.7.1 | Stellen Sie sicher, dass Produktionsumgebungen den SSH-Zugang blockieren, Debug-Endpunkte deaktivieren und Änderungsanfragen mit organisatorischen Vorankündigungsanforderungen außer im Notfall verlangen. |   2   |  D/V  |

### AC.9.8 Veröffentlichungspromotion-Gates

|    #     | Beschreibung                                                                                                                                                                                            | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.8.1 | Stellen Sie sicher, dass die Freigabetore automatisierte Sicherheitstests (SAST, DAST, Container-Scans) enthalten, wobei für die Genehmigung keine kritischen Befunde (CRITICAL Findings) erlaubt sind. |   2   |  D/V  |

### AC.9.9 Überwachung von Arbeitslast, Kapazität und Kosten

|    #     | Beschreibung                                                                                                                                                                                                                                           | Ebene | Rolle |
| :------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.9.9.1 | Überprüfen Sie, ob die GPU/TPU-Auslastung überwacht wird, wobei bei organisatorisch definierten Schwellenwerten Warnungen ausgelöst und basierend auf Kapazitätsmanagementrichtlinien eine automatische Skalierung oder Lastverteilung aktiviert wird. |   1   |  D/V  |
| AC.9.9.2 | Verifizieren Sie, dass KI-Arbeitslastmetriken (Inference-Latenz, Durchsatz, Fehlerraten) gemäß den organisatorischen Überwachungsanforderungen erfasst und mit der Infrastrukturnutzung korreliert werden.                                             |   1   |  D/V  |
| AC.9.9.3 | Überprüfen Sie, ob die Kostenüberwachung die Ausgaben pro Arbeitslast/Mieter verfolgt, mit Benachrichtigungen basierend auf organisatorischen Budgetgrenzen und automatisierten Kontrollen für Budgetüberschreitungen.                                 |   2   |   V   |
| AC.9.9.4 | Stellen Sie sicher, dass die Kapazitätsplanung historische Daten verwendet, die mit organisatorisch definierten Prognosezeiträumen übereinstimmen, und eine automatisierte Ressourcenbereitstellung basierend auf Nachfrage­mustern erfolgt.           |   3   |   V   |

### AC.9.10 Genehmigungen & Audit-Trails

|     #     | Beschreibung                                                                                                                                                                                      | Ebene | Rolle |
| :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.10.1 | Überprüfen Sie, dass die Förderung der Umgebung die Genehmigung von organisatorisch definiertem autorisiertem Personal mit kryptografischen Signaturen und unveränderlichen Prüfpfaden erfordert. |   1   |  D/V  |

### AC.9.11 IaC-Governance

|     #     | Beschreibung                                                                                                                                                                                     | Ebene | Rolle |
| :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| AC.9.11.1 | Stellen Sie sicher, dass Änderungen an Infrastructure-as-Code vor dem Zusammenführen in den Hauptzweig einer Peer-Überprüfung mit automatisiertem Testen und Sicherheitsscans unterzogen werden. |   2   |  D/V  |

### AC.9.12 Datenverarbeitung in Nicht-Produktionsumgebungen

|     #     | Beschreibung                                                                                                                                                                                                                                                   | Ebene | Rolle |
| :-------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.12.1 | Überprüfen Sie, ob Nicht-Produktionsdaten gemäß den organisatorischen Datenschutzanforderungen anonymisiert sind, synthetische Datengenerierung erfolgt oder eine vollständige Datenmaskierung mit Entfernung personenbezogener Daten (PII) verifiziert wurde. |   2   |  D/V  |

### AC.9.13 Datensicherung & Katastrophenwiederherstellung

|     #     | Beschreibung                                                                                                                                                                                                                        | Ebene | Rolle |
| :-------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.13.1 | Überprüfen Sie, ob Infrastrukturkonfigurationen gemäß den organisatorischen Sicherungsplänen in geografisch getrennte Regionen mit der Umsetzung der 3-2-1-Sicherungsstrategie gesichert werden.                                    |   1   |  D/V  |
| AC.9.13.2 | Stellen Sie sicher, dass Wiederherstellungsverfahren gemäß den organisatorischen Zeitplänen mit RTO- und RPO-Zielen, die den organisatorischen Anforderungen entsprechen, durch automatisierte Tests getestet und validiert werden. |   2   |   V   |
| AC.9.13.3 | Stellen Sie sicher, dass die Katastrophenwiederherstellung KI-spezifische Runbooks mit der Wiederherstellung der Modellgewichte, dem Wiederaufbau des GPU-Clusters und der Abbildung von Dienstabhängigkeiten umfasst.              |   3   |   V   |

### AC.9.14 Einhaltung & Dokumentation

|     #     | Beschreibung                                                                                                                                                                                                            | Ebene | Rolle |
| :-------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.14.1 | Stellen Sie sicher, dass die Einhaltung der Infrastruktur gemäß den organisatorischen Zeitplänen gegenüber SOC 2-, ISO 27001- oder FedRAMP-Kontrollen bewertet wird, wobei die Beweiserfassung automatisiert erfolgt.   |   2   |  D/V  |
| AC.9.14.2 | Stellen Sie sicher, dass die Infrastrukturdokumentation Netzwerktopologien, Datenflusskarten und Bedrohungsmodelle enthält, die gemäß den Anforderungen des organisatorischen Änderungsmanagements aktualisiert wurden. |   2   |   V   |
| AC.9.14.3 | Stellen Sie sicher, dass Infrastrukturänderungen einer automatisierten Compliance-Auswirkungsbewertung unterzogen werden, einschließlich regulatorischer Genehmigungsprozesse für risikoreiche Änderungen.              |   3   |  D/V  |

### AC.9.15 Hardware & Lieferkette

|     #     | Beschreibung                                                                                                                                                                                                      | Ebene | Rolle |
| :-------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.15.1 | Stellen Sie sicher, dass die Firmware der KI-Beschleuniger (GPU-BIOS, TPU-Firmware) mit kryptografischen Signaturen überprüft und gemäß den Zeitplänen des organisatorischen Patch-Managements aktualisiert wird. |   2   |  D/V  |
| AC.9.15.2 | Stellen Sie sicher, dass die Lieferkette der KI-Hardware eine Herkunftsprüfung mit Herstellerzertifikaten und eine Validierung der manipulationssicheren Verpackung umfasst.                                      |   3   |   V   |

### AC.9.16 Cloud-Strategie & Portabilität

|     #     | Beschreibung                                                                                                                                                                                                                       | Ebene | Rolle |
| :-------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.16.1 | Stellen Sie sicher, dass die Vermeidung von Cloud-Anbieterbindung portierbare Infrastructure-as-Code, standardisierte APIs und Datenexportfunktionen mit Formatkonvertierungswerkzeugen umfasst.                                   |   3   |   V   |
| AC.9.16.2 | Verifizieren Sie, dass die Multi-Cloud-Kostenoptimierung Sicherheitskontrollen beinhaltet, die sowohl die Ausbreitung von Ressourcen verhindern als auch unautorisierte Kosten für Datenübertragungen zwischen Clouds unterbinden. |   3   |   V   |

### AC.9.17 GitOps & Selbstheilung

|     #     | Beschreibung                                                                                                                                                                           | Ebene | Rolle |
| :-------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.17.1 | Überprüfen Sie, dass GitOps-Repositories signierte Commits mit GPG-Schlüsseln erfordern und Branch-Schutzregeln vorhanden sind, die direkte Pushes auf Hauptbranches verhindern.       |   2   |  D/V  |
| AC.9.17.2 | Verifizieren Sie, dass die selbstheilende Infrastruktur Sicherheitsereigniskorrelation mit automatisierter Vorfallreaktion und Workflows zur Benachrichtigung der Stakeholder umfasst. |   3   |   V   |

### AC.9.18 Zero-Trust, Agenten, Bereitstellung & Ansässigkeitsbescheinigung

|     #     | Beschreibung                                                                                                                                                                                             | Ebene | Rolle |
| :-------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| AC.9.18.1 | Stellen Sie sicher, dass der Zugriff auf Cloud-Ressourcen eine Zero-Trust-Verifizierung mit kontinuierlicher Authentifizierung umfasst.                                                                  |   2   |  D/V  |
| AC.9.18.2 | Stellen Sie sicher, dass die automatisierte Infrastrukturbereitstellung eine Sicherheitsrichtlinienvalidierung einschließt, wobei die Bereitstellung bei nicht konformen Konfigurationen blockiert wird. |   2   |  D/V  |
| AC.9.18.3 | Stellen Sie sicher, dass die automatisierte Infrastruktur-Bereitstellung die Sicherheitsrichtlinien während CI/CD validiert und nicht konforme Konfigurationen von der Bereitstellung blockiert werden.  |   2   |  D/V  |
| AC.9.18.4 | Überprüfen Sie, dass die Anforderungen an den Datenaufenthalt durch kryptografische Bescheinigung der Speicherorte durchgesetzt werden.                                                                  |   3   |  D/V  |
| AC.9.18.5 | Überprüfen Sie, ob die Sicherheitsbewertungen des Cloud-Anbieters agentenspezifisches Bedrohungsmodellieren und Risikoanalysen enthalten.                                                                |   3   |  D/V  |

### AC.9.19 Zugangskontrolle & Identität

|   #   | Beschreibung                                                                                                                                                                                                                         | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 5.1.3 | Stellen Sie sicher, dass neue Hauptverantwortliche eine Identitätsprüfung durchlaufen, die mit NIST 800-63-3 IAL-2 oder gleichwertigen Standards übereinstimmt, bevor sie Zugriff auf das Produktionssystem erhalten.                |   2   |   D   |
| 5.1.4 | Stellen Sie sicher, dass Zugriffsüberprüfungen vierteljährlich durchgeführt werden, einschließlich automatischer Erkennung inaktiver Konten, Durchsetzung der Anmeldeinformationen-Rotation und Workflows zur De-Provisionierung.    |   2   |   V   |
| 5.2.2 | Überprüfen Sie, dass das Prinzip der minimalen Berechtigungen bei Dienstkonten standardmäßig durchgesetzt wird, beginnend mit Lesezugriff und dass eine dokumentierte geschäftliche Begründung für Schreibzugriffe erforderlich ist. |   1   |  D/V  |
| 5.3.3 | Stellen Sie sicher, dass Richtliniendefinitionen versionskontrolliert, von Kollegen geprüft und durch automatisierte Tests in CI/CD-Pipelines validiert werden, bevor sie in der Produktion bereitgestellt werden.                   |   2   |   D   |
| 5.3.4 | Stellen Sie sicher, dass die Ergebnisse der Richtlinienbewertung Entscheidungsbegründungen enthalten und an SIEM-Systeme zur Korrelationsanalyse und Compliance-Berichterstattung übermittelt werden.                                |   2   |   V   |
| 5.4.4 | Stellen Sie sicher, dass die Latenz bei der Richtlinienbewertung kontinuierlich überwacht wird und automatisierte Warnungen für Zeitüberschreitungsbedingungen vorliegen, die eine Umgehung der Autorisierung ermöglichen könnten.   |   2   |   V   |
| 5.5.4 | Stellen Sie sicher, dass Schwärzungsalgorithmen deterministisch, versionskontrolliert sind und Audit-Protokolle führen, um Compliance-Untersuchungen und forensische Analysen zu unterstützen.                                       |   2   |   V   |
| 5.5.5 | Überprüfen Sie, dass Hochrisiko-Schwärzungsereignisse adaptive Protokolle erzeugen, die kryptographische Hashes des Originalinhalts für die forensische Wiederherstellung ohne Datenexposition enthalten.                            |   3   |   V   |
| 5.7.5 | Stellen Sie sicher, dass Agentenfehlerbedingungen und Ausnahmebehandlungen Informationen zum Fähigkeitsbereich enthalten, um die Vorfallanalyse und forensische Untersuchung zu unterstützen.                                        |   3   |   V   |
| 5.4.2 | Stellen Sie sicher, dass Zitate, Verweise und Quellenangaben in Modellausgaben anhand der Berechtigungen des Anrufers überprüft und entfernt werden, wenn unautorisierter Zugriff festgestellt wird.                                 |   1   |  D/V  |

### Neue Elemente, die oben integriert werden sollen

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                         | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 2.3.1 | Stellen Sie sicher, dass der erlaubte Zeichensatz regelmäßig überprüft und aktualisiert wird, um sicherzustellen, dass er weiterhin den geschäftlichen Anforderungen entspricht.                                                                                                                                                                                                                                     |   2   |  D/V  |
| 7.2.4 | Stellen Sie sicher, dass Schwellenwerte und Detektoren nach größeren Modell- oder Wissensbasis-Updates neu kalibriert werden.                                                                                                                                                                                                                                                                                        |   3   |  D/V  |
| 7.2.5 | Überprüfen Sie, ob Dashboard-Visualisierungen die Halluzinationsraten verfolgen.                                                                                                                                                                                                                                                                                                                                     |   3   |   V   |
| 7.5.4 | Stellen Sie sicher, dass Erklärbarkeitsartefakte zusammen mit Modellversionen versioniert werden, um die Prüfbarkeit zu gewährleisten.                                                                                                                                                                                                                                                                               |   3   |   V   |
| 7.6.5 | Stellen Sie sicher, dass Überwachungspipelines einem Penetrationstest unterzogen und zugriffskontrolliert sind, um das Austreten sensibler Protokolle zu vermeiden.                                                                                                                                                                                                                                                  |   3   |   V   |
| 7.6.4 | Überprüfen Sie, ob Überwachungsdaten in einem dokumentierten MLOps-Workflow in die Nachschulung, Feinabstimmung oder Regelaktualisierungen zurückfließen.                                                                                                                                                                                                                                                            |   2   |  D/V  |
| 9.5.4 | Stellen Sie sicher, dass Protokollimplementierungen einer Fuzzing- und statischen Analyse unterzogen werden, die sich auf Deserialisierung, Injektion, Request Smuggling und Randfälle von Zustandsautomaten konzentriert.                                                                                                                                                                                           |   3   |   V   |
| 9.7.4 | Überprüfen Sie, ob das System bei Erkennung einer Absichtsunstimmigkeit oder eines Verstoßes gegen Richtlinien/Kontraintents den Vorfall protokolliert, das zuständige Team alarmiert und den Vorfall nutzt, um die Verteidigungsmaßnahmen zu verbessern (Tests hinzufügen/aktualisieren, Richtlinien verschärfen und Erkennungsregeln aktualisieren), damit derselbe Fehler weniger wahrscheinlich erneut auftritt. |   3   |  D/V  |
| 9.8.3 | Stellen Sie sicher, dass CI/CD eigenschaftsbasierte Tests oder gleichwertige Analysen für Multi-Agenten-Protokolle umfasst, um begrenztes Verhalten und wichtige Sicherheitsinvarianten nachzuweisen (z. B. keine domänenübergreifende Nachrichtenübermittlung, keine unbegrenzte Verzweigung).                                                                                                                      |   3   |   V   |

### C8-Speicher, Einbettungen und Sicherheit von Vektordatenbanken

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 8.1.4 | Überprüfen Sie, ob die Audit-Protokolle der Vektor-Datenbank folgende Informationen aufzeichnen: authentifizierter Benutzer, Mandanten-/Benutzerebene, Operationstyp, Sammlung/Namensraum, Abfragefilter, Ähnlichkeitsschwelle/top-k und Ergebnisanzahl.                                                                                                              |   2   |  D/V  |
| 8.1.4 | Überprüfen Sie, dass automatisierte Tests die Autorisierung und Durchsetzung des Geltungsbereichs (einschließlich negativer Tests) validieren, wann immer der Vektor-Engine, die Indexeinstellungen oder die Sharding-/Partitionierungsregeln geändert werden.                                                                                                        |   3   |   V   |
| 8.2.3 | Stellen Sie sicher, dass bei der Verwendung von datenschutzfördernden Transformationen für Einbettungen (z. B. Differential Privacy, Projektion oder Rauschmechanismen) der gewählte Mechanismus und die Parameter dokumentiert, versionskontrolliert und mithilfe eines definierten Testgerüsts empirisch auf Datenschutz-/Nützlichkeitskompromisse bewertet werden. |   2   |  D/V  |
| 8.2.4 | Überprüfen Sie, ob die Wirksamkeit der Bereinigung anhand von Benchmark-Korpora und internen Stichproben gemessen wird, wobei mindestens folgende Kriterien verfolgt werden: Erkennungs-/Entfernungsrate von personenbezogenen Daten (PII), Fehlalarme und semantische Abweichungen/Nutzungsbeeinträchtigung.                                                         |   2   |   V   |
| 8.4.1 | Stellen Sie sicher, dass für jede Speicher-/RAG-Bereitstellung ein Bedrohungsmodell für das Auslaufen von Einbettungen (Inversion, Mitgliedschaftsinferenz, Attributinferenz) existiert und dieses in einem definierten Turnus (z. B. jährlich) sowie nach wesentlichen Architekturänderungen überprüft wird.                                                         |   1   |   V   |
| 8.4.4 | Überprüfen Sie, dass Tests zum Aufdecken von Embedding-Lecks (z. B. Umkehrversuche oder Mitgliedschaftsinferenzprüfungen, die für das System geeignet sind) Teil der Freigabekriterien für hochsensible Einsätze sind, mit dokumentierten Bestehens-/Nichtbestehens-Kriterien und Trendverfolgung über die Zeit.                                                      |   3   |  D/V  |
| 8.6.1 | Stellen Sie sicher, dass jeder Speichertyp (episodisch, semantisch, arbeitsgedächtnis) einen explizit definierten Sicherheitskontext aufweist: unterschiedliche Bereiche, unterschiedliche Zugriffsrichtlinien und unterschiedliche Verschlüsselungsschlüssel (oder gleichwertige Isolationskontrollen).                                                              |   1   |  D/V  |
| 8.6.2 | Stellen Sie sicher, dass Memory-Konsolidierungspipelines (Zusammenfassung, Zusammenführung, Destillation) den Inhalt vor der Speicherung validieren und bereinigen, einschließlich prompt-injektionsartiger Anweisungen und von Tools erzeugter Artefakte.                                                                                                            |   2   |  D/V  |
| 8.6.3 | Stellen Sie sicher, dass Speicherabrufe abgefragt werden, um Extraktionsmuster (z. B. iterative Top-k-Abfrage, Ähnlichkeitsabfrage) zu verhindern, und dass diese durch Ratenbegrenzungen und Anomalieerkennung kontrolliert werden.                                                                                                                                  |   2   |  D/V  |
| 8.6.4 | Stellen Sie sicher, dass „Vergessens“-Operationen (Löschen / Zurückziehen) konsequent über alle Speichertypen, abgeleiteten Indizes, Caches und Backups hinweg durchgesetzt werden, mit überprüfbaren Nachweisen über den Abschluss.                                                                                                                                  |   3   |  D/V  |
| 8.6.5 | Überprüfen Sie, dass die Integritätsüberwachung unautorisierte Änderungen an Speicherinhalten und Indexierungsstrukturen erkennt (Prüfsummen, Prüfprotokolle, Alarmierung bei unerwarteten Schreibquellen).                                                                                                                                                           |   3   |  D/V  |

