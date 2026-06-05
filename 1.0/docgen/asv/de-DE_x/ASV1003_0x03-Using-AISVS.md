# Mithilfe der AISVS

Der Artificial Intelligence Security Verification Standard (AISVS) definiert Sicherheitsanforderungen für moderne KI-Anwendungen und -Dienste und konzentriert sich dabei auf Aspekte, die in der Kontrolle der Anwendungsentwickler liegen.

Das AISVS ist für alle vorgesehen, die die Sicherheit von KI-Anwendungen entwickeln oder bewerten, einschließlich Entwicklern, Architekten, Security Engineers und Auditoren. Dieses Kapitel stellt die Struktur und die Verwendung des AISVS vor, einschließlich seiner Verifizierungsstufen, vorgesehenen Anwendungsfälle und der Einordnung neben anderen Sicherheitsstandards.

## Sicherheitsüberprüfungsstufen für Künstliche Intelligenz

Die AISVS definiert drei aufsteigende Sicherheitsprüfungsstufen. Jede Stufe ergänzt Tiefe und Komplexität und ermöglicht es Organisationen, ihre Sicherheitsstrategie an die Risikostufe ihrer KI-Systeme anzupassen.

Organisationen können bei Level 1 beginnen und zunehmend höhere Level übernehmen, wenn die Sicherheitsreife und die Bedrohungsexposition zunehmen. AISVS-Level sind mit [ASVS](https://owasp.org/www-project-application-security-verification-standard/)Levels und sind dafür vorgesehen, auf der entsprechenden ASVS-Ebene angewendet zu werden (siehe[Alignment with ASVS Levels](#alignment-with-asvs-levels)).

### Definition der Ebenen

Jede Anforderung in AISVS v1.0 wird einer der folgenden Stufen zugewiesen:

#### Level 1-Anforderungen

Level 1 umfasst die kritischsten und grundlegenden Sicherheitsanforderungen. Diese zielen darauf ab, gängige Angriffe zu verhindern, die keine anderen Voraussetzungen oder Schwachstellen ausnutzen. Die meisten Level-1-Kontrollen sind entweder relativ einfach umzusetzen oder hinreichend wesentlich, um den Aufwand zu rechtfertigen.

#### Level 2-Anforderungen

Ebene 2 bezieht sich auf fortgeschrittenere oder weniger häufige Angriffe sowie auf geschichtete Abwehrmaßnahmen gegen weit verbreitete Bedrohungen. Diese Anforderungen können eine komplexere Logik beinhalten oder spezifische Angriffsvoraussetzungen adressieren.

#### Anforderungen der Stufe 3

Ebene 3 umfasst Kontrollen, die typischerweise schwieriger umzusetzen oder in ihrer Anwendbarkeit situationsabhängig sind. Diese stellen oft Mechanismen zur Verteidigung in der Tiefe oder Gegenmaßnahmen gegen Nischen-, gezielte oder hochkomplexe Angriffe dar.

## Geltungsbereich der AISVS

AISVS ist bewusst eng gefasst. Es definiert nur Sicherheitsanforderungen, die spezifisch für KI- und ML-Systeme sind, oder bei denen allgemeine Sicherheitskontrollen KI-spezifische Nuancen aufweisen, die ein erneutes Aufgreifen rechtfertigen. Es ist kein eigenständiges Sicherheitsprogramm für eine KI-Anwendung. AISVS geht davon aus, dass die zugrunde liegende Anwendung, die Infrastruktur und die organisatorischen Praktiken bereits anhand etablierter allgemeingültiger Standards verifiziert wurden, und ergänzt darauf eine KI-spezifische Schicht.

Die folgenden Punkte sind absichtlich nicht im Geltungsbereich und werden nicht in AISVS-Kapiteln dupliziert:

* Allgemeine Anwendungssicherheit. Authentifizierung, Sitzungsverwaltung, Autorisierung, Sicherheit der Übertragung, Eingabe- und Ausgabehandhabung für Nicht-AI-Oberflächen, Geheimnisverwaltung, Handhabung von Datei-Uploads, Fehlerbehandlung und ähnliche Kontrollen werden durch das [OWASP Application Security Verification Standard (ASVS)](https://owasp.org/www-project-application-security-verification-standard/).
* Allgemeine Software- Supply-Chain- Sicherheit. Abhängigkeits- Scanning, Version- Pinning, Lockfile- Erzwingung, Build- Provenance, reproduzierbare Builds, generische SBOM- Generierung sowie Integrität von CI/CD- Pipelines werden durch die [OWASP Software Component Verification Standard (SCVS)](https://owasp.org/www-project-software-component-verification-standard/), [SLSA](https://slsa.dev/), und die [CIS Controls](https://www.cisecurity.org/controls).
* Allgemeine Infrastruktur- und Plattformhärtung. Container-, Host-, Netzwerk-, Cloud- und Kubernetes-Basis-Härtungen werden durch die [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks), [NIST SP 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), [NIST SP 800-190](https://csrc.nist.gov/pubs/sp/800/190/final), und die [NIST Cybersecurity Framework (CSF)](https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20).
* Allgemeine Datenschutz- und Datenschutzschutzvorgänge. Datenklassifizierung, Verschlüsselung bei Speicherung und Übertragung, Aufbewahrungsplanungen, sichere Löschung von herkömmlichem Speicher, Unveränderbarkeit von Audit-Logs sowie der Betrieb einer Consent-Management-Plattform werden durch ASVS definiert,[ISO/IEC 27001](https://www.iso.org/standard/27001), und geltende Datenschutzvorschriften wie die DSGVO.
* Allgemeines Protokollieren und Monitoring. Der Zugriffsschutz, die Aufbewahrungsdauer, Backups, die Verschlüsselung, die Anonymisierung, der manipulationssichere Schutz, die SIEM-Integration und die operative Telemetrie für den Zugriff auf Protokollspeicher werden durch ASVS und bewährte Standardpraktiken der Observability definiert.
* KI-Governance und Risikomanagement. Die organisatorische KI-Governance, KI-Auswirkungsanalysen, Dokumentation zu Fairness und Ethik, Model Cards, öffentliche Transparenzberichte sowie die Gestaltung von Risikomanagement-Prozessen werden festgelegt durch [ISO/IEC 42001](https://www.iso.org/standard/81230.html), [ISO/IEC 23894](https://www.iso.org/standard/77304.html), und die [NIST AI RMF](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10).

Beim Abgleich einer KI-Anwendung mit AISVS sollte parallel das entsprechende Reifegrad-/Level-Niveau dieser zugrunde liegenden Standards überprüft werden. AISVS allein ist kein Ersatz für und geht nicht in irgendeinem von ihnen auf.

## Ausrichtung an ASVS-Ebenen

Die AISVS-Levels sind auf [ASVS](https://owasp.org/www-project-application-security-verification-standard/)Stufen. Überprüfen einer KI-Anwendung anhand des AISVS Level_N_setzt außerdem voraus, dass die Anwendung ebenfalls gegen ASVS Level verifiziert wurde oder wird_N_. Die beiden Standards sind so konzipiert, dass sie gemeinsam auf den entsprechenden Ebenen angewendet werden:

| AISVS Level | Entsprechende ASVS-Ebene | Typische Verwendung                                                                                                                                             |
| :---------: | :----------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|      1      |            1             | Basis-Sicherheit für jede KI-Anwendung, die mit nicht vertrauenswürdigen Eingaben umgeht oder mit Daten beliebiger Sensitivität arbeitet.                       |
|      2      |            2             | KI-Anwendungen, die mit sensiblen Geschäftsdaten, regulierten Daten umgehen oder in adversarialen Kontexten betrieben werden.                                   |
|      3      |            3             | Hochzuverlässige KI-Anwendungen wie solche, die lebenswichtige Entscheidungen, kritische Infrastrukturen oder sehr sensible personenbezogene Daten verarbeiten. |

Wenn eine AISVS-Anforderung eine Überschneidung mit einer ASVS-Anforderung zu haben scheint, wird die AISVS-Version nur dann neu formuliert, wenn sie KI-spezifische Implementierungsdetails, Angriffsfläche oder Nachweise enthält, die ein Auditor anders bewerten muss. In allen anderen Fällen gilt die ASVS-Anforderung, und AISVS wiederholt sie nicht.

## Querverweise innerhalb von AISVS

AISVS-Kapitel sind nach Kontrollfamilien organisiert, nicht nach Angriffen oder Komponenten. Infolgedessen erfordert das Verteidigen gegen eine bestimmte KI-Bedrohung in der Regel, Anforderungen aus mehreren Kapiteln zusammen anzuwenden. Beispielsweise kombiniert das Verteidigen gegen Prompt Injection in einer agentischen Anwendung Anforderungen aus C2 (Eingabevalidierung), C7 (Ausgabekontrollen), C9 (Freigabe von Agentenaktionen), C10 (MCP-spezifische Kontrollen), C11 (adversariale Robustheit), C13 (Erkennung und Protokollierung) sowie C14 (menschliche Genehmigung für risikoreiche Aktionen).

Einzelne Kapitel und Abschnitte führen nicht auf, welche anderen AISVS-Kapitel verwandte Anliegen abdecken. Bei der Anwendung von AISVS ist der Standard als Ganzes zu behandeln und Appendix D (AI Security Controls Inventory) zu konsultieren, um einen bereichsübergreifenden Überblick darüber zu erhalten, wo jede Abwehrtechnik auftritt.


