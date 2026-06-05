# C4 Infrastruktur-, Konfigurations- & Bereitstellungssicherheit

## Kontrollziel

KI-spezifische Infrastrukturkomponenten müssen gegen Modellklau, Datenausleitung und Kontamination zwischen Mandanten abgesichert werden. Dieses Kapitel behandelt KI-Workload-Sandboxing, die Systemsicherheit von KI-Beschleunigerhardware und die Sicherheit von Edge-/verteilten KI-Bereitstellungen.

---

## C4.1 AI-Workload-Sandboxing & Validierung

Isolieren Sie nicht vertrauenswürdige KI-Modelle in sicheren Sandboxes und schützen Sie sensible KI-Workloads mithilfe vertrauenswürdiger Ausführungsumgebungen (Trusted Execution Environments, TEEs) und Technologien für vertrauliches Computing. Informationen zur Sandbox-Umgebungsausführung von Tools und Plugins innerhalb agentischer Workflows finden Sie in C9.3.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                 | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 4.1.1 | Überprüfen Sie, dass externe oder nicht vertrauenswürdige KI-Modelle in isolierten Sandboxes ausgeführt werden.                                                                                                                                                                                                                                              |   1   |
| 4.1.2 | Überprüfen Sie, dass sandboxed workloads standardmäßig keine ausgehende Netzwerkverbindung haben, wobei jeglicher erforderlicher Zugriff explizit definiert sein muss.                                                                                                                                                                                       |   1   |
| 4.1.3 | Verifizieren Sie, dass das Laden von Modellartefakten eine explizite Positivliste von Serialisierungsformaten erzwingt, die keine willkürliche Codeausführung während der Deserialisierung zulassen, und dass Formate, die eine willkürliche Codeausführung ermöglichen (z. B. Python pickle mit uneingeschränkten Globals), standardmäßig abgelehnt werden. |   1   |
| 4.1.4 | Stellen Sie sicher, dass die Workload-Atestierung vor dem Laden des Modells durchgeführt wird und dass ein kryptografischer Nachweis vorliegt, dass die Ausführungsumgebung nicht manipuliert wurde.                                                                                                                                                         |   2   |
| 4.1.5 | Verifizieren Sie, dass vertrauliche Workloads innerhalb einer Trusted Execution Environment (TEE) ausgeführt werden, die hardwaregestützte Isolation, Speicherverschlüsselung und Integritätsschutz bereitstellt.                                                                                                                                            |   3   |
| 4.1.6 | Überprüfen Sie, dass vertrauliche Inferenzdienste die Modellextraktion durch verschlüsselte Berechnungen mit versiegelten Modellgewichten und geschützter Ausführung verhindern.                                                                                                                                                                             |   3   |
| 4.1.7 | Überprüfen Sie, dass Secure Multi-Party Computation (SMPC) ein kollaboratives KI-Training ermöglicht, ohne einzelne Datensätze oder Modellparameter offenzulegen.                                                                                                                                                                                            |   3   |

---

## C4.2 KI-Hardware-Sicherheit

Sichere KI-spezifische Hardware-Komponenten einschließlich GPUs, TPUs und spezialisierter KI-Beschleuniger.

|   #   | Beschreibung                                                                                                                                                                                                                                                                               | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 4.2.1 | Verifizieren Sie, dass vor der Workload-Ausführung die Integrität des AI-Accelerators mithilfe von hardwarebasierten Attestierungsmechanismen (z. B. TPM, DRTM oder einem Äquivalent) validiert wird.                                                                                      |   2   |
| 4.2.2 | Überprüfen Sie, dass der Speicher der Beschleuniger (GPU) mithilfe von Partitionierungsmechanismen zwischen Workloads isoliert ist, mit Speicherbereinigung zwischen Jobs.                                                                                                                 |   2   |
| 4.2.3 | Verifizieren Sie, dass die Firmware der KI-Beschleuniger versionsgebunden, signiert und beim Bootvorgang attestiert ist; nicht signierte oder Debug-Firmware wird blockiert.                                                                                                               |   2   |
| 4.2.4 | Stellen Sie sicher, dass VRAM und On-Package-Speicher zwischen Jobs/Mandanten auf Null gesetzt werden und dass Geräte-Reset-Richtlinien eine datenbezogene Remanenz zwischen Mandanten verhindern.                                                                                         |   2   |
| 4.2.5 | Verifizieren Sie, dass die Partitionierungs-/Isolierungsfunktionen (z.B. MIG/VM-Partitionierung) pro Mandant erzwungen werden und den Peer-to-Peer-Zugriff auf Arbeitsspeicher zwischen Partitionen verhindern.                                                                            |   2   |
| 4.2.6 | Überprüfen Sie, dass Hardware-Sicherheitsmodule (HSMs) oder entsprechende manipulationssichere Hardware den KI-Modell-Weights und kryptografischen Schlüsseln Schutz bieten, mit Zertifizierung auf ein geeignetes Sicherheitsniveau (z.B. FIPS 140-3 Level 3 oder Common Criteria EAL4+). |   3   |
| 4.2.7 | Stellen Sie sicher, dass Accelerator-Interconnects (NVLink/PCIe/InfiniBand/RDMA/NCCL) auf genehmigte Topologien und authentifizierte Endpunkte beschränkt sind; Klartext-Cross-Tenant-Links sind nicht zulässig.                                                                           |   3   |
| 4.2.8 | Stellen Sie sicher, dass die Beschleuniger-Telemetrie (Leistungsaufnahme, Temperatur, Fehlerkorrektur, Leistungszähler) in die zentrale Sicherheitsüberwachung exportiert wird und bei Anomalien, die auf Side-Channels oder verdeckte Kanäle hindeuten, Warnungen ausgelöst werden.       |   3   |

---

## C4.3 Edge- & Distributed-AI-Sicherheit

Sichere verteilte KI-Bereitstellungen einschließlich Edge-Computing, föderiertem Lernen und Multi-Site-Architekturen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                         | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 4.3.1 | Verifizieren Sie, dass Edge-AI-Geräte sich mithilfe einer gegenseitigen Authentifizierung mit Zertifikatsvalidierung (z.B. gegenseitiges TLS) gegenüber der zentralen Infrastruktur authentifizieren.                                                                                                                                                                |   1   |
| 4.3.2 | Stellen Sie sicher, dass Modelle, die auf Edge- oder mobilen Geräten bereitgestellt werden, während des Packens kryptografisch signiert werden, und dass die On-Device-Laufzeit diese Signaturen oder Prüfsummen vor dem Laden oder der Inferenz validiert; nicht verifizierte oder veränderte Modelle müssen abgelehnt werden.                                      |   1   |
| 4.3.3 | Überprüfen Sie, dass verteilte KI-Koordination byzantiner fehlertolerante Konsensmechanismen mit Teilnehmervalidierung und Erkennung bösartiger Knoten verwendet.                                                                                                                                                                                                    |   3   |
| 4.3.4 | Überprüfen Sie, dass On-Device-Inferenz-Laufzeitumgebungen die Isolation von Prozessen, Speicher und Dateizugriff erzwingen, um Modell-Dumping, Debugging oder die Extraktion von Zwischen-Embeddings und Aktivierungen zu verhindern.                                                                                                                               |   3   |
| 4.3.5 | Überprüfen Sie, dass Modellgewichte und lokal gespeicherte sensible Parameter so verschlüsselt sind, dass sie mithilfe von hardwaregestützten Key Stores oder Secure Enclaves (z. B. Android Keystore, iOS Secure Enclave, TPM/TEE) geschützt werden, wobei die Schlüssel für den User-Space nicht zugänglich sind.                                                  |   3   |
| 4.3.6 | Stellen Sie sicher, dass Modelle, die in mobilen, IoT- oder eingebetteten Anwendungen verpackt sind, im Ruhezustand verschlüsselt oder verschleiert sind und nur innerhalb einer vertrauenswürdigen Laufzeitumgebung oder einer sicheren Enklave entschlüsselt werden, sodass eine direkte Extraktion aus dem Anwendungs-Paket oder dem Dateisystem verhindert wird. |   3   |

---

## Referenzen

* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
* [NVIDIA Multi-Instance GPU (MIG) Documentation](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/)
* [Confidential Computing Consortium](https://confidentialcomputing.io/)
* [ARM TrustZone for AI](https://www.arm.com/technologies/trustzone-for-cortex-a)

