# Anhang D: KI-Sicherheitskontroll-Übersicht

## Ziel

Dieser Anhang bietet eine kompakte Übersicht über jede Sicherheitsmaßnahme und jede Verteidigungstechnik, auf die in den AISVS-Anforderungen Bezug genommen wird. Die Maßnahmen sind nach Kategorien von Sicherheitsmaßnahmen gruppiert, damit Implementierer alle zugehörigen Abwehrmaßnahmen an einer Stelle finden können, unabhängig davon, welches AISVS-Kapitel sie definiert.

---

## AD.1 Authentifizierung

Überprüfen Sie die Identität von Benutzern, Agenten, Diensten, MCP-Clients/-Servern und Edge-Geräten, bevor Sie Zugriff gewähren.

| Control / Technik                                                                                                                       | Anforderungs-IDs |
| --------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Höherstufige Authentifizierung für risikoreiche KI-Operationen (Modellbereitstellung, Export von Gewichten, Zugriff auf Trainingsdaten) | 5.1.1            |
| Kurzlebige signierte Tokens für die föderierte Authentifizierung von KI-Agenten                                                         | 5.1.2            |
| Eindeutige kryptografische Agent- und Orchestrator-Identität                                                                            | 9.4.1            |
| Erstklassige Principal-Authentifizierung (keine Wiederverwendung von Endnutzeranmeldedaten)                                             | 9.4.1            |
| Agent-Identitätsnachweis-Rotation und schnelle Sperrung                                                                                 | 9.4.4            |
| OAuth 2.1 für die Client-Authentifizierung von MCP                                                                                      | 10.2.1           |
| MCP-Server OAuth-Token-Validierung (Aussteller, Zielgruppe, Ablauf, Berechtigung)                                                       | 10.2.2           |
| MCP-Server-Registrierung mit explizitem Ownership                                                                                       | 10.2.3           |
| Kryptografisch sichere MCP-Sitzungs-IDs (nicht für Authentifizierung verwendet)                                                         | 10.2.8           |
| Gegenseitige Authentifizierung von Edge-Geräten mit Zertifikatsvalidierung                                                              | 4.8.1            |
| Arbeitslastbestätigung für vertrauliches Computing                                                                                      | 4.5.3            |
| Hardware-basierte Attestierung (TPM, DRTM)                                                                                              | 4.7.1            |

Häufige Fallstricke: die Wiederverwendung von Endbenutzer-Identifizierungsdaten für Agent-zu-Agent-Aufrufe; die Verwendung von MCP-Sitzungs-IDs als Authentifizierungstokens; die Nichtrotierung von Agent-Identifizierungsdaten bei einem vermuteten Kompromittieren.

---

## AD.2 Autorisierung & Zugriffskontrolle

Setzen Sie Zugriffsentscheidungen über Nutzer, Agenten, Tools, Daten und MCP-Ressourcen hinweg mithilfe von richtlinienbasierten Kontrollen durch.

| Control / Technik                                                                                        | Anforderungs-IDs |
| -------------------------------------------------------------------------------------------------------- | ---------------- |
| Zugriffssteuerungen für KI-Ressourcen (Datensätze, Modelle, Endpunkte, Vektor-Sammlungen, Compute)       | 5.2.1            |
| Just-in-time privilegierter Zugriff auf KI-Ressourcen (Modellgewichte, Trainingspipelines)               | 5.2.2            |
| Klassifizierungs-Label-Propagation auf abgeleitete KI-Ressourcen (Einbettungen, Caches, Ausgaben)        | 5.2.3            |
| AI-spezifische Taxonomie zur Datenklassifizierung                                                        | 5.2.4            |
| Durchsetzung des Kontextes für die Autorisierung des Anrufers über KI-Abfrage-Pipelines                  | 5.3.1            |
| Feingranulare Agentenaktionsautorisierung (Tool, Parameter, Ressourcen, Datenscope)                      | 9.6.1            |
| Delegation-Kontextweitergabe mit Integritätsschutz (Benutzer, Mandant, Geltungsbereiche)                 | 9.6.2            |
| Kontinuierliche erneute Bewertung der Autorisierung (Kontext, Zeit, Risiko)                              | 9.6.3            |
| Durchsetzung von Richtlinien auf Anwendungsebene (Modellausgaben können nicht umgehen)                   | 9.6.4            |
| Vor-Ausführungs-Richtlinien-Constraint-Gates (Verbotsregeln, Zulassungslisten, Budgets)                  | 9.7.1            |
| Scope-filtered MCP-Tool-Erkennung (tools/list)                                                           | 10.2.6           |
| Per-Tool-MCP-Aufrufzugriffskontrolle (Argument, Token-Scope)                                             | 10.2.7           |
| Mindestumfang von Anfragen mit Eskalation der Autorisierung                                              | 10.2.11          |
| Ablehnung aufgrund von Wildcards und eines zu weit gefassten Geltungsbereichs                            | 10.2.14          |
| MCP-Richtliniendurchsetzung, dass die Modellausgabe nicht umgehen kann                                   | 10.2.4           |
| Autorisierungsbewusstes Post-Inferenz-Filtering (Durchsetzung von Berechtigungen pro Aufrufer)           | 5.4.1            |
| Zitations- und Zuschreibungsvalidierung anhand der Berechtigungen des Aufrufers                          | 5.4.2            |
| Agent-PDP-Laufzeitisolierung von der Agent-Ausführungsumgebung                                           | 5.5.1            |
| Strukturierte Handlungsbeschreibungen für PDP (nicht Roh-Agenten-Überlegungen-Kontext)                   | 5.5.2            |
| KV-Cache-Partitionierung nach Sitzung/Mandant, um Prompt-Rekonstruktion zu verhindern                    | 5.6.1            |
| Gemeinsames Modell-Serving: Mandantentrennung (Feinabstimmung, Inferenz, Embeddings)                     | 5.6.2            |
| Erkennung von Namespace-Kollisionen für MCP-Tools und Schutz vor vertrauenswürdig eingestuftem Shadowing | 10.6.5           |
| Peer-Authorisierungsrichtlinie (genehmigtes Agent-Registry) für agenten-zu-agenten Aufgabenweitergabe    | 9.6.7            |
| Dedizierte gescoped Credentials pro Agent, nicht gemeinsam genutzt über Swarm-Peers hinweg               | 9.8.7            |

Häufige Fallstricke: das Erteilen weit gefasster OAuth-Berechtigungen statt der minimal erforderlichen; das Nicht-Überarbeiten der Autorisierung, wenn sich der Kontext mitten in einer Sitzung ändert; das Zulassen, dass modellgenerierte Ausgaben harte Richtlinienentscheidungen überschreiben.

---

## AD.3 Verschlüsselung im Ruhezustand

Schützen Sie gespeicherte Daten, Modelle, Geheimnisse, Protokolle und Backups durch Verschlüsselung.

| Control / Technik                                                                                | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------ | ---------------- |
| Verschlüsselung der Trainingsdaten im Ruhezustand                                                | 1.2.3            |
| Beschriftete Datenverschlüsselung                                                                | 1.3.5            |
| Secrets-Verschlüsselung im Ruhezustand in einem Secrets-Management-System                        | 4.4.1            |
| Protokollverschlüsselung im Ruhezustand                                                          | 13.1.3           |
| TEE-Speicherverschlüsselung und Integritätsschutz                                                | 4.5.4            |
| Vertrauliche Inferenz (versiegelte Modellgewichte in geschützter Ausführung)                     | 4.5.5            |
| Sichern Sie die Netzsegmentierung mit getrennten Zugangsdaten ab                                 | 4.6.3            |
| Air-gapped / WORM-Backup-Speicher                                                                | 4.6.4            |
| Modellverschlüsselung im Ruhezustand auf Mobilgeräten mit vertrauenswürdiger Laufzeit-Decryption | 4.8.9            |
| Hardwaregestützte Key Stores (Secure Enclave, Android Keystore, TPM)                             | 4.8.8            |

Häufige Fallstricke: die Datenbank zu verschlüsseln, aber keine Modell-Checkpoints oder Einbettungen; Protokolle nicht zu verschlüsseln, die Prompt-/Antwortdaten enthalten; und Verschlüsselungsschlüssel zusammen mit den Daten zu speichern, die sie schützen.

---

## AD.4 Verschlüsselung bei der Übertragung

Schützen Sie die Daten, die zwischen Diensten, Agents, Tools und Edge-Geräten übertragen werden.

| Control / Technik                                                               | Anforderungs-IDs |
| ------------------------------------------------------------------------------- | ---------------- |
| Mutual TLS mit Zertifikatsvalidierung für die Kommunikation zwischen Diensten   | 4.3.4            |
| Mutual TLS für Agent-zu-Agent- und Agent-zu-Tool-Kommunikation (TLS 1.3+)       | 9.5.1            |
| Authentifizierter streambarer-HTTP-Transport mit TLS 1.3 für MCP                | 10.3.1, 10.3.2   |
| SSE privater Kanal mit TLS-Erzwingung                                           | 10.3.3           |
| Verschlüsselte TEE-Kommunikationskanäle                                         | 4.5.9            |
| Authentifizierte Beschleuniger-Interconnects (NVLink, PCIe, InfiniBand)         | 4.7.7            |
| Verschlüsselte Edge-to-Cloud-Kommunikation mit Bandbreiten-Throttling           | 4.8.6            |
| Protokollverschlüsselung bei der Übertragung                                    | 13.1.3           |
| MCP-Client erzwingt die minimale Protokollversion gegen Downgrade-Verhandlungen | 10.3.7           |

Häufige Fallstricke: Klartext-Verbindungen in Multi-Tenant-GPU-Clustern zulassen; SSE über das öffentliche Internet ohne TLS verwenden; Zertifikate bei Aufrufen interner Dienste nicht validieren.

---

## AD.5 Schlüssel- und Secret-Management

Verwalten Sie kryptografische Schlüssel, Geheimnisse und Anmeldeinformationen während ihres gesamten Lebenszyklus.

| Control / Technik                                                            | Anforderungs-IDs |
| ---------------------------------------------------------------------------- | ---------------- |
| Hardware-gestützter Key-Speicher (HSM, KMS, FIPS 140-3 Level 3)              | 4.4.4, 4.7.6     |
| Geheimnisseisolierung von Anwendungs-Workloads                               | 4.4.1            |
| Laufzeitbasierte Secret-Injection (aus Code, Konfiguration, Images entfernt) | 4.4.3            |
| Automatisierte Rotation von Schlüsseln und Geheimnissen                      | 4.4.5            |
| Agentenidentitätsnachweis-Rotation mit schneller Sperrung                    | 9.4.4            |
| MCP-Laufzeit-Anmeldeinformationen-Injektion (keine Klartext-Geheimnisse)     | 10.1.2           |
| Wasserzeichen-Überprüfungsschlüssel und Schutz für Trigger-Set               | 11.5.5           |
| Trenne Backup-Zugangsdaten von Produktionsdaten                              | 4.6.3            |
| Nicht-Zugänglichkeit von User-Space-Tasten auf Mobilgeräten                  | 4.8.8            |

Häufige Fallstricke: Hardcoded-Geheimnisse in Konfigurationen oder Container-Images; das Vernachlässigen von Rotationsplänen; das Speichern von MCP-OAuth-Token im Serverzustand statt einer externen Validierung.

---

## AD.6 Krypto-grafische Integrität & Signierung

Überprüfen Sie die Authentizität und erkennen Sie Manipulationen von Modellen, Artefakten, Nachrichten, Protokollen und Tool-Definitionen.

| Control / Technik                                                                               | Anforderungs-IDs   |
| ----------------------------------------------------------------------------------------------- | ------------------ |
| Kryptografische Hashes für die Integrität von Trainingsdaten                                    | 1.2.4, 1.3.4       |
| Kryptografisches Modellsignieren                                                                | 3.1.2              |
| Modellsignatur und Prüfsummenüberprüfung bei Bereitstellung und Ladevorgang                     | 3.1.3              |
| Signierte Build-Artefakte mit Build-Origin-Metadaten                                            | ASVS v5 V15 / SLSA |
| Implementiere die Signaturvalidierung bei der Bereitstellung                                    | ASVS v5 V15 / SLSA |
| Überprüfung der Herkunft und der Integrität von Modellen Dritter (signierte Aufzeichnungen)     | 6.1.1              |
| Kryptografische Signaturvalidierung für Modell-Publisher                                        | 6.2.1, 6.2.2       |
| Modell-Wasserzeichen und Fingerprinting                                                         | 7.7.5, 11.5.4      |
| Ausführungsketten kryptografische Signierung mit Nichtabstreitbarkeit- Zeitstempeln             | 9.4.2              |
| Nachrichtenintegrität mit Nonce-/Sequenz-/Zeitstempel-Replay-Schutz                             | 9.5.3              |
| Kryptografische Protokoll-Signaturen (nur Schreiben / nur Anhängen)                             | 13.1.6             |
| Manipulationssichere Audit-Logs (WORM)                                                          | 9.4.3              |
| MCP-Komponenten-Signatur und -Prüfsummenverifizierung                                           | 10.1.1             |
| MCP-Schemaintegritätsunterzeichnung und Hash-Tracking für die Tool-Definition                   | 10.4.2, 10.4.5     |
| DAG-kryptografische Signaturen und manipulationssicherer Speicher mit Nachweis                  | 13.7.3             |
| Publisher-Key-Pinning pro Quell-Registry mit Rotation und erneuter Freigabe                     | 6.2.2              |
| Dokumentmetadaten-Tag-Immeränderlichkeit nach der ersten Ingestion schreiben                    | 8.1.7              |
| Agent-bezogene Integritätsschutz für persistierten Status (MAC/Signatur, Verwerfung bei Fehler) | 9.4.6              |

Häufige Fallstricke: die Verwendung veränderbarer`:latest`Tags statt unveränderlicher Digests; keine erneute Verifizierung der Tool-Definition-Hashes zwischen MCP-Aufrufen; fehlender Replay-Schutz für Agenten-Nachrichten.

---

## AD.7 Eingabevalidierung & -bereinigung

Validieren, normalisieren und einschränken Sie alle Eingaben, bevor sie Modelle oder nachgelagerte Systeme erreichen.

| Control / Technik                                                                                                                                                               | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Regelsatz zur Erkennung von Prompt Injection / Service                                                                                                                          | 2.1.1            |
| Durchsetzung der Hierarchie der Anweisungen (system > developer > user)                                                                                                         | 2.1.2            |
| Pro-Request-Demonstrations-Limits im Kontextfenster                                                                                                                             | 2.1.5            |
| Many-shot Jailbreaking-Pattern-Erkennung (systematische verhaltensbezogene In-Context-Übersteuerung)                                                                            | 2.1.6            |
| In-Context-Verhaltensüberschreibungsversuche, als Prompt-Injection-Ereignisse klassifiziert                                                                                     | 2.1.7            |
| Kontextfenster-Proportionsgrenzen und Durchsetzung des Token-Limits (ablehnen, nicht abschneiden)                                                                               | 2.1.3            |
| Bereinigung von Inhalten Dritter                                                                                                                                                | 2.1.4            |
| Zeichenmengen-Allowlisting für Modell-Prompt-Eingaben                                                                                                                           | 2.1.9            |
| Vorverarbeitung der Eingabe-Normalisierung von Tokens (Unicode NFC, Homoglyph-Zuordnung, Entfernung von Steuer-/unsichtbaren Zeichen, Neutralisierung von bidirektionalem Text) | 2.2.1            |
| Quarantäne und Protokollierung für bösartige Eingaben                                                                                                                           | 2.2.2            |
| Erkennung und Eindämmung von Encoding- und Repräsentations-Smuggling                                                                                                            | 2.2.3            |
| Inhaltsklassifizierer für eingehende Prompts (Hass, Gewalt, sexuell, illegal)                                                                                                   | 2.3.1            |
| Vor der Modellpropagation wird eine Zurückweisung von Eingaben mit Richtlinienverstoß durchgeführt                                                                              | 2.3.2            |
| Benutzerspezifisches und agentenbewusstes Policy-Screening                                                                                                                      | 2.1.8            |
| Aus dem nicht-textbasierten Input extrahierter und verborgener Inhalt als nicht vertrauenswürdig behandelt                                                                      | 2.4.1            |
| Erkennung adversarialer Perturbationen bei Bild-/Audio-Eingaben                                                                                                                 | 2.4.2            |
| Cross-modale Angriffserkennung                                                                                                                                                  | 2.4.3            |
| MCP-Eingabetypüberprüfung, Grenzwertvalidierung und Durchsetzung der Aufzählung                                                                                                 | 10.4.4           |
| MCP Nachrichtenrahmen-Integrität und Nutzlastgrößenbeschränkungen                                                                                                               | 10.4.3           |
| MCP-Schema-Validierung für die Integrität von Tools und Ressourcen                                                                                                              | 10.4.2           |
| Tool-Ausgabe-Schema und Sicherheitsrichtlinienvalidierung vor erneuter Eingabe zum Agent                                                                                        | 9.3.3            |
| MCP-Tool-Antwortvalidierung (Prompt-Injection, Kontextmanipulation)                                                                                                             | 10.4.1           |

Häufige Fallstricke: Nur die Textmodalität zu validieren und dabei Bild-/Audio-Kanäle zu ignorieren; sich ausschließlich auf Regex zu verlassen, ohne eine semantische Erkennung; Tool-Ausgaben nicht zu validieren, bevor sie in den Agenten-Kontext zurückfließen.

---

## AD.8 Ausgabe-Filterung & Sicherheit

Beschränken, filtern und validieren Sie die Modell-Ausgaben, bevor sie die Nutzer oder nachgelagerte Systeme erreichen.

| Control / Technik                                                                            | Anforderungs-IDs |
| -------------------------------------------------------------------------------------------- | ---------------- |
| Ausgabeformat-Schemaüberprüfung                                                              | 7.1.1            |
| Stoppsequenzen und Token-Limits                                                              | 7.1.2            |
| Parametrisierte Abfragen und sichere Deserialisierer für die Verarbeitung der Ausgabe        | 7.1.3            |
| Konfidenzbewertung und Unsicherheitsschätzung                                                | 7.2.1            |
| Confidence-Schwellenwert-Gating mit Fallback-Nachrichten                                     | 7.2.2            |
| Ausgabe-Sicherheitsklassifizierer (Hass, Belästigung, Gewalt)                                | 7.3.1            |
| PII-Erkennung und -Anonymisierung (Post-Inference-Filterung)                                 | 7.3.2, 7.3.3     |
| Menschliche Genehmigung für Content mit hohem Risiko                                         | 7.3.5            |
| Entfernung von Systemprompt und Backend-Daten aus Erklärungen                                | 7.5.1            |
| Wasserzeichen für AI-generierte Medien                                                       | 7.7.5            |
| Urheberrechtsverletzungs-Erkennung                                                           | 7.7.3            |
| Explizite / nicht-einvernehmliche Inhaltsfilter                                              | 7.7.1            |
| Autorisierungsbewusstes Post-Inferenz-Filtering (durchsetzung der Berechtigung pro Aufrufer) | 5.4.1            |
| Zitations- und Zuordnungsvalidierung anhand von Berechtigungen des Anrufers                  | 5.4.2            |
| Bereinigung von MCP-Fehlerantworten (keine Stack-Traces, keine Tokens, keine internen Pfade) | 10.4.6           |
| Statistische steganografische Erkennungen verdeckter Kanäle in generierten Ausgaben          | 7.3.9            |
| RAG-Zuschreibung abgeleitet aus Abruf-Metadaten, nicht vom Modell generiert                  | 7.8.3            |

Häufige Fallstricke: Das Schwärzen von PII in Text, jedoch nicht in strukturierten Datenfeldern; das Nicht-Durchsetzen von Stop-Sequenzen bei Streaming-Ausgaben; das Offenlegen interner Architektur über Fehlermeldungen.

---

## AD.9 Ratenbegrenzung & Ressourcenbudgets

Setzen Sie Verbrauchsgrenzen durch, um Missbrauch, außer Kontrolle geratene Ausführung und Denial-of-Service zu verhindern.

| Control / Technik                                                                                     | Anforderungs-IDs     |
| ----------------------------------------------------------------------------------------------------- | -------------------- |
| Pro-User-, pro-IP-, pro-API-Schlüssel-Ratenbegrenzungen                                               | ASVS v5 V2.4         |
| Burst- und anhaltende Ratenbegrenzung                                                                 | ASVS v5 V2.4         |
| Token-, Kosten- und Tool-Call-Budgets pro Agent                                                       | 9.1.1                |
| Rekursionstiefe und maximale Parallelität / Fan-out-Limits                                            | 9.1.1                |
| Wanduhrenzeit- und monetäre Ausgabenlimits                                                            | 9.1.1                |
| Kumulative Ressourcen-Zähler mit harten Grenzwert-Schaltern                                           | 9.1.2                |
| Durchsetzungsmaßnahmen für den Leitungsschutzschalter                                                 | 9.1.3                |
| Pro-Tool-CPU-, Speicher-, Festplatten-, Egress- und Ausführungszeitlimits                             | 9.3.2                |
| Kontingent- und Timeout-Überschreitungs-Verstoß: fail-closed Terminierung                             | 9.3.7                |
| Unteraufgaben-Delegationskette-Tiefenlimit pro Ausführung                                             | 7.4.4                |
| Abfragelatenzbegrenzung zum Schutz vor Modell-Extraktion und Inversionsangriffen                      | 11.4.2, 11.5.1       |
| MCP-Ausführungsauslagerungsgrenzen, Zeitüberschreitungen, Rekursionsgrenzen und Sicherungsmechanismen | 10.5.2               |
| Erkennung und Blockierung anomaler Nutzungsmuster                                                     | 13.2.4, ASVS v5 V2.4 |
| Ressourcenkontingente (CPU, Speicher, GPU) für die Infrastruktur                                      | 4.6.1                |
| Schwellenwertbasierter Schutz wird bei Ressourcenerschöpfung ausgelöst                                | 4.6.2                |

Häufige Fallstricke: Ratenbegrenzungen pro Endpunkt festlegen, aber nicht pro Agent-Sitzung; Tool-Fan-out nicht berücksichtigen, wenn Budgets berechnet werden; keine Circuit Breaker für rekursive Agent-Ketten vorsehen.

---

## AD.10 Sandboxing & Prozessisolation

Isolieren Sie Workloads, Tools, Modelle und Agents, um Fehler einzudämmen und die seitliche Ausbreitung zu verhindern.

| Control / Technik                                                               | Anforderungs-IDs           |
| ------------------------------------------------------------------------------- | -------------------------- |
| Minimale Betriebssystem-Berechtigungen und Linux-Fähigkeiten                    | 4.1.1                      |
| Mandatory Access Control (seccomp, AppArmor, SELinux)                           | 4.1.2                      |
| Nur-Lese-Root-Dateisystem mit restriktiven Mount-Optionen                       | 4.1.3                      |
| Erkennung von Runtime-Privilege-Escalation und Container-Escape                 | 4.1.4                      |
| TEE / Vertrauliche Computerverarbeitung mit Remote-Atestation                   | 4.1.5, 4.5.4, 4.5.6, 4.5.8 |
| Untrusted AI-Modell-Sandboxing mit Netzwerktrennung                             | 4.5.1, 4.5.2               |
| Tool- und Plugin-Isolierung in Sandboxes (Container, VM, WASM, OS-Sandbox)      | 9.3.1                      |
| Sandbox-Escape-Erkennung mit automatisierter Tool-Quarantäne                    | 9.3.6                      |
| Agent-Isolation über Mandanten, Sicherheitsdomänen und Umgebungen hinweg        | 9.8.1                      |
| GPU-Speicherisolierung (MIG / VM-Partitionierung) mit Peer-to-Peer-Verhinderung | 4.7.5                      |
| On-Device-Prozess-, Speicher- und Dateizugriffsisolation                        | 4.8.7                      |
| MCP-stdio- lokale-only- Durchsetzung mit Schutz vor Terminal-Injektionen        | 10.6.1                     |
| Durchsetzung von MCP-Mandanten- und Umgebungsgrenzen                            | 10.6.3                     |

Häufige Fallstricke: die gemeinsame Nutzung von Infrastruktur zwischen Entwicklung und Produktion; die Gewährung von mehr Berechtigungen als erforderlich für Container; das Nicht-Einschränken des Zugriffs auf den Cloud-Metadatenservice durch KI-Workloads.

---

## AD.11 Netzsegmentierung & Egress-Steuerung

Control Sie Netzwerkgrenzen, Datenfluss und ausgehenden Zugriff für KI-Workloads.

| Control / Technik                                                                                  | Anforderungs-IDs |
| -------------------------------------------------------------------------------------------------- | ---------------- |
| Standardmäßig verweigernde Netzwerkrichtlinien mit expliziten Zulassungslisten                     | 4.3.1            |
| Netzwerksegmentierung über die Umgebungen Entwicklung / Test / Produktion hinweg                   | 4.3.2, 3.4.1     |
| Trennen Sie IAM-Rollen und Sicherheitsgruppen pro Umgebung ohne gemeinsam genutzte Principal(s)    | 4.3.6            |
| Eingeschränkter Zugriff auf administrative Funktionen und Blockierung des Cloud-Metadaten-Dienstes | 4.3.3            |
| Ausgehender Datenverkehr auf genehmigte Ziele beschränken, mit Protokollierung                     | 4.3.5            |
| Egress-Allowlists für Trainingsumgebungen                                                          | 3.4.4            |
| MCP Egress-Allowlist mit Blockierung durch den Cloud-Metadaten-Service                             | 10.5.1           |
| MCP-Dynamic-Dispatch und Verhinderung reflektierender Aufrufe                                      | 10.6.2           |
| Standardmäßig verweigerte ereignisübergreifende Agentenerkennung und Aufrufe                       | 9.8.1            |
| Ursprungs- und Host-Header-Validierung für DNS-Rebinding-Abwehr                                    | 10.3.4           |
| SSE-öffentliche Internetblockierung                                                                | 10.3.3           |

Häufige Fallstricke: Zulassen, dass KI-Workloads Cloud-Metadatendienste erreichen; keine Protokollierung des Egress-Verkehrs für forensische Analysen; das Versäumen der Validierung des Origin-Headers, wodurch DNS-Rebinding-Angriffe ermöglicht werden.

---

## AD.12 Lieferkette & Integrität von Artefakten

Überprüfen Sie Herkunft und Authentizität, scannen Sie Abhängigkeiten und erzwingen Sie die Integrität von Modellen, Frameworks, Datensätzen und Build-Artefakten.

| Control / Technik                                                                                  | Anforderungs-IDs          |
| -------------------------------------------------------------------------------------------------- | ------------------------- |
| Modell-Registry mit AI-BOM (SPDX, CycloneDX)                                                       | 3.1.1, 6.5.1              |
| Modellabhängigkeitsgraf-Tracking (Services, Agents, Umgebungen)                                    | 3.1.4                     |
| Modell-Originalprotokolle (Quelle, Prüfsummen der Trainingsdaten, Urheberschaft)                   | 3.1.5, 6.1.1              |
| Automatisierte reproduzierbare Builds                                                              | ASVS v5 V15 / SLSA        |
| SBOM-Erstellung aus automatisierten Builds                                                         | ASVS v5 V15.1.2 / SCVS    |
| Vergleich von Reproducible-Build-Hashes                                                            | SLSA Build L3             |
| CI-Pipeline Dependency Scanning                                                                    | ASVS v5 V15.2.1 / SCVS V5 |
| Kritische / schwerwiegende Sicherheitslücke, die in CI den Ablauf blockiert                        | ASVS v5 V15.1.1 / SCVS V5 |
| Versionsbindung durch Dependency-Pinning mit Lockfile-Enforcement                                  | SCVS V4 / CIS-Leitfaden   |
| Unveränderliche Digest-Referenzen für Container (keine veränderlichen Tags)                        | SCVS / CIS-Anleitung      |
| Erkennung abgelaufener und nicht mehr gepflegter Abhängigkeiten                                    | ASVS v5 V15.1.1, V15.2.1  |
| Genehmigte Quellenspezifikation für AI-Artefakte                                                   | 6.2.1                     |
| Scan auf bösartige Layer und Trojaner-Trigger                                                      | 6.1.2                     |
| Verbot des unsicheren Deserialisierungsformats und formatbewusstes Scannen beim Laden zur Laufzeit | 4.1.3                     |
| Bewertung der Vergiftung externer Datensätze (Fingerprinting, Ausreißererkennung)                  | 6.3.1                     |
| Urheberrechts- und PII-Erkennung in externen Datensätzen                                           | 6.3.2                     |
| Datensatzursprung- und Herkunftsdokumentation                                                      | 6.3.3                     |
| AI BOM kryptografische Signierung                                                                  | 6.5.2                     |
| Build-Attribut-aufbewahrung                                                                        | SLSA-Build-Track          |

Häufige Fallstricke: keine Feinabstimmungs-Datensätze auf Vergiftung zu prüfen; keine Rollback-Verfahren vorzusehen, wenn ein kompromittiertes Modell erkannt wird; AI-BOMs als statische Dokumente zu behandeln statt als versionierte Artefakte mit Versionskontrolle.

---

## AD.13 Bereitstellung & Lifecycle-Management

Verwalten Sie Modellbereitstellung, Rollback, Außerbetriebnahme und Notfallmaßnahmen.

| Control / Technik                                                                                      | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------------------ | ---------------- |
| Automatisierte Tests zur Validierung von Eingaben vor dem Deployment                                   | 3.2.1            |
| Automatisiertes Testen der Bereinigung von Ausgaben vor der Bereitstellung                             | 3.2.2            |
| Sicherheitsbewertungen mit Bestehen/Nichtbestehen-Schwellenwerten vor der Bereitstellung               | 3.2.3            |
| Agent-Workflow, Tool-, MCP- und RAG-Integrationstests                                                  | 3.2.4            |
| Unveränderliche Audit-Logs für Modelländerungen                                                        | 3.2.5            |
| Bereitstellungsvalidierung mit Fehlerblockierung und Genehmigung für die Außerkraftsetzung             | 3.2.6            |
| Canary / Blue-Green-Deployments mit automatischen Rollback-Auslösern                                   | 3.3.1            |
| Parallelbereitstellungskohortenisolierung (A/B, Canary, Shadow)                                        | 3.3.5            |
| Atomare Zustandswiederherstellung beim Rollback (Gewichte, Konfiguration, Adapter, Sicherheitsmodelle) | 3.3.2            |
| Notfallmodell-Abschaltfunktion mit vorgegebener Reaktionszeit                                          | 3.3.3            |
| Shutdown-Kaskade zu Tools, MCP, RAG, Anmeldeinformationen, Speicher-Stores                             | 3.3.4            |
| Trennung von Entwicklungs / Test / Produktionsumgebungen                                               | 3.4.1            |
| Keine gemeinsame Infrastruktur über Umgebungsgrenzen hinweg                                            | 3.4.2            |
| Versionskontrolle für alle Entwicklungsartefakte (Hyperparameter, Skripte, Prompts, Richtlinien)       | 3.4.3            |
| Sicheres Löschen von Modellartefakten und kryptografische Vernichtung bei Stilllegung                  | 3.5.1            |
| Widerruf der Model-Signatur und Registrierungssperrliste bei Außerbetriebnahme                         | 3.5.2            |
| AI-spezifische Incident-Response für Lieferketten (Modell-Rollback, Signatur-Widerruf)                 | 6.4.1            |

Häufige Fallstricke: nicht testen der Rollback-Verfahren, bevor sie benötigt werden; Zurücklassen stillgelegter Modellartefakte in Serving-Caches; das Fehlen eines Shutdown-Cascades zu nachgelagerten Tools und MCP-Verbindungen.

---

## AD.14 Datenschutz & Datenminimierung

Schützen Sie personenbezogene Daten und setzen Sie die Rechte der betroffenen Personen über den gesamten KI-Lebenszyklus hinweg durch.

| Control / Technik                                                                                        | Anforderungs-IDs       |
| -------------------------------------------------------------------------------------------------------- | ---------------------- |
| Datenminimierung beim Training (unnotwendige Merkmale, PII, geleakte Testdaten ausschließen)             | 1.1.2                  |
| Anonymisierung von gelabelten Daten und granularer Redaction                                             | 1.3.5                  |
| Direkte- und Quasi-Identifikator-Entfernung                                                              | 12.1.1                 |
| Messung von k-Anonymität und l-Vielfalt mit automatisierten Audits                                       | 12.1.2                 |
| Synthetische Daten mit formalen Rückidentifizierungsrisiko-Bewertungsgrenzen                             | 12.1.4                 |
| Datenlöschungsausbreitung (Datensätze, Checkpoints, Embeddings, Protokolle, Backups)                     | 12.2.1                 |
| Maschinelles Unlearning mit zertifizierten Algorithmen                                                   | 12.2.2                 |
| Schattenmodellbewertung der Wirksamkeit des Unlernens                                                    | 12.2.3                 |
| Datenschutzverlust-Buchführung mit Epsilon-Budget-Tracking und Benachrichtigungen                        | 12.3.1, 12.3.5         |
| Formale Differential-Privacy-Beweise (einschließlich Post-Training und Einbettungen)                     | 12.3.3                 |
| Zweck-Tags mit maschinenlesbarer Ausrichtung und Laufzeitdurchsetzung                                    | 12.4.1, 12.4.2, 12.4.5 |
| Consent Management Platform (CMP) mit Opt-in-Tracking                                                    | 12.5.1                 |
| Offenlegung des Consent-Token-API und Validierung des Scope auf Model-Seite                              | 12.5.2, 12.5.4         |
| Verarbeitung des Widerrufs der Einwilligung (< 24-Stunden-SLA)                                           | 12.5.3                 |
| Lokale differentielle Privatsphäre im föderierten Lernen (Client-seitiges Rauschen)                      | 12.6.1                 |
| Vergiftungsresistente Aggregation (Krum, getrimmter Mittelwert)                                          | 12.6.3                 |
| PII-Erkennung und -Entfernung in externen Datensätzen                                                    | 6.3.2                  |
| Sitzungskontext wird am Sitzungsende verworfen (nicht in nachfolgenden Sitzungen verfügbar)              | 8.3.7                  |
| Vom Abruf ausgeschlossene Inhalte aus den Suchergebnissen ausgeschlossen, während die Quarantäne bestand | 8.3.8                  |

Häufige Fallstricke: das Löschen von Datensätzen aus der Datenbank, aber nicht aus Modell-Checkpoints oder Embeddings; das Nichtberücksichtigen der Aufsummierung des Epsilon-Budgets über Abfragen hinweg; die Anonymisierung als einen einmaligen Schritt zu behandeln.

---

## AD.15 Adversarial Testing & Model Hardening

Testen Sie auf Umgehung, Extraktion, Inversion, Vergiftung und Angriffe zur Umgehung der Ausrichtung und verteidigen Sie sich dagegen.

| Control / Technik                                                                                                                                                                                                                                                            | Anforderungs-IDs |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Ablehnungs- und sichere-Vollständigung-Schutzvorkehrungen                                                                                                                                                                                                                    | 11.1.1           |
| Red-Team- und Jailbreak-Test-Suiten (versionsverwaltet)                                                                                                                                                                                                                      | 11.1.2           |
| Automatisierte Bewertung von schädlichen Content-Raten mit Regressionsdetektion                                                                                                                                                                                              | 11.1.3           |
| RLHF / Constitutional AI-Alignment-Training                                                                                                                                                                                                                                  | 11.1.4           |
| Adversarial Training und Defensive Distillation                                                                                                                                                                                                                              | 11.2.3           |
| Adversarial robuste Distillation — destillieren Sie den Teacher in den Student mithilfe adversarialem Training, sodass der Student sowohl Robustheit als auch Genauigkeit übernimmt (Implementierungsbeispiel für 11.2.3)                                                    | 11.2.3           |
| Formale Robustheitsverifikation (zertifizierte Schranken, Intervallgrenzen-Propagation)                                                                                                                                                                                      | 11.2.5           |
| Erkennung von Angriffsbeispielen mit produktionsseitigem Alarmieren                                                                                                                                                                                                          | 11.2.2           |
| Modell-Ensemble als Umgehungs-Eindämmung — leite Abfragen über unabhängig trainierte Modelle weiter und kennzeichne Uneinstimmigkeiten über einem Schwellenwert (Implementierungsbeispiel für 11.2.2)                                                                        | 11.2.2           |
| Kalibrierung und Störungsausgabe für den Datenschutz                                                                                                                                                                                                                         | 11.3.1           |
| Konfidenz-Obfuskation / Output-Perturbation — geben kalibrierte, jedoch absichtlich ungenaue Konfidenzwerte zurück, um die Modellausleitung und Membership-Inference zu erschweren (Implementierungsbeispiel für 11.3.1)                                                     | 11.3.1           |
| DP-SGD (differenziell private Schulung) mit dokumentiertem Epsilon                                                                                                                                                                                                           | 11.3.2           |
| PATE (Private Aggregation of Teacher Ensembles) — Trainieren eines Schülermodells unter Verwendung einer verrauschten Aggregation der Ausgaben von Lehrmodellen, sodass kein einzelner Trainingsdatensatz offengelegt wird (Implementierungsbeispiel für 11.3.2)             | 11.3.2           |
| Mitgliedschaftsangriffs-Simulation (Shadow-Modell, Likelihood-Ratio)                                                                                                                                                                                                         | 11.3.3           |
| Modelauszugs-Erkennung (Query-Musteranalyse, Diversitätsmessung)                                                                                                                                                                                                             | 11.5.3           |
| Statistische Ausreißererkennung und Konsistenzbewertung bei externen Eingaben                                                                                                                                                                                                | 11.6.1           |
| Adaptive Attack-Evasion-Tests                                                                                                                                                                                                                                                | 11.6.4           |
| Sicherheitsorientierte sekundäre Überprüfungsmechanismen (zweites Modell, regelbasiert)                                                                                                                                                                                      | 11.8.1           |
| Selbstmodifikations-Einschränkung mit Geltungsbereichsgrenzen und Ratenlimits                                                                                                                                                                                                | 11.9.1, 11.9.4   |
| Selbstmodifikations-Reversibilität und Integritätsprüfung, die ein Rollback auf einen bekannten Sollzustand ermöglichen                                                                                                                                                      | 11.9.6           |
| Datenaugmentation mit veränderten Eingaben für Robustheit beim Training                                                                                                                                                                                                      | 1.4.4            |
| RONI (Reject On Negative Influence)-Filtering -- berechnen Sie für jede Trainingsprobe den Influence-Score und verwerfen Sie diejenigen, die die Leistung auf einem gehaltenen Datensatz über einen Schwellenwert hinaus verschlechtern (Implementierungsbeispiel für 1.4.2) | 1.4.2            |
| Gradient-Fingerprinting / Analyse von Gradienten pro Beispiel — Erkennung abnormaler Gradienten-Normen oder -Richtungen, die auf vergiftete Samples während des Trainings hinweisen (Implementierungsbeispiel für 1.4.2)                                                     | 1.4.2            |
| Aktivierungs-Clustering — Clustern von Zwischenausgaben zur Erkennung von Backdoor-assoziierten Subpopulationen (Implementierungsbeispiel für 1.4.2)                                                                                                                         | 1.4.2            |

Häufige Fallstricke: nur bekannte Jailbreak-Muster zu testen, ohne adaptive Angriffe; Red-Team-Suiten nach Modell-Updates nicht zu aktualisieren; sich auf eine einzelne Abwehrmaßnahme zu verlassen, statt auf Defense-in-Depth.

---

## AD.16 Logging & Audit

Erfassen Sie sicherheitsrelevante Ereignisse mit Integritätsschutz für forensische Analysen und Compliance.

| Control / Technik                                                                                                              | Anforderungs-IDs       |
| ------------------------------------------------------------------------------------------------------------------------------ | ---------------------- |
| Protokollierung von Prompt- und Antwortvorgängen mit Metadaten (Zeitstempel, Benutzer-ID, Sitzung, Modellversion)              | 13.1.1                 |
| Sichere, zugriffskontrollierte Protokoll-Repositorys mit Aufbewahrungsrichtlinien                                              | 13.1.2                 |
| Protokollverschlüsselung im Ruhezustand und während der Übertragung                                                            | 13.1.3                 |
| PII-, Credential- und proprietäre Informationsanonymisierung in Protokollen                                                    | 13.1.4                 |
| Protokollierung von Policy-Entscheidungen und sicherheitsbezogenen Filterungsmaßnahmen                                         | 13.1.5                 |
| Kryptografische Protokoll-Signaturen mit schreibgeschriebenem Speicher                                                         | 13.1.6                 |
| Manipulationssicherer Audit-Log-Speicher (append-only, WORM, Hashverkettung)                                                   | 9.4.3                  |
| Audit-Log-Kontextfelder ausreichend für die forensische Rekonstruktion (Akteur, Delegation, Richtlinie, Parameter, Ergebnisse) | 9.4.5                  |
| Agent actions signieren mit Chain-ID-Bindung und Zeitstempeln                                                                  | 9.4.2                  |
| Unveränderliche Audit-Trail-Einträge für Modelländerungen (Akteur, Änderungsart, vorher/nachher)                               | 3.2.5                  |
| Unveränderliches Löschprotokoll für regulatorische Prüfpfade                                                                   | 12.2.4                 |
| CI/CD-Auditprotokoll-Streaming an SIEM                                                                                         | ASVS v5 V16.4.3        |
| Erkennungsregeln für anomale Paketabrufe und manipulierte Build-Schritte                                                       | ASVS v5 V16.3.3        |
| DAG-Visualisierung mit Zugriffskontrollen und Manipulationserkennung                                                           | 13.7.1, 13.7.2, 13.7.3 |
| Sicherheitsverletzungs-Metriken-Logging                                                                                        | 7.6.1                  |
| MCP-Richtlinienänderungsprüfung mit Protokollierung (Zeitstempel, Autor, Begründung)                                           | 11.7.3                 |
| Verfahren zum Rollback bei Policy-Änderungen und Tests                                                                         | 11.7.5                 |
| Detailliertes Protokollieren der Selbstmodifikation (was sich geändert hat, wann, unter welcher Autorisierung)                 | 11.9.3                 |

Häufige Fallstricke: Protokollieren von Prompts ohne Anonymisierung von PII; Verwendung eines veränderbaren Protokollspeichers ohne Integritätsschutz; Nichtbereitstellung ausreichenden Kontexts für die forensische Rekonstruktion.

---

## AD.17 Überwachung, Alarmierung & Incident Response

Anomalien erkennen, auf Bedrohungen hinweisen und auf Sicherheitsvorfälle in KI-Systemen reagieren.

| Control / Technik                                                                                                        | Anforderungs-IDs       |
| ------------------------------------------------------------------------------------------------------------------------ | ---------------------- |
| Erkennung von Jailbreak- und Prompt-Injection-Versuchen (signaturbasiert)                                                | 13.2.1                 |
| SIEM-Integration mit standardisierten Log-Formaten                                                                       | 13.2.2                 |
| AI-spezifische Ereignis-Anreicherung (Modell-ID, Konfidenz, Filterentscheidungen)                                        | 13.2.3                 |
| Erkennungen von Verhaltensabweichungen (ungewöhnliche Muster, exzessive Wiederholungsversuche, systematisches Sondieren) | 13.2.4, 13.2.5         |
| Echtzeit-Alarmierung bei Richtlinienverstößen und koordinierten Angriffskampagnen                                        | 13.2.6                 |
| Automatisierte Incident Response (Isolierung und Blockierung kompromittierter Modelle und bösartiger Benutzer)           | 13.2.7                 |
| Leistungsmetriken-Überwachung (Genauigkeit, Latenz, Fehlerquote) mit Alarmierung                                         | 13.3.1, 13.3.2, 13.3.3 |
| Leistungsverschlechterung: Neuqualifizierungs- und Austausch-Workflow-Trigger                                            | 13.3.10                |
| Halluzinations-Erkennung Monitoring                                                                                      | 13.3.4                 |
| Halluzinationsrate-Zeitreihenverfolgung                                                                                  | 13.3.11                |
| Erkennung von Data-Drift und Concept-Drift                                                                               | 13.6.2, 13.6.3         |
| Modell-Extraktion-Alarmgenerierung mit Abfrage-Metadatenprotokollierung                                                  | 11.5.2                 |
| Model Extraction Alert IR Playbook Integration                                                                           | 11.5.6                 |
| Erkennung emergenter Multi-Agent-Verhaltensweisen (Oszillation, Deadlock, Broadcast-Stürme)                              | 9.8.2                  |
| KI-spezifische Incident-Response-Pläne (Modellkompromittierung, Datenvergiftung, adversarialer Angriff)                  | 13.5.1                 |
| KI-spezifische Forensik-Tools zur Untersuchung des Modellverhaltens                                                      | 13.5.2                 |
| Sicherheitsverletzungs-Rate-Alarmierung                                                                                  | 7.6.2                  |
| Echtzeit-Sicherheitsrichtlinien-Updates ohne vollständige Neubereitstellung                                              | 11.7.1                 |
| Beschleuniger-Telemetrie und Erkennung von Seitkanal-Anomalien                                                           | 4.7.8                  |
| Proaktive Validierung des Agentenverhaltens mit Risikobewertung                                                          | 13.8.1, 13.8.2         |

Häufige Fallstricke: keine Korrelation von AI-spezifischen Ereignissen mit umfassenderen SIEM-Warnmeldungen; Modell-Drift als geplanten Check zu behandeln, statt als kontinuierliches Monitoring; während der Incident Response keine AI-spezifischen forensischen Tools einzusetzen.

---

## AD.18 Erklärbarkeit & Transparenz

Ermöglichen Sie menschliches Verständnis der Modellentscheidungen durch Interpretierbarkeit, Dokumentation und Quantifizierung der Unsicherheit.

| Control / Technik                                                             | Anforderungs-IDs |
| ----------------------------------------------------------------------------- | ---------------- |
| Menschlich lesbare Entscheidungserklärungen                                   | 14.4.1           |
| Erklärungsqualitätsbewertung (Human-Evaluationsstudien)                       | 14.4.2           |
| SHAP, LIME und Feature-Importance-Scores                                      | 14.4.3           |
| Gegenfaktische Erklärungen                                                    | 14.4.4           |
| Modellkarten (beabsichtigte Verwendung, bekannte Fehler, Leistungskennzahlen) | 14.5.1, 14.5.2   |
| Dokumentation zu ethischen Überlegungen und zur Bewertung von Verzerrungen    | 14.5.3           |
| Modelkarten-Versionskontrolle und Änderungsverfolgung                         | 14.5.4           |
| Quantifizierung von Unsicherheit (Konfidenzwerte, Entropiemaße)               | 14.6.1           |
| Menschliche Überprüfungs-Trigger bei Unsicherheits-Schwellenwerten            | 14.6.2           |
| Unsicherheitskalibrierung anhand von Ground Truth                             | 14.6.3           |
| Mehrstufige Unsicherheitsfortpflanzung                                        | 14.6.4           |
| Artefakte zur Modellinterpretierbarkeit (Aufmerksamkeitskarten, Attribution)  | 7.5.3            |
| Anzeige von Zusammenfassung von Vertrauen und Begründung                      | 7.5.2            |

Häufige Fallstricke: Erklärungen bereitzustellen, die System-Prompts oder interne Architektur offenlegen; Unsicherheitsabschätzungen nicht zu kalibrieren; Modellkarten als statische Dokumente statt als lebendige Artefakte zu behandeln.

---

## AD.19 Human Oversight & Approval Gates

Erfordert eine menschliche Überprüfung und Genehmigung für hochwirksame, irreversible oder sicherheitskritische Aktionen.

| Control / Technik                                                                                                      | Anforderungs-IDs |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Hochwirksame Genehmigungs-Gates für Maßnahmen (Bereitstellung, Löschung, Finanzen, Benachrichtigung)                   | 9.2.1            |
| Freigabe-Parameterbindung (Genehmigen-eins-ausführen-anderen verhindern)                                               | 9.2.2            |
| Hochwirksame Bestätigung der Absicht mit exakt gebundenen Parametern und schneller Ablaufzeit                          | 9.7.2            |
| Bestätigungsabfrage für MCP-Aktionen mit hohem Risiko (Datenlöschung, Finanzen, Systemkonfiguration)                   | 10.5.3           |
| Menschliche Genehmigung für die Generierung von Inhalten mit hohem Risiko                                              | 7.3.5            |
| Menschliche Überprüfung bei Überschreitung der Unsicherheits-Schwelle                                                  | 14.6.2           |
| Menschliche Überprüfung bei Anomalieerkennung                                                                          | 11.6.3           |
| Erweitertes Monitoring und menschliches Eingreifen bei Sicherheitswarnungen                                            | 11.8.3           |
| Sicherheitskritische proaktive Maßnahme mit Genehmigungskette-Logging genehmigen                                       | 13.8.4           |
| Quarantäne für Modelle mit hohem Risiko mit menschlicher Überprüfung und Freigabe durch Unterschrift                   | 6.1.3            |
| Nachbedingungsprüfung mit Einfassung bei Nichtübereinstimmung                                                          | 9.7.3            |
| Ausgleichsmaßnahmen und transaktionales Rollback bei Fehlschlag                                                        | 9.2.3            |
| Zwischenstufen der operativen Degradierung (Tool-Deaktivierung, Modellwechsel, Nur-Lese-Modus, Quellendatenentfernung) | 14.1.5           |

Häufige Fallstricke: keine verbindliche Genehmigung für exakte Parameter erlauben, wodurch ein Bait-and-Switch möglich wird; Bestätigungstokens ohne schnelle Ablaufzeit; fehlende Nachbedingungen-Checks nach ausgeführten genehmigten Aktionen.

---

## AD.20 Hardware- und Accelerator-Sicherheit

Sichere KI-Beschleuniger-Hardware, Firmware, Speicher, Verbindungen und Edge-Geräte.

| Control / Technik                                                                          | Anforderungs-IDs |
| ------------------------------------------------------------------------------------------ | ---------------- |
| GPU/TPU-Integritätsvalidierung mit Hardware-Attestierung (TPM, DRTM)                       | 4.7.1            |
| GPU-Speicherisolation und -bereinigung zwischen Workloads und Mandanten                    | 4.7.2            |
| Signierte GPU-Firmware mit Versions-Pinning und Attestierung                               | 4.7.3            |
| VRAM-Zeroing und Geräte-Reset zwischen Jobs                                                | 4.7.4            |
| MIG / VM-GPU-Partitionierung mit Verhinderung des Peer-to-Peer-Zugriffs                    | 4.7.5            |
| HSM mit FIPS 140-3 Level 3-Zertifizierung                                                  | 4.7.6            |
| Authentifizierte Beschleuniger-Interconnects (NVLink, PCIe, InfiniBand, RDMA)              | 4.7.7            |
| Beschleuniger-Telemetrieexport (Leistung, Temperatur, Fehlerkorrektur)                     | 4.7.8            |
| Edge-Gerät Secure Boot mit Firmware-Rollback-Schutz                                        | 4.8.3            |
| Modellsignaturüberprüfung auf Edge-Geräten                                                 | 4.8.2            |
| Mobile verifizierter Start, Code-Signierung und Laufzeit-Integritätsprüfungen              | 4.8.4            |
| Byzantinertoleranter Konsens für verteilte KI                                              | 4.8.5            |
| On-Device-Prozess-, Speicher- und Datei-Zugriffsisolation                                  | 4.8.7            |
| Modell-Obfuskation und -Deobfuskation innerhalb einer vertrauenswürdigen Laufzeitumgebung  | 4.8.9            |
| Sichere Offline-Edge-Betriebsweise mit hardwaregestütztem verschlüsseltem lokalem Speicher | 4.8.10           |

Häufige Fallstricke: VRAM nicht zwischen Mandanten-Workloads zu bereinigen; Debug-Firmware in der Produktion auszuführen; unverschlüsselte Interconnects in Multi-Tenant-GPU-Clustern zuzulassen; die Attestierung von Firmware-Updates zu vernachlässigen.

---

## References

* [NIST AI Risk Management Framework 1.0](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)
* [ISO/IEC 42001:2023: AI Management Systems Requirements](https://www.iso.org/standard/81230.html)
* [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
* [OWASP Application Security Verification Standard (ASVS)](https://owasp.org/www-project-application-security-verification-standard/)
* [NIST SP 800-218A: Secure Software Development Practices for Generative AI](https://csrc.nist.gov/pubs/sp/800/218/a/final)

