# Anhang B: Strategische Kontrollen

## C4.15 Quantenresistente Infrastruktur-Sicherheit

Bereiten Sie die KI-Infrastruktur auf Bedrohungen durch Quantencomputing durch post-quantum Kryptographie und quantensichere Protokolle vor.

|   #    | Beschreibung                                                                                                                                                                                                      | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.15.1 | Überprüfen Sie, ob die KI-Infrastruktur NIST-zugelassene postquantum-kryptografische Algorithmen (CRYSTALS-Kyber, CRYSTALS-Dilithium, SPHINCS+) für den Schlüsselaustausch und digitale Signaturen implementiert. |   3   |  D/V  |
| 4.15.2 | Verifizieren Sie, dass Quantenschlüsselverteilungssysteme (QKD) für hochsichere KI-Kommunikation mit quantensicheren Schlüsselverwaltungsprotokollen implementiert sind.                                          |   3   |  D/V  |
| 4.15.3 | Überprüfen Sie, ob kryptografische Agilitätsframeworks eine schnelle Migration zu neuen post-quanten Algorithmen mit automatisierter Zertifikats- und Schlüsselrotation ermöglichen.                              |   3   |  D/V  |
| 4.15.4 | Stellen Sie sicher, dass das Quantum Threat Modeling die Verwundbarkeit der KI-Infrastruktur gegenüber Quantenangriffen bewertet und dokumentierte Migrationszeitpläne sowie Risikoanalysen enthält.              |   3   |   V   |
| 4.15.5 | Stellen Sie sicher, dass hybride klassische-quantum kryptografische Systeme während der Quantenübergangsphase durch mehrschichtige Sicherheitsmaßnahmen mit Leistungsüberwachung Schutz bieten.                   |   3   |  D/V  |

---

## C4.17 Zero-Knowledge-Infrastruktur

Implementieren Sie Zero-Knowledge-Beweissysteme für eine datenschutzfreundliche KI-Verifizierung und Authentifizierung, ohne sensible Informationen preiszugeben.

|   #    | Beschreibung                                                                                                                                                                                       | Ebene | Rolle |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.17.1 | Bestätigen Sie, dass Zero-Knowledge-Beweise (ZK-SNARKs) die Integrität des KI-Modells und den Ursprung des Trainings verifizieren, ohne Modellgewichte oder Trainingsdaten offenzulegen.           |   3   |  D/V  |
| 4.17.2 | Überprüfen Sie, dass auf ZK basierende Authentifizierungssysteme eine datenschutzfreundliche Benutzerverifizierung für KI-Dienste ermöglichen, ohne identitätsbezogene Informationen preiszugeben. |   3   |  D/V  |
| 4.17.3 | Überprüfen Sie, dass Private Set Intersection (PSI)-Protokolle eine sichere Datenabstimmung für föderiertes KI ermöglichen, ohne einzelne Datensätze offenzulegen.                                 |   3   |  D/V  |
| 4.17.4 | Überprüfen Sie, dass Zero-Knowledge-Maschinelles Lernen (ZKML)-Systeme verifizierbare KI-Schlussfolgerungen mit kryptografischem Nachweis der korrekten Berechnung ermöglichen.                    |   3   |  D/V  |
| 4.17.5 | Überprüfen Sie, dass ZK-Rollups skalierbare, datenschutzbewahrende KI-Transaktionsverarbeitung mit Stapelverifizierung und reduziertem Rechenaufwand bieten.                                       |   3   |  D/V  |

---

## C4.18 Verhinderung von Seitenkanalangriffen

Schützen Sie die KI-Infrastruktur vor Timing-, Energie-, elektromagnetischen und cache-basierten Side-Channel-Angriffen, die vertrauliche Informationen preisgeben könnten.

|   #    | Beschreibung                                                                                                                                                                               | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 4.18.1 | Stellen Sie sicher, dass die KI-Inferenzzeit durch Verwendung von Algorithmen mit konstanter Zeit und Padding normalisiert wird, um zeitbasierte Modell-Extraktionsangriffe zu verhindern. |   3   |  D/V  |
| 4.18.2 | Stellen Sie sicher, dass der Schutz vor Leistungsanalyse die Rauschinjektion, die Filterung der Stromleitung und die randomisierten Ausführungsmuster für KI-Hardware umfasst.             |   3   |  D/V  |
| 4.18.3 | Stellen Sie sicher, dass die Side-Channel-Abmilderung auf Basis des Caches Cache-Partitionierung, Randomisierung und Flush-Anweisungen verwendet, um Informationslecks zu verhindern.      |   3   |  D/V  |
| 4.18.4 | Stellen Sie sicher, dass der Schutz vor elektromagnetischer Abstrahlung Abschirmung, Signalfilterung und randomisierte Verarbeitung umfasst, um TEMPEST-ähnliche Angriffe zu verhindern.   |   3   |  D/V  |
| 4.18.5 | Überprüfen Sie, ob mikroarchitektonische Seitenkanalabwehrmaßnahmen spekulative Ausführungssteuerungen und die Verschleierung von Speicherzugriffsmustern umfassen.                        |   3   |  D/V  |

---

## C4.19 Neuromorphe & Spezialisierte KI-Hardware-Sicherheit

Sichern Sie aufkommende KI-Hardwarearchitekturen, einschließlich neuromorpher Chips, FPGAs, kundenspezifischer ASICs und optischer Rechensysteme.

|   #    | Beschreibung                                                                                                                                                                                        | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.19.1 | Verifizieren Sie, dass die Sicherheit neuromorpher Chips die Verschlüsselung von Spike-Mustern, den Schutz synaptischer Gewichte und die hardwarebasierte Validierung von Lernregeln umfasst.       |   3   |  D/V  |
| 4.19.2 | Stellen Sie sicher, dass FPGA-basierte KI-Beschleuniger Bitstream-Verschlüsselung, Anti-Manipulationsmechanismen und sicheres Konfigurationsladen mit authentifizierten Updates implementieren.     |   3   |  D/V  |
| 4.19.3 | Verifizieren Sie, dass die benutzerdefinierte ASIC-Sicherheit On-Chip-Sicherheitsprozessoren, eine Hardware-Root-of-Trust und einen sicheren Schlüssel-Speicher mit Manipulationserkennung umfasst. |   3   |  D/V  |
| 4.19.4 | Überprüfen Sie, ob optische Computersysteme quantensichere optische Verschlüsselung, sichere photonische Schaltung und geschützte optische Signalverarbeitung implementieren.                       |   3   |  D/V  |
| 4.19.5 | Überprüfen Sie, ob hybride analog-digitale KI-Chips sichere analoge Berechnungen, geschützte Gewichtsspeicherung und authentifizierte Analog-Digital-Wandlung enthalten.                            |   3   |  D/V  |

---

## C4.20 Datenschutzbewahrende Recheninfrastruktur

Implementieren Sie Infrastruktursicherungen für datenschutzfreundliche Berechnungen, um sensible Daten während der KI-Verarbeitung und -Analyse zu schützen.

|   #    | Beschreibung                                                                                                                                                                                                                | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 4.20.1 | Überprüfen Sie, dass die homomorphe Verschlüsselungsinfrastruktur verschlüsselte Berechnungen auf sensiblen KI-Arbeitslasten mit kryptografischer Integritätsprüfung und Leistungsüberwachung ermöglicht.                   |   3   |  D/V  |
| 4.20.2 | Überprüfen Sie, dass Systeme für private Informationsabfrage Datenbankabfragen ermöglichen, ohne Abfragemuster unter kryptografischem Schutz der Zugriffsmuster offenzulegen.                                               |   3   |  D/V  |
| 4.20.3 | Überprüfen Sie, dass sichere Mehrparteienberechnungsprotokolle datenschutzfreundliche KI-Inferenz ermöglichen, ohne einzelne Eingaben oder Zwischenberechnungen offenzulegen.                                               |   3   |  D/V  |
| 4.20.4 | Stellen Sie sicher, dass der datenschutzfreundliche Schlüsselmanagementprozess verteilte Schlüsselerzeugung, Schwellenwert-Kryptographie und sichere Schlüsselrotation mit hardwaregestütztem Schutz umfasst.               |   3   |  D/V  |
| 4.20.5 | Verifizieren Sie, dass die Leistung der datenschutzwahrenden Berechnung durch Bündelung, Zwischenspeicherung und Hardwarebeschleunigung optimiert wird, während die kryptografischen Sicherheitsgarantien erhalten bleiben. |   3   |  D/V  |

| 4.9.1 | Überprüfen Sie, ob alle Cloud-Umgebungen in zentrale Identitätssysteme integriert sind, um eine konsistente Authentifizierung zu gewährleisten. | 1 | D/V |
| 4.9.2 | Überprüfen Sie, ob Multi-Cloud-Bereitstellungen föderierte Identitätsstandards (z. B. OIDC, SAML) mit zentraler Richtliniendurchsetzung über Anbieter hinweg verwenden. | 2 | D/V |
| 4.9.3 | Überprüfen Sie, ob Cloud-übergreifende und hybride Datenübertragungen End-to-End-Verschlüsselung mit vom Kunden verwalteten Schlüsseln verwenden und die territorialen Anforderungen an den Datenstandort durchgesetzt werden. | 2 | D/V |
| 4.9.1 | Überprüfen Sie, ob die Integration der Cloud-Speicherung eine Ende-zu-Ende-Verschlüsselung mit von Agenten gesteuertem Schlüsselmanagement verwendet. | 1 | D/V |
| 4.9.2 | Überprüfen Sie, ob die Grenzen der hybriden Bereitstellungssicherheit klar definiert sind und verschlüsselte Kommunikationskanäle verwendet werden. | 2 | D/V |

