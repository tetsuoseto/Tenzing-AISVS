# C4-Infrastruktur, Konfiguration und Bereitstellungssicherheit

## Kontrollziel

Die KI-Infrastruktur muss durch sichere Konfiguration, Laufzeitisolierung, vertrauenswürdige Bereitstellungspipelines und umfassendes Monitoring gegen Privilegieneskalation, Manipulation in der Lieferkette und seitliche Bewegung gehärtet werden. Nur validierte und autorisierte Infrastrukturkomponenten gelangen über kontrollierte Prozesse, die Sicherheit, Integrität und Nachvollziehbarkeit gewährleisten, in die Produktion.

---

## C4.1 Laufzeit-Umgebungsisolation

Verhindern Sie Container-Ausbrüche und Privilegienerhöhungen durch Betriebssystemebene-Isolationsprimitive.

|   #   | Beschreibung                                                                                                                                                                                                                                                                               | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 4.1.1 | Stellen Sie sicher, dass alle KI-Arbeitslasten mit den minimal erforderlichen Berechtigungen im Betriebssystem ausgeführt werden, indem beispielsweise unnötige Linux-Fähigkeiten im Fall eines Containers entfernt werden.                                                                |   1   |  D/V  |
| 4.1.2 | Stellen Sie sicher, dass Workloads durch Technologien geschützt sind, die Exploits einschränken, wie Sandboxing, Seccomp-Profile, AppArmor, SELinux oder Ähnliches, und dass die Konfiguration angemessen ist.                                                                             |   1   |  D/V  |
| 4.1.3 | Stellen Sie sicher, dass Workloads mit einem schreibgeschützten Root-Dateisystem ausgeführt werden und dass alle beschreibbaren Mounts explizit definiert und mit restriktiven Optionen gesichert sind, die Ausführung und Privilegieneskalation verhindern (z. B. noexec, nosuid, nodev). |   2   |  D/V  |
| 4.1.4 | Überprüfen Sie, dass die Laufzeitüberwachung Privilegieneskalations- und Containerentweichungsverhalten erkennt und fehlverhaltende Prozesse automatisch beendet.                                                                                                                          |   3   |  D/V  |
| 4.1.5 | Stellen Sie sicher, dass KI-Anwendungen mit hohem Risiko nur in hardware-isolierten Umgebungen (z. B. TEEs, vertrauenswürdige Hypervisoren oder Bare-Metal-Knoten) ausgeführt werden, und zwar ausschließlich nach erfolgreicher Fernbegutachtung.                                         |   3   |  D/V  |

---

## C4.2 Sichere Build- und Deployment-Pipelines

Sichern Sie kryptografische Integrität und Lieferkettensicherheit durch reproduzierbare Builds und signierte Artefakte.

|   #   | Beschreibung                                                                                                                                                                              | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.2.1 | Überprüfen Sie, dass Builds vollständig automatisiert sind und eine Software-Stückliste (SBOM) erstellen.                                                                                 |   1   |  D/V  |
| 4.2.2 | Überprüfen Sie, dass Build-Artefakte kryptographisch mit Herkunftsmetadaten signiert sind, die unabhängig verifiziert werden können.                                                      |   2   |  D/V  |
| 4.2.3 | Stellen Sie sicher, dass die Signaturen von Build-Artefakten und die Herkunftsmetadaten bei der Bereitstellungsfreigabe überprüft werden, und lehnen Sie nicht verifizierte Artefakte ab. |   2   |  D/V  |
| 4.2.4 | Stellen Sie sicher, dass Builds reproduzierbar sind und identische Ausgaben aus identischen Quellinputs erzeugen, was eine unabhängige Überprüfung der Build-Integrität ermöglicht.       |   3   |  D/V  |

---

## C4.3 Netzwerksicherheit & Zugriffskontrolle

Implementieren Sie Zero-Trust-Netzwerke mit Standard-Ablehnungsrichtlinien und verschlüsselter Kommunikation.

|   #   | Beschreibung                                                                                                                                                                                                                                                                         | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 4.3.1 | Überprüfen Sie, dass Netzwerkrichtlinien einen Default-Deny-Zugriff für Ingress und Egress durchsetzen, wobei nur die erforderlichen Dienste explizit erlaubt sind.                                                                                                                  |   1   |  D/V  |
| 4.3.2 | Überprüfen Sie, ob KI-Arbeitslasten in verschiedenen Umgebungen (Entwicklung, Test, Produktion) in isolierten Netzwerksegmenten ohne direkten Internetzugang sowie ohne gemeinsame Identitätsrollen, Sicherheitsgruppen oder Verbindungen zwischen den Umgebungen ausgeführt werden. |   1   |  D/V  |
| 4.3.3 | Stellen Sie sicher, dass administrative und Remote-Zugriffsprotokolle sowie der Zugriff auf Cloud-Metadaten-Services eingeschränkt sind und eine starke Authentifizierung erfordern.                                                                                                 |   1   |  D/V  |
| 4.3.4 | Stellen Sie sicher, dass die Kommunikation zwischen Diensten Mutual TLS mit Zertifikatsvalidierung und regelmäßiger automatischer Rotation verwendet.                                                                                                                                |   2   |  D/V  |
| 4.3.5 | Stellen Sie sicher, dass der ausgehende Datenverkehr auf genehmigte Ziele beschränkt ist und alle Anfragen protokolliert werden.                                                                                                                                                     |   3   |  D/V  |

## C4.4 Geheimnisse und kryptografisches Schlüsselmanagement

Schützen Sie Geheimnisse und kryptografische Schlüssel mit sicherer Speicherung, automatischer Rotation und starken Zugriffskontrollen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.4.1 | Stellen Sie sicher, dass Geheimnisse in einem dedizierten Geheimnisverwaltungsystem mit Verschlüsselung im Ruhezustand gespeichert sind und von Anwendungs-Workloads isoliert sind.                                                                                                   |   1   |  D/V  |
| 4.4.2 | Überprüfen Sie, ob der Zugriff auf Produktionsgeheimnisse eine starke Authentifizierung erfordert.                                                                                                                                                                                    |   1   |  D/V  |
| 4.4.3 | Stellen Sie sicher, dass Geheimnisse zur Laufzeit über ein dediziertes Geheimnisverwaltungsystem in Anwendungen bereitgestellt werden. Geheimnisse dürfen niemals in Quellcode, Konfigurationsdateien, Build-Artefakten, Container-Images oder Umgebungsvariablen eingebettet werden. |   1   |  D/V  |
| 4.4.4 | Stellen Sie sicher, dass kryptografische Schlüssel in hardwaregestützten Modulen (z. B. HSMs, Cloud-KMS) erzeugt und gespeichert werden.                                                                                                                                              |   2   |  D/V  |
| 4.4.5 | Überprüfen Sie, ob die Rotation von Geheimnissen automatisiert ist.                                                                                                                                                                                                                   |   2   |  D/V  |

---

## C4.5 AI-Workload-Sandboxing & Validierung

Isolieren Sie nicht vertrauenswürdige KI-Modelle in sicheren Sandboxes und schützen Sie sensible KI-Arbeitslasten mithilfe von Trusted Execution Environments (TEEs) und Technologien für vertrauliches Rechnen.

|   #   | Beschreibung                                                                                                                                                                                                       | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 4.5.1 | Überprüfen Sie, dass externe oder nicht vertrauenswürdige KI-Modelle in isolierten Sandboxes ausgeführt werden.                                                                                                    |   1   |  D/V  |
| 4.5.2 | Stellen Sie sicher, dass sandboxed Workloads standardmäßig keine ausgehende Netzwerkverbindung haben und jeglicher erforderlicher Zugriff explizit definiert ist.                                                  |   1   |  D/V  |
| 4.5.3 | Überprüfen Sie, dass die Workload-Attestation vor dem Laden des Modells durchgeführt wird, um einen kryptografischen Nachweis zu gewährleisten, dass die Ausführungsumgebung nicht manipuliert wurde.              |   2   |  D/V  |
| 4.5.4 | Stellen Sie sicher, dass vertrauliche Arbeitslasten innerhalb einer Trusted Execution Environment (TEE) ausgeführt werden, die hardware-gestützte Isolation, Speicherverschlüsselung und Integritätsschutz bietet. |   3   |  D/V  |
| 4.5.5 | Stellen Sie sicher, dass vertrauliche Inferenzdienste die Modellauswertung durch verschlüsselte Berechnungen mit versiegelten Modellgewichten und geschützter Ausführung verhindern.                               |   3   |  D/V  |
| 4.5.6 | Stellen Sie sicher, dass die Orchestrierung vertrauenswürdiger Ausführungsumgebungen das Lebenszyklusmanagement, die Fernattestierung und verschlüsselte Kommunikationskanäle umfasst.                             |   3   |  D/V  |
| 4.5.7 | Stellen Sie sicher, dass sichere Mehrparteienberechnung (SMPC) kollaboratives KI-Training ermöglicht, ohne einzelne Datensätze oder Modellparameter offenzulegen.                                                  |   3   |  D/V  |

---

## C4.6 Verwaltung von KI-Infrastrukturressourcen, Sicherung und Wiederherstellung

Verhindern Sie Ressourcenauslastungsangriffe und gewährleisten Sie eine faire Ressourcenzuteilung durch Quoten und Überwachung. Erhalten Sie die Infrastrukturresilienz durch sichere Backups, getestete Wiederherstellungsverfahren und Maßnahmen zur Katastrophenwiederherstellung.

|   #   | Beschreibung                                                                                                                                                                                                                                                               | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.6.1 | Stellen Sie sicher, dass der Ressourcenverbrauch von Arbeitslasten durch Quoten und Limits (z. B. CPU, Arbeitsspeicher, GPU) begrenzt wird, um Denial-of-Service-Angriffe zu verhindern.                                                                                   |   1   |  D/V  |
| 4.6.2 | Überprüfen Sie, ob eine Ressourcenerschöpfung automatisierte Schutzmaßnahmen auslöst (z. B. Ratenbegrenzung oder Arbeitslastisolierung), sobald definierte CPU-, Speicher- oder Anforderungsschwellenwerte überschritten werden.                                           |   2   |  D/V  |
| 4.6.3 | Überprüfen Sie, dass Sicherungssysteme in isolierten Netzwerken mit separaten Zugangsdaten betrieben werden und das Speichersystem entweder in einem luftgetrennten Netzwerk läuft oder einen WORM-Schutz (Write-Once-Read-Many) gegen unbefugte Änderungen implementiert. |   2   |  D/V  |

---

## C4.7 KI-Hardware-Sicherheit

Sichern Sie AI-spezifische Hardwarekomponenten, einschließlich GPUs, TPUs und spezialisierter AI-Beschleuniger.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                               | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.7.1 | Stellen Sie sicher, dass vor der Ausführung der Arbeitslast die Integrität des KI-Beschleunigers mittels hardwarebasierter Attestationsmechanismen (z. B. TPM, DRTM oder gleichwertig) validiert wird.                                                                                                     |   2   |  D/V  |
| 4.7.2 | Überprüfen Sie, dass der Speicher des Beschleunigers (GPU) zwischen Arbeitslasten durch Partitionierungsmechanismen mit Speichersanitierung zwischen den Aufgaben isoliert ist.                                                                                                                            |   2   |  D/V  |
| 4.7.3 | Überprüfen Sie, dass die Firmware des KI-Beschleunigers auf eine feste Version festgelegt, signiert und beim Start attestiert ist; nicht signierte oder Debug-Firmware wird blockiert.                                                                                                                     |   2   |  D/V  |
| 4.7.4 | Überprüfen Sie, dass VRAM und On-Package-Speicher zwischen Aufgaben/Mandanten auf Null gesetzt werden und dass Richtlinien für Geräte-Reset das Verbleiben von Daten zwischen Mandanten verhindern.                                                                                                        |   2   |  D/V  |
| 4.7.5 | Überprüfen Sie, ob Partitionierungs-/Isolationsfunktionen (z. B. MIG/VM-Partitionierung) pro Mandant durchgesetzt werden und den direkten Speicherzugriff zwischen Partitionen verhindern.                                                                                                                 |   2   |  D/V  |
| 4.7.6 | Stellen Sie sicher, dass Hardware-Sicherheitsmodule (HSMs) oder gleichwertige manipulationssichere Hardware die KI-Modellgewichte und kryptografischen Schlüssel schützen und eine Zertifizierung für ein entsprechendes Sicherheitsniveau besitzen (z. B. FIPS 140-3 Level 3 oder Common Criteria EAL4+). |   3   |  D/V  |
| 4.7.7 | Überprüfen Sie, dass Beschleunigerverbindungen (NVLink/PCIe/InfiniBand/RDMA/NCCL) auf genehmigte Topologien und authentifizierte Endpunkte beschränkt sind; unverschlüsselte Verbindungen zwischen Mandanten sind nicht erlaubt.                                                                           |   3   |  D/V  |
| 4.7.8 | Überprüfen Sie, ob die Telemetriedaten des Beschleunigers (Stromverbrauch, Temperatur, Fehlerkorrektur, Leistungszähler) an das zentralisierte Sicherheitsmonitoring exportiert werden und ob bei Anomalien, die auf Seitenkanäle oder verdeckte Kanäle hinweisen, Warnungen ausgelöst werden.             |   3   |   D   |

---

## C4.8 Edge- und verteilte KI-Sicherheit

Sichere verteilte KI-Einsätze einschließlich Edge-Computing, föderiertem Lernen und Multi-Site-Architekturen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                        | Ebene | Rolle |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.8.1 | Stellen Sie sicher, dass Edge-AI-Geräte sich bei der zentralen Infrastruktur mithilfe von gegenseitiger Authentifizierung mit Zertifikatsvalidierung (z. B. gegenseitiges TLS) authentifizieren.                                                                                                                                                    |   1   |  D/V  |
| 4.8.2 | Stellen Sie sicher, dass Modelle, die für Edge- oder Mobilgeräte bereitgestellt werden, während der Verpackung kryptografisch signiert sind und dass die Laufzeitumgebung auf dem Gerät diese Signaturen oder Prüfsummen vor dem Laden oder der Inferenz validiert; nicht verifizierte oder veränderte Modelle müssen abgelehnt werden.             |   1   |  D/V  |
| 4.8.3 | Stellen Sie sicher, dass Edge-Geräte Secure Boot mit verifizierten Signaturen und Rollback-Schutz implementieren, um Firmware-Downgrade-Angriffe zu verhindern.                                                                                                                                                                                     |   2   |  D/V  |
| 4.8.4 | Stellen Sie sicher, dass mobile oder Edge-Inferenzanwendungen plattformbezogene Anti-Manipulations-Schutzmaßnahmen implementieren (z. B. Code-Signierung, verifizierter Bootvorgang, Laufzeit-Integritätsprüfungen), die modifizierte Binärdateien, neu verpackte Anwendungen oder angehängte Instrumentierungs-Frameworks erkennen und blockieren. |   2   |  D/V  |
| 4.8.5 | Überprüfen Sie, dass die verteilte KI-Koordination byzantinisch fehlertolerante Konsensmechanismen mit Teilnehmervalidierung und Erkennung bösartiger Knoten verwendet.                                                                                                                                                                             |   3   |  D/V  |
| 4.8.6 | Stellen Sie sicher, dass die Kommunikation zwischen Edge und Cloud Bandbreitenbegrenzung, Datenkompression und sicheren Offline-Betrieb mit verschlüsselter lokaler Speicherung unterstützt.                                                                                                                                                        |   3   |  D/V  |
| 4.8.7 | Stellen Sie sicher, dass Inferenz-Laufzeiten auf dem Gerät Prozess-, Speicher- und Dateizugriffsisolation durchsetzen, um das Auslesen von Modellen, Debugging oder die Extraktion von Zwischen-Einbettungen und Aktivierungen zu verhindern.                                                                                                       |   3   |  D/V  |
| 4.8.8 | Stellen Sie sicher, dass Modellgewichte und sensible lokal gespeicherte Parameter mithilfe von hardwaregestützten Schlüssel-Speichern oder sicheren Enklaven (z. B. Android Keystore, iOS Secure Enclave, TPM/TEE) verschlüsselt sind, wobei die Schlüssel für den Benutzerspace unzugänglich sind.                                                 |   3   |  D/V  |
| 4.8.9 | Verifizieren Sie, dass Modelle, die in mobilen, IoT- oder Embedded-Anwendungen verpackt sind, im Ruhezustand verschlüsselt oder verfremdet sind und nur innerhalb einer vertrauenswürdigen Laufzeitumgebung oder eines sicheren Enklaven entschlüsselt werden, um eine direkte Extraktion aus dem App-Paket oder Dateisystem zu verhindern.         |   3   |  D/V  |

---

## Literaturverzeichnis

* [NIST Cybersecurity Framework 2.0](https://www.nist.gov/cyberframework)
* [CIS Controls v8](https://www.cisecurity.org/controls/v8)
* [Kubernetes Security Best Practices](https://kubernetes.io/docs/concepts/security/)
* [Cloud Security Alliance: Cloud Controls Matrix](https://cloudsecurityalliance.org/research/cloud-controls-matrix/)
* [ENISA: Secure Infrastructure Design](https://www.enisa.europa.eu/topics/critical-information-infrastructures-and-services)
* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

