# C4 Infrastruktur-, Konfigurations- & Bereitstellungssicherheit

## Kontrollziel

KI-spezifische Infrastrukturkomponenten müssen gegen Model Theft, Datenausleitung und Kontamination zwischen Mandanten gehärtet werden. Dieses Kapitel behandelt das Sandboxing von KI-Workloads, die Systemsicherheit von KI-Beschleunigerhardware und die Sicherheit von Edge-/verteilten KI-Bereitstellungen. Allgemeine Infrastruktur-Sicherheitsmaßnahmen (Container-Härtung, Netzwerksegmentierung, Secrets-Management, CI/CD-Pipeline-Sicherheit) werden in ASVS, CIS Benchmarks und NIST SP 800-53 behandelt und hier nicht wiederholt. KI-spezifische Supply-Chain-Kontrollen werden in C6 behandelt.

---

## C4.1 AI-Workload-Isolierung & Validierung

Isolieren Sie nicht vertrauenswürdige KI-Modelle in sicheren Sandboxes und schützen Sie sensible KI-Workloads mithilfe vertrauenswürdiger Ausführungsumgebungen (TEEs) und Technologien für vertrauliches Computing.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                               | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 4.1.1 | Stellen Sie sicher, dass externe oder nicht vertrauenswürdige KI-Modelle in isolierten Sandboxes ausgeführt werden.                                                                                                                                                                                                                                        |   1   |
| 4.1.2 | Überprüfen Sie, dass sandboxed Workloads standardmäßig über keine ausgehende Netzwerk-Konnektivität verfügen, und dass etwaig erforderlicher Zugriff explizit definiert ist.                                                                                                                                                                               |   1   |
| 4.1.3 | Stellen Sie sicher, dass das Laden von Modellartefakten eine explizite Zulassungsliste für Serialisierungsformate erzwingt, die keine willkürliche Codeausführung während der Deserialisierung erlauben, und dass Formate, die willkürliche Codeausführung ermöglichen (z.B. Python pickle mit uneingeschränkten Globals), standardmäßig abgelehnt werden. |   1   |
| 4.1.4 | Stellen Sie sicher, dass die Workload-Attribution vor dem Laden des Modells durchgeführt wird, und gewährleisten Sie einen kryptografischen Nachweis, dass die Ausführungsumgebung nicht manipuliert wurde.                                                                                                                                                |   2   |
| 4.1.5 | Verifizieren Sie, dass vertrauliche Workloads innerhalb einer vertrauenswürdigen Ausführungsumgebung (TEE) ausgeführt werden, die hardwaregestützte Isolation, Speicherverschlüsselung und Integritätsschutz bereitstellt.                                                                                                                                 |   3   |
| 4.1.6 | Verifizieren Sie, dass vertrauliche Inferenzdienste eine Modellextraktion durch verschlüsselte Berechnungen mit versiegelten Modellgewichten und geschützter Ausführung verhindern.                                                                                                                                                                        |   3   |
| 4.1.7 | Verifizieren Sie, dass Secure Multi-Party Computation (SMPC) kooperatives KI-Training ermöglicht, ohne einzelne Datensätze oder Modellparameter offenzulegen.                                                                                                                                                                                              |   3   |

---

## C4.2 KI-Hardware-Sicherheit

Sichere AI-spezifische Hardwarekomponenten einschließlich GPUs, TPUs und spezialisierter AI-Beschleuniger.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                 | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 4.2.1 | Verifizieren Sie, dass die Integrität des KI-Beschleunigers vor der Ausführung der Workload mithilfe von hardwarebasierten Attestierungsmechanismen (z. B. TPM, DRTM oder gleichwertig) validiert wird.                                                                                                      |   2   |
| 4.2.2 | Stellen Sie sicher, dass der Accelerator-(GPU)-Speicher zwischen Workloads durch Partitionierungsmechanismen isoliert ist, mit Speicherbereinigung zwischen Jobs.                                                                                                                                            |   2   |
| 4.2.3 | Verifizieren Sie, dass AI-Accelerator-Firmware beim Booten versionsgebunden, signiert und attestiert ist; nicht signierte oder Debug-Firmware wird blockiert.                                                                                                                                                |   2   |
| 4.2.4 | Verifizieren Sie, dass VRAM und On-Package-Speicher zwischen Jobs/Mandanten auf Null gesetzt werden und dass Richtlinien für Geräte-Resets eine Remanenz von Daten zwischen Mandanten verhindern.                                                                                                            |   2   |
| 4.2.5 | Stellen Sie sicher, dass Partitionierungs-/Isolierungsfunktionen (z.B. MIG/VM-Partitionierung) pro Mandant erzwungen werden und einen Peer-to-Peer-Speicherzugriff über Partitionen hinweg verhindern.                                                                                                       |   2   |
| 4.2.6 | Überprüfen, dass Hardware-Sicherheitsmodule (HSMs) oder gleichwertige manipulationssichere Hardware den Schutz von KI-Modellgewichten und kryptografischen Schlüsseln bereitstellen, mit Zertifizierung auf ein geeignetes Vertrauenswürdigkeitsniveau (z.B. FIPS 140-3 Level 3 oder Common Criteria EAL4+). |   3   |
| 4.2.7 | Überprüfen Sie, dass Beschleuniger-Verbindungen (NVLink/PCIe/InfiniBand/RDMA/NCCL) auf genehmigte Topologien und authentifizierte Endpunkte beschränkt sind; Klartext-Cross-Tenant-Verbindungen sind nicht zulässig.                                                                                         |   3   |
| 4.2.8 | Verifizieren Sie, dass Beschleuniger-Telemetriedaten (Leistungsaufnahme, Temperatur, Fehlerkorrektur, Leistungszähler) in die zentrale Sicherheitsüberwachung exportiert werden und dass Warnungen bei Anomalien ausgelöst werden, die auf Seitkanäle oder verdeckte Kanäle hindeuten.                       |   3   |

---

## C4.3 Edge- & Distributed-AI-Sicherheit

Sichere verteilte KI-Bereitstellungen einschließlich Edge-Computing, föderiertes Lernen und Multi-Site-Architekturen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 4.3.1 | Überprüfen Sie, dass Edge-AI-Geräte mithilfe einer gegenseitigen Authentifizierung mit Zertifikatsvalidierung (z. B. mutual TLS) bei der zentralen Infrastruktur authentifizieren.                                                                                                                                                                          |   1   |
| 4.3.2 | Stellen Sie sicher, dass Modelle, die auf Edge- oder mobilen Geräten bereitgestellt werden, während des Packens kryptografisch signiert werden, und dass die On-Device-Laufzeit diese Signaturen oder Prüfsummen vor dem Laden oder der Inferenz validiert; nicht verifizierte oder veränderte Modelle müssen abgelehnt werden.                             |   1   |
| 4.3.3 | Überprüfen Sie, dass verteilte KI-Koordination byzantinertolerante Konsensmechanismen mit Validierung der Teilnehmer und Erkennung bösartiger Knoten verwendet.                                                                                                                                                                                             |   3   |
| 4.3.4 | Stellen Sie sicher, dass On-Device-Inferenz-Laufzeiten die Isolierung von Prozessen, Speicher und Dateizugriff durchsetzen, um zu verhindern, dass Modelle gedumpt, Debugging betrieben oder extrahiert werden, einschließlich der Zwischeneinbettungen und -aktivierungen.                                                                                 |   3   |
| 4.3.5 | Verifizieren Sie, dass Modellgewichte und sensible Parameter, die lokal gespeichert sind, mithilfe hardwaregestützter Key Stores oder sicherer Enklaven (z.B. Android Keystore, iOS Secure Enclave, TPM/TEE) verschlüsselt sind, wobei die Schlüssel für den User Space nicht zugänglich sind.                                                              |   3   |
| 4.3.6 | Verifizieren Sie, dass Modelle, die in mobilen, IoT- oder eingebetteten Anwendungen verpackt sind, im Ruhezustand verschlüsselt oder verschleiert sind und nur innerhalb einer vertrauenswürdigen Laufzeitumgebung oder eines sicheren Enclave entschlüsselt werden, sodass eine direkte Extraktion aus dem App-Paket oder dem Dateisystem verhindert wird. |   3   |

---

## References

* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
* [NVIDIA Multi-Instance GPU (MIG) Documentation](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/)
* [Confidential Computing Consortium](https://confidentialcomputing.io/)
* [ARM TrustZone for AI](https://www.arm.com/technologies/trustzone-for-cortex-a)

