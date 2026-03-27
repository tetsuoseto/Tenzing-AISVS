# C11 Gegnerische Robustheit und Datenschutzabwehr

## Kontrollziel

Stellen Sie sicher, dass KI-Modelle zuverlässig, datenschutzwahrend und missbrauchsresistent bleiben, wenn sie Angriffen wie Umgehung, Inferenz, Extraktion oder Vergiftung ausgesetzt sind.

---

## C11.1 Modellabstimmung & Sicherheit

Schützen Sie vor schädlichen oder gegen Richtlinien verstoßenden Ausgaben.

|   #    | Beschreibung                                                                                                                                                                                           | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 11.1.1 | Stellen Sie sicher, dass eine Alignment-Test-Suite (Red-Team-Eingabeaufforderungen, Jailbreak-Prüfungen, nicht erlaubte Inhalte) versionskontrolliert ist und bei jeder Modellversion ausgeführt wird. |   1   |  D/V  |
| 11.1.2 | Überprüfen Sie, ob Verweigerungs- und sichere Abschluss-Grenzwerte durchgesetzt werden.                                                                                                                |   1   |   D   |
| 11.1.3 | Überprüfen Sie, ob ein automatisierter Evaluator die Rate schädlicher Inhalte misst und Rückschritte über einem festgelegten Schwellenwert markiert.                                                   |   2   |  D/V  |
| 11.1.4 | Stellen Sie sicher, dass das Training zur Gegenmaßnahmen gegen Jailbreaks dokumentiert und reproduzierbar ist.                                                                                         |   2   |   D   |
| 11.1.5 | Überprüfen Sie, ob formelle Nachweise der Richtlinienkonformität oder zertifizierte Überwachungen kritische Bereiche abdecken.                                                                         |   3   |   V   |

---

## C11.2 Härtung gegen adversariale Beispiele

Erhöhen Sie die Robustheit gegenüber manipulierten Eingaben. Robustes adversariales Training und Benchmark-Bewertungen sind derzeit die bewährten Methoden.

|   #    | Beschreibung                                                                                                                                      | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.2.1 | Überprüfen Sie, ob die Projekt-Repositories adversariale Trainingskonfigurationen mit reproduzierbaren Seeds enthalten.                           |   1   |   D   |
| 11.2.2 | Stellen Sie sicher, dass die Erkennung von adversarialen Beispielen in Produktions-Pipelines Blockierungswarnungen auslöst.                       |   2   |  D/V  |
| 11.2.4 | Verifizieren Sie, dass zertifizierte Robustheitsnachweise oder Intervall-Grenzzertifikate mindestens die wichtigsten kritischen Klassen abdecken. |   3   |   V   |
| 11.2.5 | Überprüfen Sie, dass Regressions tests adaptive Angriffe verwenden, um keinen messbaren Robustheitsverlust zu bestätigen.                         |   3   |   V   |

---

## C11.3 Mitgliedschaftsinferenz-Minderung

Begrenzen Sie die Möglichkeit zu entscheiden, ob ein Datensatz im Trainingsdatensatz enthalten war. Differentielle Privatsphäre und Maskierung des Konfidenz-Scores bleiben die bekanntesten und effektivsten Schutzmaßnahmen.

|   #    | Beschreibung                                                                                                                          | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.3.1 | Überprüfen Sie, ob die Entropieregulierung pro Abfrage oder das Temperatur-Skalieren übermäßig zuversichtliche Vorhersagen reduziert. |   1   |   D   |
| 11.3.2 | Stellen Sie sicher, dass das Training für sensible Datensätze eine ε-begrenzte differentielle private Optimierung verwendet.          |   2   |   D   |
| 11.3.3 | Überprüfen Sie, dass Angriffssimulationen (Shadow-Model oder Black-Box) einen Angriff AUC ≤ 0,60 auf zurückgehaltenen Daten zeigen.   |   2   |   V   |

---

## C11.4 Widerstand gegen Modellinversion

Verhindern Sie die Rekonstruktion privater Attribute. Neuere Untersuchungen betonen Ausgabeabschnittung und DP-Garantien als praktikable Schutzmaßnahmen.

|   #    | Beschreibung                                                                                                                                | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.4.1 | Stellen Sie sicher, dass sensible Attribute niemals direkt ausgegeben werden; verwenden Sie bei Bedarf Buckets oder Einwegtransformationen. |   1   |   D   |
| 11.4.2 | Überprüfen Sie, ob die Abfrage-Ratenbegrenzungen wiederholte adaptive Abfragen vom selben Principal drosseln.                               |   1   |  D/V  |
| 11.4.3 | Verifizieren Sie, dass das Modell mit datenschutzfreundlichem Rauschen trainiert wurde.                                                     |   2   |   D   |

---

## C11.5 Modell-Extraktionsabwehr

Erkennen und Verhindern von unbefugtem Klonen. Wasserzeichen und Analyse von Abfrage-Mustern werden empfohlen.

|   #    | Beschreibung                                                                                                                                                          | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.5.1 | Stellen Sie sicher, dass Inferenz-Gateways globale und pro-API-Schlüssel Ratenbegrenzungen durchsetzen, die auf die Memorierungsschwelle des Modells abgestimmt sind. |   1   |   D   |
| 11.5.2 | Überprüfen Sie, ob die Statistiken zur Abfrage-Entropie und Eingabe-Mehrzahligkeit einen automatisierten Extraktionsdetektor speisen.                                 |   2   |  D/V  |
| 11.5.3 | Überprüfen Sie, dass fragile oder probabilistische Wasserzeichen mit p < 0,01 in ≤ 1 000 Abfragen gegen einen verdächtigten Klon bewiesen werden können.              |   2   |   V   |
| 11.5.4 | Überprüfen Sie, dass Wasserzeichen-Schlüssel und Auslöse-Sätze in einem Hardware-Sicherheitsmodul gespeichert und jährlich rotiert werden.                            |   3   |   D   |
| 11.5.5 | Stellen Sie sicher, dass Extraction-Alert-Ereignisse die verursachenden Abfragen enthalten und in Incident-Response-Playbooks integriert sind.                        |   3   |   V   |

---

## C11.6 Erkennung von zur Inferenzzeit vergifteten Daten

Identifizieren und Neutralisieren von mit Hintertüren verseuchten oder vergifteten Eingaben.

|   #    | Beschreibung                                                                                                                                                                                   | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.6.1 | Überprüfen Sie, ob Eingaben vor der Modellauswertung einen Anomalie-Detektor (z. B. STRIP, Konsistenzbewertung) durchlaufen.                                                                   |   1   |   D   |
| 11.6.2 | Überprüfen Sie, dass die Schwellenwerte des Detektors auf sauberen/verseuchten Validierungsdatensätzen so eingestellt sind, dass weniger als 5 % Fehlalarme (False Positives) erreicht werden. |   1   |   V   |
| 11.6.3 | Überprüfen Sie, ob als vergiftet markierte Eingaben Soft-Blocking und menschliche Prüfprozesse auslösen.                                                                                       |   2   |   D   |
| 11.6.4 | Stellen Sie sicher, dass Detektoren mit adaptiven, triggerlosen Backdoor-Angriffen auf Belastungsprobe getestet werden.                                                                        |   2   |   V   |
| 11.6.5 | Stellen Sie sicher, dass Metriken zur Erkennungseffizienz protokolliert und regelmäßig mit aktuellen Bedrohungsinformationen neu bewertet werden.                                              |   3   |   D   |

---

## C11.7 Dynamische Anpassung der Sicherheitsrichtlinie

Echtzeit-Sicherheitsrichtlinienaktualisierungen basierend auf Bedrohungsinformationen und Verhaltensanalysen.

|   #    | Beschreibung                                                                                                                                                                            | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.7.1 | Überprüfen Sie, dass Sicherheitsrichtlinien dynamisch aktualisiert werden können, ohne den Agenten neu zu starten, und dabei die Integrität der Richtlinienversion erhalten bleibt.     |   1   |  D/V  |
| 11.7.2 | Überprüfen Sie, dass Richtlinienaktualisierungen kryptografisch von autorisiertem Sicherheitspersonal signiert und vor der Anwendung validiert werden.                                  |   2   |  D/V  |
| 11.7.3 | Stellen Sie sicher, dass dynamische Richtlinienänderungen mit vollständigen Audit-Trails protokolliert werden, einschließlich Begründung, Genehmigungsketten und Rücksetzungsverfahren. |   2   |  D/V  |
| 11.7.4 | Überprüfen Sie, ob adaptive Sicherheitsmechanismen die Empfindlichkeit der Bedrohungserkennung basierend auf dem Risikokontext und Verhaltensmustern anpassen.                          |   3   |  D/V  |
| 11.7.5 | Stellen Sie sicher, dass Entscheidungen zur Richtlinienanpassung erklärbar sind und Nachweise für die Überprüfung durch das Sicherheitsteam enthalten.                                  |   3   |  D/V  |

---

## C11.8 Reflexionsbasierte Sicherheitsanalyse

Sicherheitsvalidierung durch Agenten-Selbstreflexion und metakognitive Analyse.

|   #    | Beschreibung                                                                                                                                                          | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.8.1 | Überprüfen Sie, ob Agenten-Reflexionsmechanismen eine sicherheitsorientierte Selbstbewertung von Entscheidungen und Handlungen umfassen.                              |   1   |  D/V  |
| 11.8.2 | Stellen Sie sicher, dass Reflektionsausgaben validiert werden, um die Manipulation von Selbstbewertungsmechanismen durch adversariale Eingaben zu verhindern.         |   2   |  D/V  |
| 11.8.3 | Überprüfen Sie, ob die metakognitive Sicherheitsanalyse potenzielle Voreingenommenheit, Manipulation oder Beeinträchtigung in den Denkprozessen von Agenten erkennt.  |   2   |  D/V  |
| 11.8.4 | Überprüfen Sie, ob sicherheitsbezogene Warnungen auf Basis von Reflection eine erweiterte Überwachung und potenzielle Workflows für menschliches Eingreifen auslösen. |   3   |  D/V  |
| 11.8.5 | Überprüfen Sie, ob kontinuierliches Lernen aus Sicherheitsüberprüfungen die Bedrohungserkennung verbessert, ohne die legitime Funktionalität zu beeinträchtigen.      |   3   |  D/V  |

---

## C11.9 Evolution & Selbstverbesserung Sicherheit

Sicherheitskontrollen für Agentensysteme, die zur Selbstmodifikation und Evolution fähig sind.

|   #    | Beschreibung                                                                                                                                          | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 11.9.1 | Überprüfen Sie, dass Selbstmodifikationsfähigkeiten auf ausgewiesene sichere Bereiche mit formalen Verifikationsgrenzen beschränkt sind.              |   1   |  D/V  |
| 11.9.2 | Stellen Sie sicher, dass Entwicklungsvorschläge vor der Umsetzung einer Sicherheitsauswirkungsbewertung unterzogen werden.                            |   2   |  D/V  |
| 11.9.3 | Verifizieren Sie, dass Selbstverbesserungsmechanismen Rücksetzfunktionen mit Integritätsprüfung umfassen.                                             |   2   |  D/V  |
| 11.9.4 | Überprüfen Sie, ob Meta-Lern-Sicherheit die feindliche Manipulation von Verbesserungsalgorithmen verhindert.                                          |   3   |  D/V  |
| 11.9.5 | Verifizieren Sie, dass rekursive Selbstverbesserung durch formale Sicherheitsbeschränkungen begrenzt ist, mit mathematischen Beweisen der Konvergenz. |   3   |  D/V  |

---

### Literaturverzeichnis

