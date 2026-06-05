# Anhang D: Bestand an AI-Sicherheitskontrollen

## Ziel

Dieser Anhang stellt ein kompaktes Verzeichnis aller Sicherheitskontrollen und Abwehrtechniken bereit, die in den AISVS-Anforderungen genannt werden. Die Kontrollen sind nach Kategorien von Sicherheitskontrollen gruppiert, sodass Implementierer alle zugehörigen Abwehrmaßnahmen an einem Ort finden können, unabhängig davon, in welchem AISVS-Kapitel sie definiert sind.

---

## AD.1 Authentifizierung

Überprüfen Sie die Identität von Benutzern, Agenten, Diensten, MCP-Clients/Servern und Edge-Geräten, bevor Sie Zugriff gewähren.

| Control / Technik                                                                                                                   | Anforderungs-IDs |
| ----------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Stufenweise Authentifizierung für risikoreiche KI-Vorgänge (Modellbereitstellung, Export von Gewichten, Zugriff auf Trainingsdaten) | 5.1.1            |
| Kurzlebige signierte Tokens für die föderierte KI-Agenten-Authentifizierung                                                         | 5.1.2            |
| Eindeutige kryptografische Agent- und Orchestrator-Identität                                                                        | 9.4.1            |
| Erstklassige Principal-Authentifizierung (keine Wiederverwendung von Endbenutzer-Anmeldeinformationen)                              | 9.4.1            |
| Agentenidentitätsnachweis-Rotation und schnelle Sperrung                                                                            | 9.4.5            |
| OAuth 2.1 für die Client-Authentifizierung von MCP                                                                                  | 10.2.1           |
| MCP-Server OAuth-Token-Validierung (Aussteller, Zielgruppe, Ablaufzeit, Geltungsbereich)                                            | 10.2.2           |
| MCP-Serverregistrierung mit explizitem Eigentum                                                                                     | 10.2.4           |
| Kryptografisch sichere MCP-Sitzungs-IDs (nicht für Authentifizierung verwendet)                                                     | 10.2.8           |

Häufige Fallstricke: das Wiederverwenden von Endbenutzer-Anmeldeinformationen für Agent-zu-Agent-Aufrufe; die Verwendung von MCP-Sitzungs-IDs als Authentifizierungstokens; das Nichtrotieren von Agent-Anmeldeinformationen bei vermutetem Kompromittieren.

---

## AD.2 Autorisierung & Zugriffskontrolle

Setzen Sie Zugriffsentscheidungen über Benutzer, Agenten, Tools, Daten und MCP-Ressourcen hinweg mittels richtlinienbasierten Kontrollen durch.

| Control / Technik                                                                                      | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------------ | ---------------- |
| Zugriffskontrollen für KI-Ressourcen (Datensätze, Modelle, Endpunkte, Vektor-Sammlungen, Compute)      | 5.2.1            |
| Just-in-time privilegierter Zugriff auf KI-Ressourcen (Modellgewichte, Trainingspipelines)             | 5.2.2            |
| AI-spezifische Datenklassifizierungs-Taxonomie                                                         | 5.2.3            |
| Klassifizierungslabelweitergabe an abgeleitete KI-Ressourcen (Einbettungen, Caches, Ausgaben)          | 5.2.4            |
| Durchsetzung des Autorisierungskontexts des Aufrufers über KI-Abfrage-Pipelines                        | 5.3.1            |
| Fein abgestimmte Autorisierung von Agentenaktionen (Tool, Parameter, Ressourcen, Datenbereich)         | 9.6.1            |
| Delegation-Kontextweitergabe mit Integritätsschutz (Benutzer, Mandant, Bereiche)                       | 9.6.2            |
| Durchsetzung von Richtlinien auf Anwendungsebene (Modellausgabe kann nicht umgehen)                    | 9.6.3            |
| Vor-Ausführungsrichtlinien-Constraint-Gates (Verweigerungsregeln, Erlaubnislisten, Budgets)            | 9.7.1            |
| Scope-gefilterte MCP-Tool-Erkennung (tools/list)                                                       | 10.2.8           |
| Per-Tool-MCP-Aufrufzugriffskontrolle (Argument, Token-Scope)                                           | 10.2.9           |
| MCP-Richtlinienerzwingung, dass die Modellausgabe keine Umgehung ermöglichen darf                      | 10.2.7           |
| Autorisierungsbewusstes Post-Inferenz-Filtering (Durchsetzung von Berechtigungen pro Aufrufer)         | 5.4.1            |
| Zitations- und Attributionsvalidierung gegen die Berechtigungen des Aufrufers                          | 5.4.2            |
| Agenten-PDP-Laufzeitisolierung von der Agentenausführungsumgebung                                      | 5.5.1            |
| Strukturierte Handlungsbeschreibungen für PDP (nicht im Kontext einer rohen Agentenbegründung)         | 5.5.2            |
| KV-Cache-Partitionierung nach Sitzung/Mandant, um Prompt-Rekonstruktion zu verhindern                  | 5.6.1            |
| Geteiltes Modell-Serving-Mandantenisolierung (Feinabstimmung, Inferenz, Embeddings)                    | 5.6.2            |
| Peer-Authorization-Richtlinie (genehmigtes Agenten-Registry) für die agent-zu-agent Aufgabendelegation | 9.6.6            |

Häufige Fallstricke: das Vergeben weitreichender OAuth-Scopes statt der minimal erforderlichen; das nicht erneute Prüfen der Autorisierung, wenn sich der Kontext während der Sitzung ändert; das Zulassen, dass modelgenerierte Ausgaben harte Richtlinienentscheidungen überschreiben.

---

## AD.3 Verschlüsselung im Ruhezustand

Schützen Sie gespeicherte Daten, Modelle, Geheimnisse, Protokolle und Backups durch Verschlüsselung.

| Control / Technik                                 | Anforderungs-IDs |
| ------------------------------------------------- | ---------------- |
| Verschlüsselung der Trainingsdaten im Ruhezustand | ASVS v5 V6       |
| Beschriftete Datenverschlüsselung                 | 1.3.5            |
| Verschlüsselung im Ruhezustand protokollieren     | 13.1.4           |

Häufige Fallstricke: die Datenbank zu verschlüsseln, aber nicht Modell-Checkpoints oder Einbettungen; Protokolle nicht zu verschlüsseln, die Prompt-/Antwortdaten enthalten; Verschlüsselungsschlüssel zusammen mit den Daten zu speichern, die sie schützen.

---

## AD.4 Verschlüsselung während der Übertragung

Schützen Sie die Daten, die zwischen Diensten, Agenten, Tools und Edge-Geräten übertragen werden.

| Control / Technik                                                                     | Anforderungs-IDs |
| ------------------------------------------------------------------------------------- | ---------------- |
| Mutual TLS mit Zertifikatsvalidierung für die Kommunikation zwischen Diensten         | 4.3.4            |
| Authentifizierter streambarer-HTTP-Transport mit TLS 1.3 für MCP                      | 10.3.1, 10.3.2   |
| SSE privater Kanal mit TLS-Durchsetzung                                               | 10.3.2           |
| Protokollverschlüsselung während der Übertragung                                      | 13.1.4           |
| Durchsetzung der Mindestprotokollversion für MCP-Clients gegen Downstream-Aushandlung | 10.3.5           |

Häufige Fallstricke: das Zulassen von unverschlüsselten Verbindungen zwischen Systemen in Multi-Tenant-GPU-Clusters; die Nutzung von SSE über das öffentliche Internet ohne TLS; das Nichtvalidieren von Zertifikaten bei internen Service-Aufrufen.

---

## AD.5 Schlüssel- und Secret-Management

Verwalten Sie kryptografische Schlüssel, Geheimnisse und Anmeldeinformationen während ihres gesamten Lebenszyklus.

| Control / Technik                                              | Anforderungs-IDs |
| -------------------------------------------------------------- | ---------------- |
| Agent-Identitätsnachweis-Rotation mit schneller Sperrung       | 9.4.5            |
| MCP-Laufzeit-Credential-Injection (keine Klartext-Geheimnisse) | 10.1.2           |

Häufige Fallstricke: fest codierte Geheimnisse in Konfigurationsdateien oder Container-Images; das Vernachlässigen von Rotationsplänen; das Speichern von MCP OAuth-Tokens im Serverzustand statt deren Validierung extern.

---

## AD.6 Kryptografische Integrität & Signierung

Überprüfen Sie die Authentizität und erkennen Sie Manipulationen von Modellen, Artefakten, Nachrichten, Protokollen und Tool-Definitionen.

| Control / Technik                                                                               | Anforderungs-IDs   |
| ----------------------------------------------------------------------------------------------- | ------------------ |
| Kryptografische Hashes für die Integrität von Trainingsdaten                                    | 1.2.2, 1.3.4       |
| Kryptografische Modellsignierung                                                                | 3.1.2              |
| Modellsignatur- und Prüfsummenüberprüfung bei Bereitstellung und Ladevorgang                    | 3.1.3              |
| Signierte Build-Artefakte mit Build-Origin-Metadaten                                            | ASVS v5 V15 / SLSA |
| Signaturvalidierung bei der Bereitstellung erstellen                                            | ASVS v5 V15 / SLSA |
| Überprüfung der Herkunft und Integrität von Modellen Dritter (signierte Aufzeichnungen)         | 6.1.1              |
| Kryptografische Signaturvalidierung für Modellveröffentlicher                                   | 6.2.1, 6.2.2       |
| Modell-Wasserzeichen und Fingerprinting                                                         | 11.5.5             |
| Ausführungsketten- kryptografische Bindung (Chain-ID) für Agentenaktionen                       | 9.4.2              |
| Agentenaktionssignierung und Zeitstempel für Nichtabstreitbarkeit und Nachvollziehbarkeit       | 9.4.4              |
| MCP-Komponenten-Signatur und Prüfsummenverifikation                                             | 10.1.1             |
| MCP-Schema-Integritätsunterzeichnung und Tool-Definitions-Hash-Tracking                         | 10.4.8, 10.4.5     |
| Publisher-Key-Pinning pro Quell-Registry mit Rotation und erneuter Freigabe                     | 6.2.2              |
| Integritätsschutz für den persistierten Agentenzustand (MAC/Signatur, Zurückweisung bei Fehler) | 9.4.6              |

Häufige Fallstricke: die Verwendung veränderbarer`:latest`Tags statt unveränderlicher Digests; keine erneute Verifizierung der Hashes der Tool-Definitionen zwischen MCP-Aufrufen; fehlender Replay-Schutz für Agent-Nachrichten.

---

## AD.7 Eingabevalidierung & -bereinigung

Validieren, normalisieren und begrenzen Sie alle Eingaben, bevor sie Modelle oder nachgelagerte Systeme erreichen.

| Control / Technik                                                                                                                                                        | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------- |
| Prompt Injection Detection Regelwerk / Service                                                                                                                           | 2.1.1            |
| Durchsetzung der Hierarchie der Anweisungen (System > Entwickler > Benutzer)                                                                                             | 2.1.7            |
| Beibehaltung der Anweisungs-Hierarchie über mehrstufige und tool-unterstützte Workflows hinweg, einschließlich Prompt-Komposition                                        | 2.1.8            |
| Pro-Request-Demonstrationsgrenzen im Kontextfenster                                                                                                                      | 2.1.5            |
| Many-Shot Jailbreaking-Pattern-Erkennung (systematische verhaltensbezogene In-Context-Übersteuerung)                                                                     | 2.1.9            |
| Im-kontextbezogene Versuche einer Verhaltensüberschreibung, die als Prompt-Injection-Ereignisse klassifiziert wurden                                                     | 2.1.10           |
| Kontextfenster-Proportionsgrenzen und Token-Limit-Erzwingung (ablehnen, nicht abschneiden)                                                                               | 2.1.2            |
| Bereinigung von Inhalten Dritter                                                                                                                                         | 2.1.4            |
| Zeichenmenge-Whitelist für Modell-Prompt-Eingaben                                                                                                                        | 2.1.3            |
| Vornormalisierung der Vor-Tokenisierung (Unicode NFC, Homoglyph-Zuordnung, Entfernung von Steuer-/unsichtbaren Zeichen, Neutralisierung bidirektionaler Texte)           | 2.2.1            |
| Post-Normalisierung: verdächtige Artefakte verwerfen oder markieren                                                                                                      | 2.2.3            |
| Quarantäne und Protokollierung für adversarialen Input                                                                                                                   | 2.2.2            |
| Eingabe- und Repräsentations-Smguggling-Erkennung und -Minderung                                                                                                         | 2.2.4            |
| Inhaltsklassifizierer für eingehende Prompts (Hass, Gewalt, sexuell, illegal) mit schwellenwertbasierter Ablehnung oder Bereinigung                                      | 2.3.1            |
| Mehrsprachige Bewertung von Lücken bei Klassifizierern mit ausgleichenden Kontrollen (Spracherkennung, konservative Schwellenwerte, Weiterleitung zur manuellen Prüfung) | 2.3.2            |
| Policy-verletzende Eingabeablehnung vor der Modellpropagation                                                                                                            | 2.3.3            |
| Benutzerspezifische und agentenbewusste Richtlinienüberprüfung                                                                                                           | 2.1.6            |
| Aus extrahierte und ausgeblendete Inhalte aus nicht-textuellen Eingaben werden als nicht vertrauenswürdig behandelt                                                      | 2.4.1            |
| Erkennung adversarieller Perturbationen bei Bild-/Audio-Eingaben                                                                                                         | 2.4.2            |
| Erkennung von Cross-Modal-Angriffen                                                                                                                                      | 2.4.3            |
| MCP-Eingabetypprüfung, Grenzwertvalidierung und Enumeration-Durchsetzung                                                                                                 | 10.4.4           |
| MCP-Ablehnung von nicht erkannten oder zu großen Funktionsaufrufsparametern                                                                                              | 10.4.7           |
| MCP-Nachrichtenrahmenintegrität und strikte Schema-Validierung                                                                                                           | 10.4.3           |
| MCP maximale Nutzlastgrößenbegrenzungen und Ablehnung fehlerhaft geformter Frames                                                                                        | 10.4.6           |
| MCP-Schemavalidierung für die Tool- und Ressourcenintegrität                                                                                                             | 10.4.8           |
| Tools-Ausgabe-Schema und Sicherheitsrichtlinienvalidierung vor erneuter Rückgabe an den Agent                                                                            | 9.3.3            |
| MCP-Tool-Antwortvalidierung (Prompt-Injection, Kontextmanipulation)                                                                                                      | 10.4.1           |

Häufige Fallstricke: nur die Textmodalität zu validieren und dabei Bild-/Audio-Kanäle zu ignorieren; sich ausschließlich auf reguläre Ausdrücke zu verlassen, ohne eine semantische Erkennung; Tool-Ausgaben nicht vor ihrer erneuten Einbindung in den Agent-Kontext zu validieren.

---

## AD.8 Ausgabe-Filterung & Sicherheit

Beschränken, filtern und validieren Sie die Modell-Ausgaben, bevor sie Benutzern oder nachgelagerten Systemen bereitgestellt werden.

| Control / Technik                                                                                                                                                             | Anforderungs-IDs |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Ausgabeformat-Schemavalidierung                                                                                                                                               | 7.1.1            |
| Stoppsequenzen und Token-Limits                                                                                                                                               | 7.1.2            |
| Parametrisierte Abfragen und sichere Deserialisierer für die Ausgabe-Verarbeitung                                                                                             | 7.1.3            |
| Konfidenzbewertung und Unsicherheitsabschätzung                                                                                                                               | 7.2.1            |
| Konfidenzschwellenwert-Gating mit Fallback-Nachrichten                                                                                                                        | 7.2.2            |
| Ausgabe-Sicherheitsklassifizierer (Hass, Belästigung, Gewalt)                                                                                                                 | 7.3.1            |
| Systemprompt-Leckageerkennung in Ausgaben (wortgetreu und paraphrasiert)                                                                                                      | 7.3.2            |
| Verhinderung von automatisch ausgelösten ausgehenden Anfragen aus aus modellgenerierter Ausgabe heraus                                                                        | 7.3.3            |
| Erkennung und Bereinigung von Output-Encoding- und Repräsentations-Smuggling                                                                                                  | 7.3.5            |
| System-Prompt und Entfernung von Backend-Daten aus Erklärungen                                                                                                                | 7.5.1            |
| RAG nicht unterstützte Behauptungen blockieren oder vor dem Bereitstellen redigieren                                                                                          | 7.6.4            |
| Autorisierungsbewusstes Post-Inferenz-Filtering (durchsetzungsbasierte Durchsetzung von Berechtigungen pro Aufrufer)                                                          | 5.4.1            |
| Zitations- und Attributionsvalidierung anhand der Berechtigungen des Aufrufers                                                                                                | 5.4.2            |
| MCP-Fehlerantwort-Säuberung (keine Stack-Traces, Tokens, internen Pfade)                                                                                                      | 10.4.2           |
| Generalisierung oder einseitige Transformation von vom Modell abgeleiteten sensiblen Attributen (Bereiche, Bins), um die Rekonstruktion von Trainingsdatensätzen zu begrenzen | 11.4.1           |

Häufige Fallstricke: das Ausblenden von PII im Text, aber nicht in strukturierten Datenfeldern; das Nichtdurchsetzen von Stop-Sequenzen bei Streaming-Ausgaben; das Offenlegen der internen Architektur durch Fehlermeldungen.

---

## AD.9 Ratenbegrenzung & Ressourcenbudgets

Durchsetzen von Konsumbeschränkungen, um Missbrauch, endlose Ausführung und Denial-of-Service zu verhindern.

| Control / Technik                                                                                                                                                                                                                                                                    | Anforderungs-IDs     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- |
| Pro-Benutzer-, pro-IP-, pro-API-Schlüssel-Ratenlimits                                                                                                                                                                                                                                | ASVS v5 V2.4         |
| Burst- und dauerhafte Ratenbegrenzung                                                                                                                                                                                                                                                | ASVS v5 V2.4         |
| Pro-Agent-Token-, Kosten- und Tool-Call-Budgets                                                                                                                                                                                                                                      | 9.1.1                |
| Rekursionstiefe und maximale Parallelitäts- / Fan-out-Grenzen                                                                                                                                                                                                                        | 9.1.1                |
| Wall-Clock-Zeit- und Ausgabengrenzen (Geldmittel)                                                                                                                                                                                                                                    | 9.1.1                |
| Kumulative Ressourcenzähler mit Hard-Stop-Schwellenwerten und Durchsetzungsmechanismen für den Circuit Breaker                                                                                                                                                                       | 9.1.2                |
| Pro-Tool-Kontingente für CPU, Speicher, Datenträger, ausgehenden Datenverkehr und Ausführungszeit mit fail-closed-Terminierung bei Überschreitung                                                                                                                                    | 9.3.2                |
| Protokollierung bei Quota- und Timeout-Überschreitung (Tool, Grenzwert überschritten, Zeitstempel)                                                                                                                                                                                   | 9.3.4                |
| Abfragelimitierung zur Modell-Extraktion und -Inversion-Abwehr, skaliert entsprechend dem Bedrohungsmodell (z.B. der Anzahl von Abfragen, die erforderlich sind, um das Modell zu approximieren oder Trainingsdatensätze zu rekonstruieren) und nicht als generisches API-Throttling | 11.4.2, 11.5.1       |
| Erkennung und Blockierung anomaler Nutzungsmuster                                                                                                                                                                                                                                    | 13.2.3, ASVS v5 V2.4 |

Häufige Fehler: Rate-Limits pro Endpoint festlegen, aber nicht pro Agent-Session; Tool-Fan-Out nicht berücksichtigen, wenn Budgets berechnet werden; keine Circuit Breaker für rekursive Agent-Ketten hinzufügen.

---

## AD.10 Sandboxing & Prozessisolierung

Isolieren Sie Workloads, Tools, Modelle und Agenten, um Ausfälle einzudämmen und laterale Bewegungen zu verhindern.

| Control / Technik                                                         | Anforderungs-IDs |
| ------------------------------------------------------------------------- | ---------------- |
| Minimale Betriebssystem-Berechtigungen und Linux-Fähigkeiten              | 4.1.1            |
| Mandatory Access Control (seccomp, AppArmor, SELinux)                     | 4.1.2            |
| Read-only Root-Dateisystem mit restriktiven Mount-Optionen                | 4.1.3            |
| Erkennung von Laufzeit-Privilegieneskalation und Container-Ausbruch       | 4.1.4            |
| TEE / Vertrauliches Computing mit Remote-Attestierung                     | 4.1.5            |
| Tool- und Plugin-Sandboxing (Container, VM, WASM, OS-Sandbox)             | 9.3.1            |
| Sandbox-Ausbruchserkennung mit automatisierter Tool-Quarantäne            | 9.3.7            |
| Agent-Isolierung über Mandanten, Sicherheitsdomänen und Umgebungen hinweg | 9.8.1            |
| MCP-stdio lokale-only Erzwingung mit Schutz vor Terminal-Injection        | 10.6.1           |

Häufige Fallstricke: die gemeinsame Nutzung von Infrastruktur zwischen Dev und Prod; das Gewähren von mehr Fähigkeiten als nötig für Container; das Nicht-Einschränken des Zugriffs auf den Cloud-Metadaten-Dienst durch AI-Workloads.

---

## AD.11 Netzsegmentierung & Egress-Kontrolle

Control Sie Netzwerkgrenzen, den Datenfluss und den ausgehenden Zugriff für KI-Workloads.

| Control / Technik                                                                                      | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------------ | ---------------- |
| Standardmäßig verweigernde Netzwerk-Richtlinien mit expliziten Erlaubnis-Listen                        | 4.3.1            |
| Netzwerksegmentierung über die Umgebungen dev / test / prod hinweg                                     | 4.3.2, 3.4.1     |
| Trennen Sie IAM-Rollen und Sicherheitsgruppen pro Umgebung, ohne gemeinsame Principals                 | 4.3.6            |
| Eingeschränkter administrativer Zugriff und Blockierung des Cloud-Metadatendienstes                    | 4.3.3            |
| Egress-Verkehrsbeschränkung auf genehmigte Ziele mit Protokollierung                                   | 4.3.5            |
| MCP ausgehender Egress ist auf genehmigte Ziele beschränkt (alle anderen sind standardmäßig blockiert) | 10.5.1           |
| MCP-Funktionsaufruf auf statisch definierte, genehmigte (Allow-Listed) Namen beschränkt                | 10.6.2           |
| Standardmäßig die zustandslose Erkennung agents über Domänen hinweg und deren Aufrufe verweigern       | 9.8.1            |
| Ursprung- und Host-Header-Validierung zur DNS-Rebinding-Abwehr                                         | 10.3.3           |
| SSE-öffentliche Internetblockierung                                                                    | 10.3.2           |

Häufige Fallstricke: Zulassen, dass KI-Workloads auf Cloud-Metadaten-Dienste zugreifen; kein Protokollieren des Egress-Traffics für forensische Analysen; das Versäumen der Validierung des Origin-Headers, wodurch DNS-Rebinding-Angriffe ermöglicht werden.

---

## AD.12 Lieferkette & Integrität von Artefakten

Überprüfen Sie die Herkunft und Echtheit, scannen Sie Abhängigkeiten und stellen Sie die Integrität von Modellen, Frameworks, Datensätzen und Build-Artefakten sicher.

| Control / Technik                                                                                 | Anforderungs-IDs          |
| ------------------------------------------------------------------------------------------------- | ------------------------- |
| Modellregister-Inventar der bereitgestellten Modellartefakte                                      | 3.1.1                     |
| AI BOM Veröffentlichung (CycloneDX, SPDX)                                                         | 6.5.1                     |
| Modell-abhängigkeitsdiagramm-Tracking (Services, Agents, Umgebungen)                              | 3.1.4                     |
| Modellursprungsaufzeichnungen (Quelle, Trainingsdaten-Prüfsummen, Urheberschaft)                  | 3.1.5, 6.1.1              |
| Automatisierte reproduzierbare Builds                                                             | ASVS v5 V15 / SLSA        |
| SBOM-Erstellung aus automatisierten Builds                                                        | ASVS v5 V15.1.2 / SCVS    |
| Vergleich der Hashes reproduzierbarer Builds                                                      | SLSA Build L3             |
| Abhängigkeits-Scanning der CI-Pipeline                                                            | ASVS v5 V15.2.1 / SCVS V5 |
| Kritische / Hochrisiko-Sicherheitslücke, die in CI blockierend ist                                | ASVS v5 V15.1.1 / SCVS V5 |
| Abhängigkeitversions-Pinning mit Lockfile-Erzwingung                                              | SCVS V4 / CIS Guide       |
| Unveränderliche Digest-Referenzen für Container (keine veränderlichen Tags)                       | SCVS / CIS-Handbuch       |
| Erkennung abgelaufener und nicht gepflegter Abhängigkeiten                                        | ASVS v5 V15.1.1, V15.2.1  |
| Genehmigte Durchsetzung von Quellenangaben für KI-Artefakte                                       | 6.2.1                     |
| Erkennung von bösartigen Schichten und Trojaner-Auslösern                                         | 6.1.2                     |
| Verbot eines unsicheren Deserialisierungsformats und formatbewusstes Scannen zur Ladezeit         | 4.1.3                     |
| Bewertung von Datenvergiftung durch externe Datensätze (Fingerprinting, Erkennung von Ausreißern) | 6.3.1                     |
| Urheberrecht- und PII-Erkennung in externen Datensätzen                                           | 6.3.2                     |
| Datensatzherkunft und Dokumentation der Abstammung                                                | 6.3.3                     |
| AI BOM kryptografische Signierung                                                                 | 6.5.2                     |
| Build-Attribution-Retention                                                                       | SLSA-Build-Track          |

Häufige Fallstricke: Nicht scannen von Fine-Tuning-Datensätzen auf Poisoning; keine Rollback-Verfahren einzuführen, wenn ein kompromittiertes Modell erkannt wird; KI-BOMs als statische Dokumente statt als versionierte Artefakte zu behandeln.

---

## AD.13 Bereitstellung & Lebenszyklus-Management

Verwalten Sie die Modellbereitstellung, den Rollback, die Außerbetriebnahme und die Notfallreaktion.

| Control / Technik                                                                                            | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------------------ | ---------------- |
| Automatisiertes Testen der Eingabevalidierung vor der Bereitstellung                                         | 3.2.1            |
| Automatisiertes Testen der Bereinigung von Ausgaben vor dem Deployment                                       | 3.2.2            |
| Sicherheitsbewertungen mit Bestehen/Nichtbestehen-Grenzwerten vor der Bereitstellung                         | 3.2.3            |
| Automatische Bereitstellungsblockierung bei Nichterreichen der Sicherheitsbewertungsschwelle                 | 3.2.4            |
| Agent-Workflow, Tool-, MCP- und RAG-Integrations-Tests                                                       | 3.2.5            |
| Unveränderliche Audit-Records für Modelländerungen                                                           | 3.2.6            |
| Canary / Blue-Green-Deployments mit automatisierten Rollback-Triggern                                        | 3.3.1            |
| Parallele Bereitstellung: Kohortenisolierung (A/B, Canary, Shadow)                                           | 3.3.3            |
| Wiederherstellung des atomaren Zustands beim Rollback (Gewichte, Konfiguration, Adapter, Sicherheitsmodelle) | 3.3.2            |
| Trennung von Entwicklungs-, Test- und Produktionsumgebungen                                                  | 3.4.1            |
| Keine gemeinsam genutzte Infrastruktur über Umgebungsgrenzen hinweg                                          | 3.4.2            |
| Versionskontrolle für alle Entwicklungsartefakte (Hyperparameter, Skripte, Prompts, Richtlinien)             | 3.4.3            |
| Sicheres Löschen von Modellartefakten und kryptografische Auslöschung bei Ausscheiden                        | 3.5.1            |
| Modellsignatur-Widerruf und Registrierung-Blacklist bei der Außerbetriebnahme                                | 3.5.2            |
| KI-spezifische Incident Response in der Lieferkette (Model-Rollback, Signaturwiderruf)                       | 6.4.1            |

Häufige Fallstricke: Rollback-Verfahren nicht testen, bevor sie benötigt werden; ausgemusterte Modellartefakte in Serving-Caches belassen; das Herunterfahren mit einer Shutdown-Kaskade für nachgelagerte Tools und MCP-Verbindungen verfehlen.

---

## AD.14 Datenschutz & Datenminimierung

Schützen Sie personenbezogene Daten und setzen Sie die Rechte der betroffenen Personen während des gesamten KI-Lebenszyklus durch.

| Control / Technik                                                                                              | Anforderungs-IDs |
| -------------------------------------------------------------------------------------------------------------- | ---------------- |
| Minimierung von Trainingsdaten (unnötige Features, personenbezogene Daten, geleakte Testdaten ausschließen)    | 1.1.2            |
| Anonymisierung gelabelter Daten und granulare Schwärzung                                                       | 1.3.5            |
| Direkte und quasi-identifizierende Entfernung                                                                  | 12.1.1           |
| k-Anonymität und l-Diversität-Messung mit automatisierten Audits                                               | 12.1.2           |
| Feature-Importance-Leckage-Check auf trainierten Modellen                                                      | 12.1.3           |
| Synthetische Daten mit formalen Zurückverknüpfungsrisiko-Schranken                                             | 12.1.4           |
| Datenlöschungsweitergabe über KI-Artefakte (Datensätze, Checkpoints, Caches)                                   | 12.2.1           |
| Schattenmodellbewertung der Wirksamkeit des Unlearning                                                         | 12.2.2           |
| Maschinelles Unlearning mit zertifizierten Algorithmen                                                         | 12.2.3           |
| Datenschutz-Fehlverlust-Bilanzierung mit Epsilon-Budget-Tracking und -Benachrichtigungen                       | 12.3.1           |
| Empirische (Black-Box-)Differential-Privacy-Prüfungen                                                          | 12.3.2           |
| Formale Beweise zur Differential Privacy (einschließlich Nachtraining und Einbettungen)                        | 12.3.3           |
| Zweck-Tags mit maschinenlesbarer Ausrichtung und Laufzeitdurchsetzung                                          | 12.4.1, 12.4.2   |
| Validierung des Gültigkeitsbereichs der Einwilligung vor der Modellinferenz (Vorgänge und betroffene Personen) | 12.5.1           |
| Durchsetzung des Einwilligungsumfangs: Antwort verweigern oder herabstufen, bevor sie bereitgestellt wird      | 12.5.2           |
| Einwilligungsrücknahme-Ausbreitung über KI-Artefakte (im Einklang mit der Lösch-SLA)                           | 12.5.3           |
| Lokale oder zentrale Differential Privacy im föderierten Lernen                                                | 12.6.1           |
| Differenziell private Trainingsmetriken                                                                        | 12.6.2           |
| föderiertes Canary-basiertes Datenschutz-Auditing                                                              | 12.6.3           |
| Dienstprogramm für föderiertes Training: Fehlerminimierungs-Grenzwert im Abgleich mit ε-Budget                 | 12.6.4           |
| PII-Erkennung und -Entfernung in externen Datensätzen                                                          | 6.3.2            |

Häufige Fallstricke: Das Löschen von Datensätzen in der Datenbank, aber nicht in Modell-Checkpoints oder Embeddings; das Nichtberücksichtigen der sich über Abfragen aufsummierenden Epsilon-Budgets; die Annahme, dass Anonymisierung ein einmaliger Schritt ist.

---

## AD.15 Adversarial Testing & Model Hardening

Testen und Abwehren von Ausweich-, Extraktions-, Inversions-, Vergiftungs- und Alignment-Bypass-Angriffen.

| Control / Technik                                                                                                                                                                                                                                                             | Anforderungs-IDs |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Weigerungs- und Safe-Completion-Schutzplanken                                                                                                                                                                                                                                 | 11.1.1           |
| Red-Team- und Jailbreak-Test-Suiten (versionkontrolliert)                                                                                                                                                                                                                     | 11.1.2           |
| Automatisierte Bewertung der Rate für schädliche Inhalte mit Regressionsdetektion                                                                                                                                                                                             | 11.1.3           |
| RLHF / Constitutional AI-Ausrichtungstraining                                                                                                                                                                                                                                 | 11.1.4           |
| Adversarial Training und entsprechende Härtungstechniken, die jeweils nach Möglichkeit angewendet werden                                                                                                                                                                      | 11.2.3           |
| Dokumentierte und reproduzierbare Konfigurationen und Vorgehensweisen zur adversarialen Härtung                                                                                                                                                                               | 11.2.5           |
| Adversarial robustes Distillation — destillieren Sie den Lehrer in den Schüler, indem Sie adversariales Training verwenden, sodass der Schüler Robustheit ebenso wie Genauigkeit übernimmt (Implementierungsbeispiel für 11.2.3)                                              | 11.2.3           |
| Zertifizierte robuste Metriken zur Nachverfolgung pro Modellversion mit Degradationswarnung                                                                                                                                                                                   | 11.2.4           |
| Formale Robustheitsprüfung (zertifizierte Schranken, Intervall-Propagierung)                                                                                                                                                                                                  | 11.2.7           |
| Robustheit nach der Transformation: erneute Zertifizierung (Feinabstimmung, Destillation, Quantisierung, Adapter-Merging)                                                                                                                                                     | 11.2.8           |
| Erkennung von Adversarial-Examples mit produktionsseitiger Alarmierung                                                                                                                                                                                                        | 11.2.2           |
| Modell-Ensemble als Umgehungs-Eindämmung — leite Anfragen über unabhängig trainierte Modelle weiter und markiere Meinungsverschiedenheiten jenseits eines Schwellenwerts (Implementierungsbeispiel für 11.2.2)                                                                | 11.2.2           |
| Kalibrierung und Perturbation der Ausgabe für den Datenschutz                                                                                                                                                                                                                 | 11.3.1           |
| Confidence-Verschleierung / Output-Störung — gib kalibrierte, aber absichtlich ungenaue Confidence-Scores zurück, um die Modellauslese und die Membership-Inferenz zu erschweren (Implementierungsbeispiel für 11.3.1)                                                        | 11.3.1           |
| DP-SGD (differenziell private Schulung) mit dokumentiertem epsilon                                                                                                                                                                                                            | 11.3.2           |
| PATE (Private Aggregation of Teacher Ensembles) — trainiere ein Studentenmodell mithilfe einer verrauschten Aggregation von Lehrer-Ausgaben, sodass keine einzelnen Trainingsdatenaufzeichnungen offengelegt werden (Implementierungsbeispiel für 11.3.2)                     | 11.3.2           |
| Mitgliedschafts-Erkennungs-Angriffssimulation (Shadow-Modell, Likelihood-Quotient)                                                                                                                                                                                            | 11.3.3           |
| Modellextraktions-Erkennung (Abfrage-Pattern-Analyse, Diversitätsmessung)                                                                                                                                                                                                     | 11.5.3           |
| Statistische Ausreißer und Konsistenzbewertung bei externen Eingaben                                                                                                                                                                                                          | 11.6.1           |
| Testen der adaptiven Angriffsausweichung                                                                                                                                                                                                                                      | 11.6.5           |
| KI-gestützte Überprüfung risikoreicher Agentenaktionen (sekundäres Modell, strukturierte Selbstüberprüfung, Ensemble von Beurteilern), ergänzt die deterministische Policy-Gating-Logik (C9.7.1)                                                                              | 11.8.1           |
| KI-gestützter Überprüfungsmechanismus, der gegen Prompt-Injection-Umgehung geschützt ist                                                                                                                                                                                      | 11.8.2           |
| Selbstmodifikations-Einschränkung mit Gültigkeitsbereichsgrenzen und Ratenbegrenzungen                                                                                                                                                                                        | 11.9.1, 11.9.5   |
| Selbstmodifikations-Rückgängig-Machbarkeit und Integritätsverifikation, die ein Rollback auf einen bekannten funktionsfähigen Zustand ermöglichen                                                                                                                             | 11.9.4           |
| Sicherheitsverletzungs-Feedback-Pipeline-Integrität, Poisoning-Erkennung und menschliche Prüfungs-Gates                                                                                                                                                                       | 11.9.6           |
| Datenaugmentation mit gestörten Eingaben zur Verbesserung der Robustheit beim Training                                                                                                                                                                                        | 1.4.6            |
| RONI (Reject On Negative Influence)-Filterung — berechnen Sie für jede Trainingsprobe den Influence-Score und verwerfen Sie diejenigen, die die Leistung auf einem zurückgehaltenen Datensatz über einen Grenzwert hinaus verschlechtern (Implementierungsbeispiel für 1.4.2) | 1.4.2            |
| Gradient-Fingerprinting / Analyse von Gradienten pro Probe — Erkennung abnormer Gradienten-Normen oder -Richtungen, die während des Trainings auf vergiftete Proben hindeuten (Implementierungsbeispiel für 1.4.2)                                                            | 1.4.2            |
| Aktivierungs-Clustering — Clustern von Zwischenaktivierungen zur Erkennung von durch Backdoors assoziierten Teilpopulationen (Implementierungsbeispiel für 1.4.2)                                                                                                             | 1.4.2            |

Häufige Fallstricke: nur bekannte Jailbreak-Muster zu testen, ohne adaptive Angriffe; Red-Team-Suites nach Modellupdates nicht zu aktualisieren; sich auf nur eine einzige Verteidigung zu verlassen, statt Defense-in-Depth.

---

## AD.16 Logging & Audit

Erfassen Sie sicherheitsrelevante Ereignisse mit Integritätsschutz für forensische Analyse und Compliance.

| Control / Technik                                                                                                                                                                                        | Anforderungs-IDs |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Sicherheitsrelevante Metadatenprotokollierung für KI-Interaktionen (Zeitstempel, Benutzer-ID, Sitzungs-ID, Modellversion, Tokenanzahl, Eingabe-Hash, Konfidenzwert, Ergebnis der Sicherheitsfilterung)   | 13.1.1           |
| KI-Interaktionsprotokolle schließen standardmäßig Prompt- und Antwortinhalte aus; das Protokollieren von Inhalten erfordert eine ausdrückliche Opt-in-Einwilligung und eine dokumentierte Begründung     | 13.1.2           |
| Sichere, zugriffskontrollierte Protokoll-Repositorys mit Aufbewahrungsrichtlinien                                                                                                                        | 13.1.3           |
| Verschlüsselung im Ruhezustand und bei der Übertragung protokollieren                                                                                                                                    | 13.1.4           |
| PII-, Credential- und proprietäre Informationen-Ausblendung in Protokollen                                                                                                                               | 13.1.5           |
| Protokollierung von Entscheidungen zu Richtlinien und Sicherheitsfilteraktionen                                                                                                                          | 13.1.3           |
| Audit-Log-Kontextfelder ausreichend für die forensische Rekonstruktion (Akteur, Delegation, Richtlinie, Parameter, Ergebnisse)                                                                           | 9.4.3            |
| Agent-Aktionskryptografische Ketten-ID-Bindung                                                                                                                                                           | 9.4.2            |
| Agent-Aktionssignierung und Zeitstempel zur Nichtabstreitbarkeit                                                                                                                                         | 9.4.4            |
| Unveränderliche Auditprotokolle für Modelländerungen (Akteur, Änderungsart, vorher/nachher)                                                                                                              | 3.2.6            |
| Generische Prüfprotokoll- Unveränderbarkeit und Manipulationsnachweisfähigkeit                                                                                                                           | ASVS v5 V16.4.2  |
| CI/CD-Auditprotokoll-Streaming an SIEM                                                                                                                                                                   | ASVS v5 V16.4.3  |
| Erkennungsregeln für anomale Paketabrufe und manipulierte Build-Schritte                                                                                                                                 | ASVS v5 V16.3.3  |
| Protokollierung von Sicherheitsverstoß-Metriken                                                                                                                                                          | 7.6.1            |
| Selbstmodifikations-Protokollierung wird als Sicherheitsereignis klassifiziert, mit den Angaben was/wann/durch wen/Autorisierungsdetails                                                                 | 11.9.3           |
| Protokollierung von menschlichen Aufsichtseingriffen (Aktivierungen des Kill-Switch, Moduswechsel, Override-Befehle) mit Betreiberidentität, Kanal, Auslöser sowie vorherigem und resultierendem Zustand | 14.3.1           |

Häufige Fallstricke: Protokollieren von Prompts ohne Redaktion von personenbezogenen Daten (PII); Verwendung eines veränderbaren Log-Speichers ohne Integritätsschutz; Nichtaufnehmen ausreichenden Kontextes für die forensische Rekonstruktion; Protokollieren von Agentenaktionen und -freigaben, aber nicht von vom Menschen initiierten Überschreibungen wie Kill-Switch-Aktivierungen.

---

## AD.17 Überwachung, Alarmierung & Incident Response

Anomalien erkennen, auf Bedrohungen hinweisen und auf Sicherheitsvorfälle in KI-Systemen reagieren.

| Control / Technik                                                                                                                            | Anforderungs-IDs       |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| Erkennung von Jailbreak- und Prompt-Injection-Versuchen (signaturbasiert)                                                                    | 13.2.1                 |
| SIEM-Integration mit standardisierten Protokollformaten                                                                                      | 13.2.2                 |
| AI-spezifische Ereignis-Anreicherung (Modell-ID, Konfidenz, Filterentscheidungen)                                                            | 13.2.2                 |
| Verhaltensbedingte Anomalieerkennung (ungewöhnliche Muster, übermäßige Wiederholungsversuche, systematisches Sondieren)                      | 13.2.3, 13.2.5         |
| Erkennungsregeln für AI-spezifische Angriffsmuster (Jailbreak-Kampagnen, Prompt-Injection, Extraktion von System-Prompts, Modell-Extraktion) | 13.2.4                 |
| Automatisierte Incident Response (Isolation und Blockierung kompromittierter Modelle und bösartiger Benutzer)                                | 13.2.6                 |
| Leistungsmetriken-Überwachung (Genauigkeit, Latenz, Fehlerquote) mit Benachrichtigung                                                        | 13.3.1, 13.3.3, 13.3.4 |
| Leistungsbeeinträchtigungs-, Retraining- und Austausch-Workflow-Auslöser                                                                     | 13.3.8                 |
| Halluzinations-Erkennung und -Überwachung                                                                                                    | 13.3.5                 |
| Halluzinationsrate-Zeitreihenverfolgung                                                                                                      | 13.3.9                 |
| Telemetrieüberwachung der Trainings-Pipeline (Laufzeitdauer, Verlustverlauf, Konvergenzrate) mit Baseline-Alarmierung und Artefakt-Gating    | 13.3.10                |
| Modell-Extraktionswarnungen mit Protokollierung von Abfrage-Metadaten generieren                                                             | 11.5.2                 |
| Erkennung emergenter Multi-Agenten-Verhaltensweisen (Oszillation, Deadlock, Broadcast-Stürme)                                                | 9.8.4                  |
| KI-spezifische Incident-Response-Pläne (Modellkompromittierung, Datenvergiftung, adversarialer Angriff)                                      | 13.5.1                 |
| KI-spezifische Forensik-Tools zur Untersuchung des Modellverhaltens                                                                          | 13.5.2                 |
| Sicherheitsverletzungsrate-Benachrichtigung                                                                                                  | 7.6.3                  |
| Sofortige Sicherheitsrichtlinien-Updates ohne vollständige Neu-Bereitstellung                                                                | 11.7.1                 |
| Rollback-Verfahren und Tests für Änderungen der Richtlinie                                                                                   | 11.7.3                 |

Häufige Fehler: AI-spezifische Ereignisse nicht mit umfassenderen SIEM-Alarms zu korrelieren; Modell-Drift als geplante Prüfung statt als kontinuierliches Monitoring zu behandeln; während der Incident Response keine AI-spezifischen forensischen Tools einzusetzen.

---

## AD.18 Erklärbarkeit & Transparenz

Ermöglichen Sie das menschliche Verständnis von Modellentscheidungen durch Interpretierbarkeits-Artefakte und Unsicherheitsquantifizierung, mit Erklärungen, die bereinigt sind, um das Offenlegen internen Kontexts zu vermeiden.

| Control / Technik                                                                                                                     | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Bereinigung von benutzersichtlichen Erklärungen, um Systemprompts und Backend-Daten zu entfernen                                      | 7.4.1            |
| Protokollierung von Modell-Interpretierbarkeitsartefakten (Aufmerksamkeitskarten, Feature-Zuschreibungen) zur forensischen Verwendung | 7.4.2            |
| Konfidenz- oder Unsicherheitsabschätzung für generierte Antworten                                                                     | 7.2.1            |
| Automatisches Blockieren oder Fallback, wenn die Zuverlässigkeit unter einen definierten Schwellwert fällt                            | 7.2.2            |
| Kalibrierung der Modellausgabe zur Reduzierung übermäßig selbstsicherer Vorhersagen, die durch Membership-Inference ausnutzbar sind   | 11.3.1           |

Häufige Fallstricke: Erklärungen bereitzustellen, die System-Prompts oder interne Architektur offenlegen; LLM-generierte Begründungen als getreue Beschreibungen der Modellinternen zu behandeln; Unsicherheitsabschätzungen nicht zu kalibrieren, sodass nachgelagerte Prüfungen sie nicht vertrauen können.

---

## AD.19 Menschliche Aufsicht & Genehmigungs-Engpassstellen

Erfordert eine menschliche Überprüfung und Freigabe für hochwirksame, irreversible oder sicherheitskritische Aktionen und stellt zuverlässige Abschalt- und Graceful-Degradation-Pfade bereit, die unter menschlicher Kontrolle stehen. Wirksame menschliche Aufsicht erfordert vier kooperierende Ebenen: eine Richtlinie, die klassifiziert, welche Aktionen als hochriskant gelten (C14.2), ein Laufzeit-Gate, das die Ausführung blockiert, bis eine Freigabe erhalten wurde (C9.2), Kill-Switch- und Graceful-Degradation-Mechanismen, um das System bei Bedarf anzuhalten oder einzuschränken (C14.1), sowie unabhängige Audit Trails für sowohl Freigaben (C13.6.4) als auch menschlich initiierte Overrides (C14.3). Jede Ebene ist separat verifizierbar; ein Freigabe-Gate ohne Richtlinie ist nicht durchsetzbar, eine Richtlinie ohne Laufzeit-Gate ist nicht durchgesetzt, und entweder ohne Audit Trails ist nicht zuordenbar.

| Control / Technik                                                                                                                                                                                                                      | Anforderungs-IDs |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Dokumentierte Richtlinie für risikoreiche Aktionen (Klassifizierungskriterien, Genehmigungsbefugnis)                                                                                                                                   | 14.2.1           |
| Hochwirksame Aktionsfreigabe- Gates (bereitstellen, löschen, finanziell, benachrichtigen)                                                                                                                                              | 9.2.1            |
| Genehmigungsparameter-Bindung (approve-one-execute-another verhindern)                                                                                                                                                                 | 9.2.2            |
| Hochwirksame Bestätigung der Absicht mit exakter Parameterbindung und schneller Ablaufzeit                                                                                                                                             | 9.2.3            |
| Fail-closed Standardaktion (Blockieren bis zur Aktion), wenn keine menschliche Genehmigung innerhalb der TTL erfolgt                                                                                                                   | 14.2.2           |
| Jede nicht im Fail-Closed-Modus ausfallende TTL-Ablauf-Standardkonfiguration, die ausdrücklich autorisiert und als eine Entscheidung für eine High-Risk-Policy klassifiziert ist, die eine Genehmigungsbefugnis-Unterschrift erfordert | 14.2.3           |
| Menschliche Überprüfung der Anomalieerkennung                                                                                                                                                                                          | 11.6.3           |
| Hochrisiko-Modellquarantäne mit menschlicher Überprüfung und Freigabe durch Unterschrift                                                                                                                                               | 6.1.3            |
| Nachbedingungsprüfung des Ergebnisses mit Einschluss bei Nichtübereinstimmung                                                                                                                                                          | 9.7.2            |
| Ausgleichsmaßnahmen und Transaktions-Rollback bei einem Fehlschlag                                                                                                                                                                     | 9.2.4            |
| Manueller Kill-Switch, um die Modellausgabe und -ausgabevorgänge zu stoppen                                                                                                                                                            | 14.1.1           |
| Zwischenstufen der betrieblichen Leistungsbeeinträchtigung (Werkzeug-Deaktivierung, Modell-Wechsel, Nur-Lesen, Quelllöschung)                                                                                                          | 14.1.3           |
| Wiederkehrende Ausübung von Kill-Switch- und Zwischenzustandsmechanismen mit Verifikationen der Antwortzeit                                                                                                                            | 14.1.2           |
| Out-of-Band-Override und Kill-Switch-Kanal für autonome Agenten                                                                                                                                                                        | 14.1.4           |

Häufige Fallstricke: die Dokumentation einer Richtlinie für eine High-Risk-Aktion, die nie an eine Laufzeit-Gate-Funktion gekoppelt wird; die Bindung einer Genehmigung an einen Hash von Parametern ohne Bindung an Identität oder Kontext (Wiedergabe über Sitzungen hinweg); Bestätigungstokens ohne schnelle Ablaufzeit; standardmäßig „fail-open“, wenn der Genehmigende nicht antwortet, sodass das Gate stillschweigend umgangen wird; die Annahme, dass ein In-Band-Kill-Switch gegen einen kompromittierten Agenten funktionieren wird; ein implementierter Kill-Switch, der jedoch nie ausgeführt wird, wodurch er verkümmert, bis der Moment kommt, in dem er benötigt wird.

---

---

## Referenzen

* [NIST AI Risk Management Framework 1.0](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)
* [ISO/IEC 42001:2023: AI Management Systems Requirements](https://www.iso.org/standard/42001)
* [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
* [OWASP Application Security Verification Standard (ASVS)](https://owasp.org/www-project-application-security-verification-standard/)
* [NIST SP 800-218A: Secure Software Development Practices for Generative AI](https://csrc.nist.gov/pubs/sp/800/218/a/final)

