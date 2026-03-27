# C9 Autonome Orchestrierung & agentische Handlungssicherheit

## Kontrollziel

Autonome und Multi-Agenten-Systeme müssen nur autorisierte, beabsichtigte und begrenzte Aktionen ausführen. Diese Kontrollfamilie reduziert Risiken durch Werkzeugmissbrauch, Privilegieneskalation, unkontrollierte Rekursion/Kostensteigerung, Protokollmanipulation sowie Interferenzen zwischen Agenten oder Mandanten, indem sie Folgendes durchsetzt: explizite Autorisierung, sandboxartige Ausführung, kryptografische Identität und manipulationssichere Auditierung, Nachrichtensicherheit sowie Intent-/Beschränkungstore.

---

## C9.1 Ausführungsbudgets, Schleifensteuerung und Circuit Breakers

Begrenzte Laufzeiterweiterung (Rekursion, Nebenläufigkeit, Kosten) und sicheres Anhalten bei unkontrolliertem Verhalten.

|   #   | Beschreibung                                                                                                                                                                                                                             | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 9.1.1 | Verifizieren Sie, dass pro Ausführung festgelegte Budgets (maximale Rekursionstiefe, maximale Fan-out/Konkurrenz, Echtzeit, Tokens und monetäre Ausgaben) von der Orchestrierungs-Laufzeitumgebung konfiguriert und durchgesetzt werden. |   1   |  D/V  |
| 9.1.2 | Überprüfen Sie, ob kumulative Ressourcen-/Ausgabenzähler pro Anforderungskette verfolgt werden, und stoppen Sie die Kette bei Überschreitung der Schwellenwerte sofort.                                                                  |   2   |  D/V  |
| 9.1.3 | Überprüfen Sie, dass Schutzschalter die Ausführung bei Budgetüberschreitungen beenden.                                                                                                                                                   |   2   |  D/V  |
| 9.1.4 | Stellen Sie sicher, dass die Sicherheitstests ausufernde Schleifen, Budgeterschöpfung und Teilfehler-Szenarien abdecken, um eine sichere Beendigung und einen konsistenten Zustand zu bestätigen.                                        |   3   |   V   |
| 9.1.5 | Stellen Sie sicher, dass Budget- und Circuit-Breaker-Richtlinien als Policy-as-Code ausgedrückt und in der CI/CD validiert werden, um Abweichungen und unsichere Konfigurationsänderungen zu verhindern.                                 |   3   |  D/V  |

---

## C9.2 Genehmigung von Maßnahmen mit hoher Auswirkung und Kontrollmechanismen zur Irreversibilität

Explizite Kontrollpunkte für privilegierte oder irreversible Ergebnisse sind erforderlich.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                    | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 9.2.1 | Stellen Sie sicher, dass privilegierte oder irreversible Aktionen (z. B. Codezusammenführungen/-bereitstellungen, finanzielle Überweisungen, Änderungen des Benutzerzugriffs, destruktive Löschungen, externe Benachrichtigungen) eine ausdrückliche menschliche Freigabe im Prozess erfordern. |   1   |  D/V  |
| 9.2.2 | Überprüfen Sie, ob Genehmigungsanfragen die genauen Aktionsparameter (Diff/Befehl/Empfänger/Betrag/Umfang) enthalten und binden Sie Genehmigungen an diese Parameter, um zu verhindern, dass „eine Sache genehmigt, eine andere ausgeführt“ wird.                                               |   2   |  D/V  |
| 9.2.3 | Überprüfen Sie, dass dort, wo ein Rollback möglich ist, ausgleichende Maßnahmen definiert und getestet sind (transaktionale Semantik) und Fehler ein Rollback oder eine sichere Eingrenzung auslösen.                                                                                           |   3   |   V   |

---

## C9.3 Werkzeug- und Plugin-Isolation und sichere Integration

Beschränken Sie die Ausführung von Tools, das Laden und die Ausgaben, um unbefugten Systemzugriff und unsichere Nebeneffekte zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                                                     | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 9.3.1 | Verifizieren Sie, dass jedes Tool/Plugin in einer isolierten Sandbox (Container/VM/WASM/OS-Sandbox) mit den jeweils geringstmöglichen Berechtigungen für Dateisystem, Netzwerkausgang und Systemaufrufe ausgeführt wird, die der Funktion des Tools entsprechen. |   1   |  D/V  |
| 9.3.2 | Überprüfen Sie, dass pro Tool festgelegte Kontingente und Zeitlimits (CPU, Speicher, Festplatte, Ausgangs-Datenvolumen, Ausführungszeit) eingehalten und protokolliert werden und dass bei Überschreitung der Kontingente ein sicherer Fehlerzustand eintritt.   |   1   |  D/V  |
| 9.3.3 | Überprüfen Sie, ob Tool-Manifeste die erforderlichen Berechtigungen, das Nebenwirkungsniveau, Ressourcengrenzen und Anforderungen an die Ausgabevalidierung deklarieren und ob die Laufzeitumgebung diese Deklarationen durchsetzt.                              |   2   |  D/V  |
| 9.3.4 | Stellen Sie sicher, dass die Ausgaben von Werkzeugen vor der Einbindung in nachgelagerte Schlussfolgerungen oder Folgeaktionen anhand strenger Schemata und Sicherheitsrichtlinien validiert werden.                                                             |   2   |  D/V  |
| 9.3.5 | Stellen Sie sicher, dass Tool-Binärdateien vor dem Laden auf Integrität geschützt und validiert sind.                                                                                                                                                            |   2   |  D/V  |
| 9.3.6 | Überprüfen Sie, ob Sandbox-Escape-Indikatoren oder Richtlinienverstöße eine automatisierte Eindämmung (Werkzeug deaktiviert/quarantänisiert) auslösen.                                                                                                           |   3   |  D/V  |

---

## C9.4 Agenten- und Orchestrator-Identität, Signierung und manipulationssicheres Audit

Machen Sie jede Aktion nachvollziehbar und jede Mutation erkennbar.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                 | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 9.4.1 | Stellen Sie sicher, dass jede Agenteninstanz (und Orchestrator/Laufzeit) eine eindeutige kryptografische Identität besitzt und sich als erstklassiges Prinzipal gegenüber nachgelagerten Systemen authentifiziert (keine Wiederverwendung von Endbenutzer-Anmeldeinformationen).                                                                                                             |   1   |  D/V  |
| 9.4.2 | Überprüfen Sie, dass von Agenten initiierte Aktionen kryptografisch an die Ausführungskette (Chain-ID) gebunden sind und für Nichtabstreitbarkeit sowie Nachvollziehbarkeit signiert und mit Zeitstempel versehen werden.                                                                                                                                                                    |   2   |  D/V  |
| 9.4.3 | Stellen Sie sicher, dass die Prüfprotokolle manipulationssicher sind (nur-anfügen/WORM/unveränderlicher Protokollspeicher) und ausreichenden Kontext enthalten, um zu rekonstruieren, wer/was gehandelt hat, den identifizierenden Benutzer, den Delegationsumfang, die Autorisierungsentscheidung (Richtlinie/Version), Werkzeugparameter, Genehmigungen (falls zutreffend) und Ergebnisse. |   2   |  D/V  |
| 9.4.4 | Überprüfen Sie, dass Agenten-Identitätsnachweise (Schlüssel/Zertifikate/Token) nach einem definierten Zeitplan und bei Hinweisen auf Kompromittierung rotieren, mit schneller Sperrung und Quarantäne bei Verdacht auf Kompromittierung oder Spoofing-Versuche.                                                                                                                              |   3   |  D/V  |

---

## C9.5 Sichere Nachrichtenübermittlung und Protokollhärtung

Schützen Sie die Kommunikation zwischen Agenten sowie zwischen Agent und Tool vor Hijacking, Injektion, Wiedergabe und Desynchronisation.

|   #   | Beschreibung                                                                                                                                                                                                                   | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 9.5.1 | Verifizieren Sie, dass Agent-zu-Agent- und Agent-zu-Tool-Kanäle gegenseitige Authentifizierung und Verschlüsselung mit modernen Protokollen (z. B. TLS 1.3) sowie eine starke Zertifikats-/Token-Validierung durchsetzen.      |   1   |  D/V  |
| 9.5.2 | Stellen Sie sicher, dass alle Nachrichten streng schemavalidiert sind; unbekannte Felder, fehlerhafte Nutzlasten und übergroße Frames werden abgelehnt.                                                                        |   1   |  D/V  |
| 9.5.3 | Stellen Sie sicher, dass die Nachrichtenintegrität die vollständige Nutzlast einschließlich der Werkzeugparameter abdeckt und dass Wiedergabeschutzmechanismen (Nonces/Sequenznummern/Zeitstempelfenster) durchgesetzt werden. |   2   |  D/V  |

---

## C9.6 Autorisierung, Delegation und kontinuierliche Durchsetzung

Stellen Sie sicher, dass jede Aktion zur Ausführungszeit autorisiert und durch den Geltungsbereich eingeschränkt ist.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                              | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 9.6.1 | Überprüfen Sie, ob Agentenaktionen gegen fein granulare Richtlinien autorisiert sind, die von der Laufzeit durchgesetzt werden und einschränken, welche Tools ein Agent aufrufen darf, welche Parameterwerte er angeben darf (z. B. erlaubte Ressourcen, Datenbereiche, Aktionstypen), und dass Richtlinienverletzungen blockiert werden. |   1   |  D/V  |
| 9.6.2 | Stellen Sie sicher, dass die Laufzeitumgebung beim Handeln eines Agenten im Auftrag eines Benutzers einen integritätsgeschützten Delegationskontext (Benutzer-ID, Mandant, Sitzung, Berechtigungen) weitergibt und diesen Kontext bei jedem nachgelagerten Aufruf durchsetzt, ohne die Anmeldeinformationen des Benutzers zu verwenden.   |   2   |  D/V  |
| 9.6.3 | Verifizieren Sie, dass die Autorisierung bei jedem Aufruf (kontinuierliche Autorisierung) unter Verwendung des aktuellen Kontexts (Benutzer, Mandant, Umgebung, Datenklassifizierung, Zeit, Risiko) erneut bewertet wird.                                                                                                                 |   2   |  D/V  |
| 9.6.4 | Stellen Sie sicher, dass alle Zugriffsentscheidungen durch die Anwendungslogik oder eine Richtlinien-Engine durchgesetzt werden, niemals durch das KI-Modell selbst, und dass vom Modell generierte Ausgaben (z. B. „dem Benutzer ist dies erlaubt“) Zugriffsprüfungen nicht überschreiben oder umgehen können.                           |   3   |  D/V  |

---

## C9.7 Absichtsüberprüfung und Einschränkungstore

Verhindern Sie „technisch autorisierte, aber unbeabsichtigte“ Aktionen, indem Sie die Ausführung an die Benutzerabsicht und harte Beschränkungen binden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                         | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 9.7.1 | Überprüfen Sie, dass Vor-Ausführungs-Gates vorgeschlagene Aktionen und Parameter anhand harter Richtlinienbeschränkungen (Verweigerungsregeln, Datenhandhabungsbeschränkungen, Positivlisten, Nebenwirkungsbudgets) bewerten und die Ausführung bei jeglicher Verletzung blockieren. |   1   |  D/V  |
| 9.7.2 | Stellen Sie sicher, dass hochwirksame Aktionen eine explizite Benutzerabsichtserklärung erfordern, die integritätsschutzgesichert ist und an die genauen Aktionsparameter gebunden ist (und schnell verfällt), um veraltete oder ausgetauschte Genehmigungen zu verhindern.          |   2   |  D/V  |
| 9.7.3 | Überprüfen Sie, ob Nachbedingungsprüfungen das beabsichtigte Ergebnis bestätigen und unbeabsichtigte Nebeneffekte erkennen; jede Abweichung löst eine Eindämmung (und gegebenenfalls ausgleichende Maßnahmen) aus.                                                                   |   2   |   V   |

---

## C9.8 Mehragentige Domänenisolation und Schwarm-Risikokontrollen

Reduzieren Sie Interferenzen zwischen verschiedenen Domänen und aufkommendes unsicheres kollektives Verhalten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 9.8.1 | Stellen Sie sicher, dass Agenten in verschiedenen Mandanten, Sicherheitsdomänen oder Umgebungen (Entwicklung/Test/Produktion) in isolierten Laufzeitumgebungen und Netzwerksegmenten ausgeführt werden, mit Standard-Deny-Kontrollen, die eine domänenübergreifende Erkennung und Aufrufe verhindern. |   1   |  D/V  |
| 9.8.2 | Überprüfen Sie, ob die Laufzeitüberwachung unsicheres emergentes Verhalten (Oszillation, Deadlocks, unkontrollierte Broadcasts, abnormale Aufrufgraphen) erkennt und automatisch Korrekturmaßnahmen anwendet (Drosselung, Isolierung, Beendigung).                                                    |   3   |  D/V  |

---

## Literaturverzeichnis

* [NIST SP 800-207: Zero Trust Architecture](https://csrc.nist.gov/publications/detail/sp/800-207/final)

