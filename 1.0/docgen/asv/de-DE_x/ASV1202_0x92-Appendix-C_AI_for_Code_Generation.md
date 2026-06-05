# Anhang C: KI-gestütztes Secure Coding

<!-- markdownlint-disable-next-line MD013 -->
<!-- cspell:words SSDF SAMM CICD PBAC Pulumi Conftest tfsec KICS Allstar unreviewed weaponization stylometric -->

## Ziel

Dieser Anhang listet organisatorische Kontrollen für die sichere Nutzung von KI-Entwicklungstools auf. Der Umfang reicht von Baseline bis fortgeschritten. Der Geltungsbereich umfasst das Codieren, Code-Review und den Rest der SSDLC.

Behandle den KI-Coding-Agenten als Akteur in der Lieferkette, nicht als passiven Helfer. Er hat eine Identität, Autorität und die Fähigkeit, in eigenem Namen zu handeln oder von einem Angreifer in die Lage versetzt zu werden, mit ihm zu handeln.

Zwei Dinge ergeben sich aus dieser Rahmung.

Ihr eigener Agent kann gegen Sie eingesetzt werden. Ein Code-Review-Bot, der eine bösartige PR-Beschreibung liest, kann durch Prompt-Injection dazu gebracht werden, denselben Code zu genehmigen, den er eigentlich ablehnen sollte. Die Injection muss nicht besonders subtil sein. Sie muss lediglich den Kontext-Window des Bots erreichen.

Angreifer betreiben ihre eigene KI, oft in großem Maßstab. Vertraute Muster sind automatisierte Fork-and-Pull-Request-Kampagnen, die darauf abzielen auf`pull_request_target`- Klassen löst, KI-generierte Payloads, die auf ein bestimmtes Ziel-Repository zugeschnitten sind, und Missbrauch langfristiger CI-Geheimnisse, die dabei abgegriffen wurden.

Der Anhang ist mit NIST SSDF (SP 800-218 und SP 800-218A), NIST SP 800-204D, NIST AI RMF (AI 100-1), dem NIST Generative AI Profile (AI 600-1), NIST SP 800-207 Zero Trust Architecture, SLSA v1.2 (Build- und Source-Tracks), OWASP ASVS v5, den OWASP Top 10 CI/CD Security Risks, den OWASP Top 10 for Large Language Model Applications (2025), den OWASP Top 10 for Agentic Applications (2026, ASI01-ASI10), ISO/IEC 42001:2023 sowie MITRE ATLAS und ATT&CK abgestimmt.

>Geltungsbereichshinweis: Nur die AI-spezifische Delta-Änderung ist hier im Geltungsbereich. Die generische CI/CD-Pipeline-Sicherheitsabsicherung (Branch-Schutz, signierte Commits, Runner-Härtung, Secret-Scanning, Dependency-Pinning) ist bereits durch OWASP ASVS v5, die OWASP Top 10 CI/CD Security Risks, NIST SP 800-204D und SLSA v1.2 abgedeckt. Diese Baselines müssen bereits vorhanden sein. Die Verweise darauf in diesem Anhang dienen als Erinnerung. Die AI-Ergänzung darf sie nicht abschwächen. Und die AI-spezifischen Bedrohungsklassen (Ausnutzung von Fork-PR-Triggern, Prompt Injection, Angreifer, die ihrerseits eigene AI ausführen) müssen ebenfalls adressiert werden.
> 
>Beziehung zu normativen Kapiteln: Mehrere Kontrollen in diesem Anhang sind in der Tat Anwendungen einer AISVS-Kontrolle aus einem Kapitel auf den Fall der sicheren Programmierung. Die Kapitel, die am häufigsten herangezogen werden, sind C2.1 (Prompt Input Validation), C9.3 (Tool Sandboxing) und C9.6 (Action Authorization). Die zugehörige FAMILIE-Einführung weist darauf hin, sofern dies zutrifft. Für Gutachter: Zählen Sie eine Feststellung aus Anhang C entweder als eine zusätzliche Lücke, die die vorgelagerte Kapitelprüfung nicht geschlossen hat, oder als bereits unter dem Kapitel gezählt. Nicht als beides.

---

### Architekturvoraussetzungen

Bevor Sie mit der Überprüfung gegen Anhang C beginnen, muss die Hosting-Umgebung diese Basisanforderungen erfüllen:

* OWASP ASVS v5-Konformität. Dieses Anhängelement ergänzt die ASVS v5-Anforderungen an die Codierungsqualität und die CI/CD-Bereitstellungssicherheit (V10 über allem). Es ersetzt diese nicht. Die ASVS v5-Abdeckung der CI/CD-Pipelinesicherheit muss vorhanden sein, bevor Anhang C verifiziert wird. Das Gleiche gilt für die Abdeckung der OWASP Top 10 CI/CD Security Risks.
* SLSA-Implementierung. SLSA Build Track Level 2 oder höher auf den zentralen Integrations- und Bereitstellungslinien, mit erzeugter und verifizierter Herkunft (Provenance) für Release-Artefakte. Wenn Produktions-AI-Agenten auf Quell-Repositorys agieren, übernehmen Sie zusätzlich den SLSA Source Track (v1.2) für Urheberschafts- und Überprüfungs-Kontrollen.
* Plattform-Control- Invarianten. Branch-Schutz- oder Regelnetz-Einschränkungen auf den Release-Pfaden. Mindestens: keine nicht überprüften Merges in die Default- oder Release-Branches, signierte Commits, sofern die Plattform dies unterstützt, erforderliche Statuschecks, geschützte Umgebungen und eine nachvollziehbare Dokumentation für jede menschliche Ausnahme.

---

## AC.1 KI-unterstützter sicherer Code-Workflow

KI-Tools müssen sich in die bestehende SSDLC einfügen, ohne irgendeines der bereits vorhandenen Sicherheits-„Gates“ zu schwächen. Genauso wichtig: Schreiben Sie die Adversarial-AI-Threat-Szenarien auf, die jede Schutzmaßnahme begründen. Das ist viel einfacher, wenn man es gleich zu Beginn macht, statt es danach mühsam zu rekonstruieren.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                       | Ebene |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.1.1 | Stellen Sie sicher, dass der schriftlich festgelegte Workflow angibt, wann KI-Tools Code generieren, refaktorisieren oder überprüfen dürfen. Der Workflow nennt die genehmigten Tools, die verbotenen Anwendungsfälle sowie die Datenklassifizierungen, die als Eingabe zulässig sind.                                                                                                             | 1     |
| AC.1.2 | Prüfen Sie, dass der Workflow jede Phase des SSDLC abdeckt, von Design und Implementierung über Code Review, Tests, Deployment und die Überwachung nach dem Deployment, und dass die Security Gates benannt werden, die unabhängig davon, ob AI beteiligt war oder nicht, weiterhin verpflichtend bleiben.                                                                                         | 2     |
| AC.1.3 | Verifizieren Sie, dass die Workflow-Namen die adversarial-AI Threat-Szenarien benennen, die sie abzumildern beabsichtigt. Die Liste sollte Prompt-Injection-Szenarien abdecken, die über PR-Inhalte bereitgestellt werden, KI-generierte Supply-Chain-Payloads, autonome Agents, die ihre eigene Arbeit genehmigen, Fork-PR-Secret-Exfiltration und eine Kompromittierung der Modell-Supply-Chain. | 2     |
| AC.1.4 | Verifizieren Sie, dass Kennzahlen für durch KI erzeugten und durch KI vermittelten Code erfasst werden und dass die Ergebnisse gegen eine Human-only-Basislinie verglichen werden. Die Verwundbarkeitsdichte, die mittlere Zeit bis zur Erkennung, die KI-zurechenbare Defektrate, die Prompt-Injection-Erkennungsrate und die Fork-PR-Ablehnungsrate sind allesamt nützlich.                      | 3     |

Zuordnungen & Verweise:

* AC.1.1: NIST SSDF PO.1 (Sicherheitsanforderungen für die Softwareentwicklung definieren); ISO/IEC 42001 Abschnitte 6, 8; OWASP SAMM-Strategie & -Metriken (SM), Strategie & Compliance (PC).
* AC.1.2: NIST SSDF PW.1, PW.7; OWASP SAMM Education & Guidance (EG); ISO/IEC 5338 Abschnitt 6.
* AC.1.3: MITRE ATLAS (Reconnaissance & Initial Access Taktiken); NIST AI 600-1 GOVERN; OWASP LLM Top 10 (2025) LLM03; OWASP Agentic Top 10 (2026) ASI04.
* AC.1.4: NIST AI RMF MEASURE; ISO/IEC 42001 Abschnitt 9; OWASP SAMM-Strategie & Kennzahlen (SM).

---

## AC.2 Qualifizierung von KI-Tools & Threat Modeling

Nehmen Sie kein KI-Tool zum Programmieren an, bis es bewertet wurde. Drei Bereiche im Besonderen: seine Sicherheitsfunktionen, seine Widerstandsfähigkeit gegen adversarialen Input und das Risiko, das von seiner Lieferkette übernommen wird.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Ebene |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----- |
| AC.2.1 | Verifizieren Sie, dass jedes KI-Tool, unabhängig davon, ob es sich um einen Assistenten, einen Prüfer, einen Agenten oder einen MCP-Server handelt, über ein Bedrohungsmodell verfügt. Das Bedrohungsmodell deckt Fehlverwendung, Modellinversion, das Offenlegen von Trainingsdaten, Prompt-Injection aus nicht vertrauenswürdigen Eingaben, unsichere Verarbeitung der Ausgaben, übermäßige Handlungsautonomie sowie Risiken ab, die aus der Abhängigkeitskette übernommen werden. | 1     |
| AC.2.2 | Stellen Sie sicher, dass die Bewertung jedes Tools die lokalen Komponenten (statische und dynamische Analyse), die SaaS-Endpunkte (TLS, AuthN/AuthZ, Protokollierung, Datenresidenz) und die Lieferkette des Modells des Anbieters (Herkunft der Trainingsdaten, Fine-Tune-Historie, RAG-Quellen) abdeckt. Jede dieser Komponenten wird überprüft und die Überprüfung wird dokumentiert.                                                                                             | 2     |
| AC.2.3 | Verifizieren Sie, dass jedes Tool vor der Onboarding-Freigabe einem Test auf adversariale Robustheit unterzogen wird. Die Tests werden nach jeder wesentlichen Änderung am Modell oder an den System-Prompts wiederholt. Die Abdeckung umfasst automatisierte Prompt-Injection-Tests, Jailbreak-Suiten und Indirekt-Injection-Korpora, die über realistische PR- und Issue-Oberflächen bereitgestellt werden.                                                                        | 2     |
| AC.2.4 | Stellen Sie sicher, dass die Bewertungen einem anerkannten Rahmen folgen, wie z. B. dem NIST AI RMF, dem NIST AI 600-1 Generative AI Profile oder der ISO/IEC 42001. Die Bewertungen werden nach einer größeren Versionsänderung, einem Vorfall beim Anbieter oder neuen Bedrohungsinformationen, die für die Tool-Klasse relevant sind, wiederholt.                                                                                                                                 | 3     |

Zuordnungen & Verweise:

* AC.2.1: OWASP LLM Top 10 (2025) LLM01, LLM06; OWASP Agentic Top 10 (2026) ASI01, ASI02, ASI03; AISVS C9; MITRE ATLAS (Threat modeling).
* AC.2.2: OWASP LLM Top 10 (2025) LLM03; OWASP Agentic Top 10 (2026) ASI04; NIST SSDF PO.1, PO.5; ISO/IEC 42001 Abschnitt 8.
* AC.2.3: MITRE ATLAS (Adversarial ML testing); AISVS C2.3; NIST AI 600-1 MEASURE.
* AC.2.4: ISO/IEC 42001 Klausel 9.2; NIST AI RMF GOVERN.

---

## AC.3 Sicheres Prompt- & Kontextmanagement

Zwei Ziele in dieser Familie. Erstens: verhindern, dass Geheimnisse, proprietärer Code und personenbezogene Daten in Prompts auslaufen. Zweitens: jeden Inhalt, der aus dem Repository, einem PR oder einem Dritten stammt, als nicht vertrauenswürdige Eingabe behandeln. Alles davon kann eine Prompt-Injection-Nutzlast enthalten, und in den meisten Fällen ist das nicht so. Gerade das macht den seltenen feindseligen Fall leicht zu übersehen.

>Beziehung zu AISVS C2.1: AC.3.3, AC.3.4 und AC.3.5 wenden AISVS C2.1 (Prompt Input Validation) im Coding-Fall an. Wenn ein Befund hier etwas ist, das die C2.1-Verifizierung nicht bereits geschlossen hat, zähle ihn als zusätzliche Lücke (spezifisch für die Konstruktion von Coding-Tool-Prompts). Wenn C2.1 es bereits geschlossen hat, zähle es nicht doppelt.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                        | Ebene |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.3.1 | Verifizieren Sie, dass die schriftliche Anleitung das Eingeben von Geheimnissen, Zugangsdaten, PII oder klassifizierten Daten in jede an ein KI-Tool gesendete Eingabe verbietet. Die Anleitung wird über Pre-Commit-Hooks, IDE-Integrationen und CI durchgesetzt.                                                                                                                                                                  | 1     |
| AC.3.2 | Stellen Sie sicher, dass technische Kontrollen automatisch sensible Inhalte aus jedem Kontextfenster entfernen, das an ein KI-Tool gesendet wird. Client-seitige Redaction, genehmigte Kontextfilter und Secret-Scanner mit Pre-Prompt-Hooks erfüllen alle die Anforderungen.                                                                                                                                                       | 1     |
| AC.3.3 | Verifizieren Sie, dass jeder extern bereitgestellte Kontext, der einem KI-Tool zugeführt wird, als nicht vertrauenswürdig behandelt und auf Prompt-Injection überprüft wird, bevor er den Prompt erreicht. Zu behandelnde Quellen: Pull-Request-Beschreibungen und Kommentare, von einer Fork bereitgestellte Diffs, Issue-Beschreibungen, Commit-Nachrichten, Dokumentation Dritter, Websuchergebnisse und Ausgaben von MCP-Tools. | 1     |
| AC.3.4 | Verifizieren Sie, dass das KI-Tool eine Anweisungs-Hierarchie durchsetzt, wobei System- und Entwicklernachrichten Vorrang vor nicht vertrauenswürdigen Repository-Inhalten haben. Diese Hierarchie muss über Multi-Turn-Konversationen und tool-unterstützte Workflows hinweg bestehen bleiben.                                                                                                                                     | 1     |
| AC.3.5 | Verifizieren Sie, dass die Eingabelängensteuerung verhindert, dass nicht vertrauenswürdige Pull Requests oder Repository-Inhalte Systemanweisungen oder Sicherheitsrichtlinien aus dem effektiven Kontextfenster verdrängen. Übergroße Eingaben werden unverzüglich zurückgewiesen. Stille Kürzung ist nicht akzeptabel.                                                                                                            | 2     |
| AC.3.6 | Stellen Sie sicher, dass Prompts und KI-Antworten sowohl während der Übertragung als auch im Ruhezustand verschlüsselt sind und gemäß der Datensicherheitsklassifizierungsrichtlinie aufbewahrt werden. Mandanten und Projekte sind kryptografisch voneinander getrennt.                                                                                                                                                            | 3     |

Zuordnungen & Verweise:

* AC.3.1: OWASP LLM Top 10 (2025) LLM02 (Offenlegung sensibler Informationen); OWASP ASVS v5 V14 (Datenschutz); ISO/IEC 27001:2022 A.8.12 (Verhinderung von Datenabfluss).
* AC.3.2: AISVS C2.4; OWASP LLM Top 10 (2025) LLM02; NIST SSDF PW.3.
* AC.3.3: AISVS C2.1, C2.4; OWASP LLM Top 10 (2025) LLM01; OWASP Agentic Top 10 (2026) ASI06; MITRE ATLAS (indirekte Prompt-Injection).
* AC.3.4: AISVS C2.1.2; OWASP LLM Top 10 (2025) LLM01; CISA Secure by Design.
* AC.3.5: OWASP LLM Top 10 (2025) LLM10; AISVS C2.1.4.
* AC.3.6: OWASP ASVS v5 V6 (Kryptografie), V14 (Datenschutz); ISO/IEC 27001:2022 A.8.24 (Einsatz von Kryptografie).

---

## AC.4 Validierung von KI-generiertem Code

Erkennen Sie die Schwachstellen, die durch die KI-Ausgabe eingeführt werden. Beheben Sie sie, bevor der Code einer Zusammenführung oder einer Bereitstellung zugeführt wird.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Ebene |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----- |
| AC.4.1 | Stellen Sie sicher, dass vom KI-System generierter Code immer durch eine Code-Überprüfung durch einen qualifizierten menschlichen Ingenieur geht. Der Prüfer darf nicht dieselbe Identität sein, die ursprünglich die KI-Generierung angefordert hat (Trennung der Verantwortlichkeiten). Und der KI-Agent selbst zählt nicht als menschlicher Prüfer.                                                                                                                         | 1     |
| AC.4.2 | Stellen Sie sicher, dass automatisiertes Sicherheitstesten bei jeder Pull Request ausgeführt wird, die von KI generierten Code enthält: SAST, IAST, DAST, Secret-Scanning, IaC-Scanning und SCA. Wo der Scanner dies unterstützt, sind AI-Zuordnungsbewusste Regeln aktiviert.                                                                                                                                                                                                 | 2     |
| AC.4.3 | Stellen Sie sicher, dass Pull Requests, die aus KI-generiertem Code bestehen, vom Zusammenführen blockiert werden, wenn ein automatischer Scan eine kritische Sicherheitsfeststellung erkennt, die als CVSS >= 9.0 oder der entsprechende Schwellenwert in der Richtlinie zur Schwierigkeitsgradeinstufung von Schwachstellen der Organisation definiert ist. Das Umgehen der Sperre erfordert eine schriftliche Ausnahme, die von einer autorisierten Person genehmigt wurde. | 2     |
| AC.4.4 | Stellen Sie sicher, dass sicherheitskritische Dateien eine erhöhte Prüf-Schwelle erfordern, wenn sie durch KI generiert oder geändert wurden: Zwei-Personen-Prüfung, Freigabe durch das Sicherheitsteam oder strengere Anforderungen. Zu den sicherheitskritischen Dateien hier zählen Authentifizierungs-, Autorisierungs- und Kryptografiecode; IAM-Richtlinien; CI/CD-Workflow-Definitionen; Bereitstellungs-Manifeste; sowie Sandbox- oder Netzwerkrichtlinienartefakte.   | 2     |
| AC.4.5 | Stellen Sie sicher, dass differentielles Fuzz-Testing oder eigenschaftsbasierte Tests die sicherheitskritischen Verhaltensweisen von KI-generiertem Code abdecken: Eingabevalidierung, Autorisierungslogik und Deserialisierungssicherheit.                                                                                                                                                                                                                                    | 3     |

Zuordnungen & Verweise:

* AC.4.1: NIST SSDF PW.7; OWASP ASVS v5 V10 (Codequalit\u00e4t); ISO/IEC 27001:2022 A.5.3 (Aufgabentrennung).
* AC.4.2: NIST SP 800-204D (Pipeline scanning controls); SLSA v1.2 Build Track L2; OWASP SAMM Security Testing (ST).
* AC.4.3: OWASP CI/CD Top 10 CICD-SEC-04 (Vergiftete Pipeline-Ausfuehrung); NIST SSDF PW.7, PW.8.
* AC.4.4: NIST SSDF PW.4, PW.7; OWASP CI/CD Top 10 CICD-SEC-01 (Insufficient Flow Control); ISO/IEC 27001:2022 A.8.32 (Change Management).
* AC.4.5: NIST SSDF PW.8; OWASP ASVS v5 V11 (Geschäftslogik).

---

## AC.5 Erklärbarkeit & Nachvollziehbarkeit von Codevorschlägen

Auditoren, Verteidiger und die Entwickler selbst müssen sehen können, warum eine bestimmte KI-Empfehlung abgegeben wurde und wie sie in einem ausgelieferten Artefakt gelandet ist.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                           | Ebene |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.5.1 | Stellen Sie sicher, dass Prompt-und-Antwort-Paare mit stabilen Korrelationskennungen protokolliert werden, sodass ein Ermittler die gesamte Kette später erneut abspielen kann: Prompt → Antwort → Commit → Build → Deployment.                                        | 1     |
| AC.5.2 | Stellen Sie sicher, dass Entwickler die Zitate (Training Snippets, abgerufene Dokumente, Ausgaben von MCP-Tools) anzeigen können, die eine Empfehlung unterstützen, und dass die Zitierkette mit dem Artefakt mitwandert.                                              | 2     |
| AC.5.3 | Verifizieren, dass Erklärbarkeitsberichte, KI-Ereignisprotokolle und Zitieraufzeichnungen in manipulationssicherem Speicher abgelegt werden (append-only, WORM oder ein unveränderlicher Log-Store) und dass sie während Sicherheitsüberprüfungen referenziert werden. | 3     |

Zuordnungen & Verweise:

* AC.5.1: ISO/IEC 42001 Abschnitt 7.5 (Dokumentierte Informationen); OWASP ASVS v5 V8 (Protokollierung); NIST SP 800-218A (Leitfaden zur Protokollierung für Generative KI).
* AC.5.2: NIST AI RMF-Maßnahme; OWASP LLM Top 10 (2025) LLM03.
* AC.5.3: ISO/IEC 27001:2022 A.8.15 (Protokollierung); NIST AI 600-1 MESSUNG; ISO/IEC 42001 (Nachverfolgbarkeit).

---

## AC.6 Kontinuierliches Feedback, adversarialer Test & Modell-Feinabstimmung

Verbessern Sie die Modellsicherheit im Laufe der Zeit. Achten Sie auf negativen Drift. Setzen Sie das Red-Teaming der KI-Tools fort. Der Umfang des Red-Teaming in dieser Familie umfasst die KI-Tools selbst; die zugrunde liegenden Systeme und Dienste, von denen die Tools abhängen, werden von separaten Programmen behandelt.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                            | Ebene |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.6.1 | Verifizieren, dass Entwickler und Prüfer unsichere oder nicht-konforme Vorschläge markieren können und dass jede Markierung bis zur Schließung nachverfolgt wird, mit Links zurück zur zugrunde liegenden Eingabeaufforderung und Antwort sowie weiter zu allen nachgelagerten Artefakten.                                                                                                              | 1     |
| AC.6.2 | Stellen Sie sicher, dass aggregiertes Feedback in periodische Updates der System-Prompt(s) einfließt oder dass eine Retrieval-Augmented Generation anhand geprüfter Secure-Coding-Korpora erfolgt (OWASP Cheat Sheets, interne Coding-Standards). Wenn die Organisation die Modell-Trainingsinfrastruktur kontrolliert, ist außerdem ein Fine-Tuning auf demselben Feedback-Korpus erforderlich.        | 2     |
| AC.6.3 | Stellen Sie sicher, dass geplante Red-Team-Übungen auf das KI-Tooling selbst ausgerichtet sind. Die Übungen beinhalten direkte und indirekte Prompt-Injection-Tests, die über realistische PR-, Issue- und Kommentar-Oberflächen bereitgestellt werden, Jailbreak-Korpora sowie die Erzeugung von Supply-Chain-Payloads. Die Ergebnisse werden unter Einhaltung nachverfolgbarer Severity-SLAs behoben. | 2     |
| AC.6.4 | Stellen Sie sicher, dass ein Closed-Loop-Evaluations-Framework nach jedem Fine-tuning, System-Prompt-Änderung oder Modell-Upgrade Regressionstests ausführt. Sicherheitsmetriken müssen den bisherigen Baseline-Wert erreichen oder überschreiten, bevor eine Bereitstellung erfolgt.                                                                                                                   | 3     |

Zuordnungen & Verweise:

* AC.6.1: NIST AI RMF MANAGE; ISO/IEC 42001 Klausel 10; OWASP SAMM Fehlerbehebungsmanagement (DM).
* AC.6.2: OWASP LLM Top 10 (2025) LLM03; NIST SSDF PO.3.
* AC.6.3: MITRE ATLAS (Adversarial-ML-Lifecycle); NIST AI 600-1 MEASURE 2.7; OWASP SAMM Security Testing (ST).
* AC.6.4: ISO/IEC 42001 Abschnitt 9.1; NIST AI RMF MESSUNG.

---

## AC.7 Von KI erzeugte Infrastruktur- und Pipeline-Artefakte

Infrastrukturcode, CI/CD-Workflow-Dateien, Bereitstellungsmanifeste und sicherheitsbezogene Richtlinienartefakte haben jeweils eine überproportionale Auswirkung, wenn sie fehlerhaft sind. Wenn KI sie generiert, muss die Validierung entsprechend strenger sein als bei gewöhnlichem Anwendungscode.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Ebene |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.7.1 | Stellen Sie sicher, dass KI-generierte oder KI-modifizierte Artefakte eindeutig als solche gekennzeichnet und entsprechend nachverfolgt werden. In den Geltungsbereich fallen folgende Artefaktklassen: Infrastructure-as-Code (Terraform, CloudFormation, Pulumi, Bicep), CI/CD-Workflow-Dateien (GitHub Actions, GitLab CI, Jenkinsfile, Argo Workflows, Tekton), Container- und Orchestrierungs-Manifestdateien (Dockerfile, Kubernetes, Helm) sowie Artefakte für Sicherheitsrichtlinien (IAM, OPA/Rego, NetworkPolicy, Admission Controller). | 1     |
| AC.7.2 | Stellen Sie sicher, dass durch KI generierte Infrastruktur- und Pipeline-Konfigurationen eine menschliche Überprüfung und Genehmigung erfordern, bevor sie in jeder Umgebung außer einer hermetischen Sandbox ausgeführt werden.                                                                                                                                                                                                                                                                                                                   | 2     |
| AC.7.3 | Verifizieren Sie, dass durch KI generierte Infrastruktur- und Workflow-Änderungen die Policy-as-Code-Durchsetzung (OPA, Conftest, Checkov, tfsec, KICS, kube-linter) auf demselben Niveau wie oder strenger als von Menschen verfasste Änderungen bestehen. Richtlinienverletzungen blockieren die Promotion.                                                                                                                                                                                                                                      | 2     |
| AC.7.4 | Stellen Sie sicher, dass Änderungen an den Konfigurationen für Pipeline-Trigger mit hoher Auswirkung sowohl eine Dual-Control-Freigabe als auch eine Überprüfung durch das Sicherheitsteam erfordern, unabhängig davon, wer oder was die Änderung vorgenommen hat. Die in diesem Umfang enthaltenen Konfigurationen umfassen GitHub Actions`pull_request_target`und`workflow_run`, selbstgehostete Runner-Labels, Workflow`permissions:`Blöcke, OIDC-Trust-Richtlinien und Zuordnungen von Secret-Umgebungen.                                      | 2     |
| AC.7.5 | Stellen Sie sicher, dass die Drift-Erkennung die bereitgestellte Infrastruktur und die Live-Workflow-Konfigurationen mit den signierten, durch KI zugeordneten Baselines vergleicht und bei jeder nicht autorisierten Änderung alarmiert.                                                                                                                                                                                                                                                                                                          | 3     |

Zuordnungen & Verweise:

* AC.7.1: OWASP CI/CD Top 10 CICD-SEC-05 (Unzureichendes PBAC); SLSA v1.2 Build-Track-Provenienz; NIST SSDF PW.1.
* AC.7.2: NIST SP 800-204D (Freigabe-Gating); OWASP CI/CD Top 10 CICD-SEC-01; ISO/IEC 27001:2022 A.8.32 (Änderungsmanagement).
* AC.7.3: OWASP ASVS v5 V10 (CI/CD Deployment Security); OWASP CI/CD Top 10 CICD-SEC-07 (Insecure System Configuration); NIST SSDF PW.4.
* AC.7.4: OWASP CI/CD Top 10 CICD-SEC-01, CICD-SEC-02; GitHub Security Lab „Preventing pwn requests“-Reihe; NIST SP 800-204D (Pipeline-Governance).
* AC.7.5: NIST SP 800-204D (Continuous monitoring); ISO/IEC 27001:2022 A.8.19.

---

## AC.8 Anforderungen an die Änderungssteuerung für autonome Agenten

Autonome KI-Agenten, die Code oder Konfiguration generieren, erhalten die gleiche Trennung von Aufgaben wie Menschen. Sie können ihre eigene Arbeit nicht genehmigen, zusammenführen oder befördern. Dies gilt sowohl auf der Policy-Ebene als auch auf der technischen Ebene.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                               | Ebene |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----- |
| AC.8.1 | Stellen Sie sicher, dass autonome Agenten keine Artefakte genehmigen, zusammenführen, signieren oder bereitstellen können, die sie selbst erzeugt haben, und dass diese Einschränkung durch das Quellcodeverwaltungssystem, das CI-System und das Artefakt-Repository erzwungen wird. Allein die Richtlinie erfüllt diese Kontrolle nicht. | 1     |
| AC.8.2 | Stellen Sie sicher, dass KI-Systeme mit vorab festgelegten, nicht-menschlichen Identitäten (Service Accounts, Workload-Identitäten, von OIDC ausgegebene ephemere Tokens) ausgeführt werden und dass diese Identitäten nicht dazu verwendet werden können, um ihre eigenen generierten Artefakte über Umgebungen hinweg zu bewerben.       | 2     |
| AC.8.3 | Stellen Sie sicher, dass autonome Agenten Branch-Schutz, erforderliche Überprüfungen, erforderliche Statusprüfungen, signierte-Commit-Anforderungen oder Merge-Queues nicht umgehen können. Jeder Versuch eines Agenten, diese Einstellungen zu ändern, löst einen Sicherheitsalarm aus.                                                   | 2     |
| AC.8.4 | Stellen Sie sicher, dass die Aufgabentrennung über die Phasen einer durch KI erzeugten Änderung hinweg gilt. Jede Phase (Generierung, Überprüfung, Freigabe, Bereitstellung) wird von einer eigenständigen verantwortlichen Instanz ausgeführt, sei es ein Mensch oder ein System.                                                         | 3     |

Zuordnungen & Verweise:

* AC.8.1: OWASP Agentic Top 10 (2026) ASI03 (Missbrauch von Identität und Privilegien), ASI10 (Rogue Agents); OWASP ASVS v5 V10; NIST SP 800-53r5 AC-5 (Trennung von Zuständigkeiten).
* AC.8.2: NIST SP 800-207 (Zero Trust Architektur); OWASP CI/CD Top 10 CICD-SEC-02; ISO/IEC 27001:2022 A.5.15 (Zugriffskontrolle).
* AC.8.3: OWASP CI/CD Top 10 CICD-SEC-01; GitHub Docs (Branch protection rules and rulesets); OWASP Agentic Top 10 (2026) ASI03.
* AC.8.4: NIST SSDF PO.2; ISO/IEC 27001:2022 A.5.3; NIST SP 800-53r5 AC-5.

---

## AC.9 KI-Artifact-Ursprungsvalidierung für die Bereitstellung

Bereitstellungs- und Promotions-Pipelines müssen die kryptografische Herkunft und die Generierungshistorie von KI-generierten Artefakten validieren. Sie tun dies, bevor sie das Artefakt durchlassen.

<!-- markdownlint-disable MD013 -->
| #      | Beschreibung                                                                                                                                                                                                                                                                                                                                                            | Ebene |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.9.1 | Verifizieren Sie, dass durch KI erzeugte Artefakte eine signierte Herkunfts- und Generierungsmetadaten tragen (in-toto- oder SLSA-Provenance-Attestierungen, AI-BOM-Einträge), die das KI-System identifizieren, das sie erzeugt hat, den Generierungskontext, die beteiligten Menschen und die zugehörigen Prüfprotokolle.                                             | 1     |
| AC.9.2 | Stellen Sie sicher, dass Bereitstellungspipelines das Vorhandensein, die Signatur und die Integrität von Ursprungs- und Generierungsmetadaten auf KI-erzeugten Artefakten vor der Beförderung überprüfen, mithilfe eines vertrauenswürdigen Verifiers (Sigstore/cosign, in-toto-Verifizierung).                                                                         | 2     |
| AC.9.3 | Stellen Sie sicher, dass Artefakte bei der Bereitstellung zurückgewiesen und zur Überprüfung in Quarantäne verschoben werden, wenn ihnen die erforderlichen Ursprungs- und Generierungsinformationen fehlen, sie mit nicht vertrauenswürdigen Schlüsseln signiert sind oder von einem nicht genehmigten KI-System oder einer nicht genehmigten Umgebung erzeugt wurden. | 3     |

Zuordnungen & Verweise:

* AC.9.1: SLSA v1.2 (Provenienz-Atestierungen); CycloneDX ML-BOM; In-toto-Attestation-Framework.
* AC.9.2: SLSA v1.2 (Verification Summary Attestations); Sigstore/cosign (Signaturverifizierung); OWASP SCVS.
* AC.9.3: SLSA v1.2 (Verifieranforderungen); NIST SP 800-204D (Promotion-Gating).

---

## AC.10 Vollständigkeit und Validierung des Generation-Audit-Trails

Von KI erzeugte Artefakte benötigen vollständige und konsistente Herkunfts- und Generierungsaufzeichnungen, die vor der Integration oder Bereitstellung validiert werden. Der Grund ist entscheidend. Durchsetzung der Herkunftsverfolgung auf Basis von Richtlinien funktioniert nur, wenn die erfassten Informationen selbst vollständig und konsistent sind. Wenn Aufzeichnungen Felder vermissen oder wenn die vorhandenen Felder einander widersprechen, werden Erkennungen übersehen und die Durchsetzung schafft Lücken. Daher wird die Herkunftsverfolgung hier als erstklassige Anforderung behandelt und vor der Akzeptanz eines Artefakts validiert.

<!-- markdownlint-disable MD013 -->
| #       | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Ebene |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.10.1 | Stellen Sie sicher, dass KI-generierte Artefakte die erforderlichen Ursprungs- und Generierungsfelder tragen: Modellidentität und -version, Werkzeug- oder Agentenidentität, Generierungskontext, Prompt-Hash, menschliche Beteiligung, Sitzungskennungen und Korrelations-IDs.                                                                                                                                                                                              | 1     |
| AC.10.2 | Stellen Sie sicher, dass die Metadaten für Herkunft und Generierung auf Vollständigkeit und Konsistenz geprüft werden: keine fehlenden oder mehrdeutigen Felder, Werte in eine einzige Darstellung normalisiert und eine Signaturkette, die bis zu einer vertrauenswürdigen Wurzel zurückvalidiert.                                                                                                                                                                          | 2     |
| AC.10.3 | Verifizieren, dass Artefakte mit unvollständigen, inkonsistenten oder nicht verifizierbaren Ursprungs- und Generierungsmetadaten vor dem Zusammenführen (Merge) oder der Bereitstellung abgelehnt werden, und dass das Ereignis der Ablehnung protokolliert wird, damit Trends verfolgt werden können. Die Ablehnung erfolgt auf der Verifizierer-Seite, anhand des in SLSA definierten Attestations- oder Proof-Modells sowie der Verifizierungskriterien in ISO/IEC 42001. | 3     |

Zuordnungen & Verweise:

* AC.10.1: CycloneDX ML-BOM-Schema; NIST SP 800-218A (Provenienz für Generative AI); ISO/IEC 42001 Abschnitt 7.5.
* AC.10.2: OWASP SCVS (Herkunft und Abstammung); SLSA v1.2 VSA-Verifizierung.
* AC.10.3: SLSA v1.2 (Durchsetzung auf der Verifier-Seite); ISO/IEC 42001 Klausel 9.

---

## AC.11 AI Code-Review & Assistant Bot-Härtung

KI-Code-Review-Bots, PR-Kommentar-Bots, MCP-gesteuerte Assistenten (Model Context Protocol) und IDE-Copilots sind alle über nicht vertrauenswürdigen Repository-Inhalt erreichbar. Die erreichbaren Angriffsflächen umfassen PR-Diffs, Beschreibungen, Kommentare, Issues und alle Workflow-Dateien, die von einem Fork bereitgestellt werden. Diese Kategorie deckt den Fall ab, in dem ein Angreifer eine dieser Oberflächen nutzt, um den eigenen KI-Agenten des Verteidigers dazu zu bringen, eine Supply-Chain-Attacke zu genehmigen, zu ignorieren oder aktiv zu unterstützen.

>Beziehung zu AISVS C2.1, C9.3 und C9.6: AC.11.1 bis AC.11.5 sind Anwendungen von drei AISVS-Kapitelkontrollen auf den konkreten Fall von KI-Code-Reviews und Assistant-Bots, die über nicht vertrauenswürdige PR-Inhalte (Pull Requests) operieren. Die drei Kapitelkontrollen sind C2.1 (Prompt Input Validation), C9.3 (Tool Sandboxing) und C9.6 (Action Authorization). Der Anhang fasst jede dieser Kontrollen erneut zusammen, jedoch mit botspezifischer Anleitung. Die Zählregel ist wie an anderer Stelle: Eine Feststellung hier ist entweder eine zusätzliche Lücke, die das übergeordnete Kapitel nicht geschlossen hat, oder sie ist bereits im Kapitel gezählt. Nicht beides.

<!-- markdownlint-disable MD013 -->
| #       | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                              | Ebene |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.11.1 | Verifizieren Sie, dass KI-Review- und Assistenz-Bots jede vom PR bereitgestellte Inhaltspassage (Diff, Titel, Beschreibung, Kommentare, Dateiinhalte, Commit-Nachrichten, verlinkte externe URLs) als nicht vertrauenswürdig behandeln und die AISVS-C2.1-Prompt-Injection-Abwehrmaßnahmen anwenden: Durchsetzung der Anweisungshierarchie, Inhaltsbereinigung und Erkennung von indirekten Injections.                   | 1     |
| AC.11.2 | Stellen Sie sicher, dass die System-Prompts und Richtlinienkonfigurationen für den KI-Review und den Assistant-Bot beim Laden auf Integrität geprüft werden (signiert, hash-gesichert/„hash-pinned“) und dass nichts im Repository, in den Inhalten des Branches, in PR-Quell-Umgebungsvariablen oder in irgendeiner anderen nutzerkontrollierbaren Eingabe sie ändern kann.                                              | 1     |
| AC.11.3 | Stellen Sie sicher, dass KI-Review- und Assistenzbots ausschließlich strukturiertes, schema-validiertes Ausgabeformat ausgeben (JSON mit einer Whitelist von Feldern und Aktionen). Jede frei formulierte Ausgabe wird als nicht vertrauenswürdig behandelt und niemals als Befehl, Abfrage, Shell-Snippet oder Workflow-Schritt ausgeführt.                                                                              | 1     |
| AC.11.4 | Verifizieren Sie, dass KI-Review- und Assistenz-Bots in netzwerkisolierten, least-privilege-Sandboxes laufen: ein dedizierter Namespace, ausgehender Standard-Block (default-deny egress) mit einer Allowlist für nur genehmigte APIs, keine eingebundenen Repository-Geheimnisse und ausschließlich temporäre, ephemere Zugangsdaten.                                                                                    | 2     |
| AC.11.5 | Stellen Sie sicher, dass jede privilegierte Aktion, die ein Bot ausführen kann (Genehmigung eines PR, Zusammenführen, Kennzeichnen, Ablehnen von Reviews, Kommentieren außerhalb seines Sandboxes, Aufrufen externer Tools), über einen separaten, überprüften Autorisierungsweg läuft. Dieser Pfad wird von einer Richtlinien-Engine entschieden, nicht vom LLM.                                                         | 2     |
| AC.11.6 | Stellen Sie sicher, dass KI-Review- und Assistenten-Bots alle Prompts (einschließlich extern bereitgestelltem Kontext), Tool-Aufrufe und Ausgaben in manipulationssicherem Speicher protokollieren. Exfiltrationsindikatoren werden kontinuierlich anhand von Egress-Mustern (URLs, IPs, DNS, Nutzdatenmengen) überwacht, wobei die Benachrichtigung für Ziele wie Webhooks, Paste-Sites und Bin-Services abgestimmt ist. | 2     |
| AC.11.7 | Stellen Sie sicher, dass KI-Review-Bots in einem Zero-Privilege-, schreibgeschützten Shadow-Modus für nicht vertrauenswürdige Fork-PRs ausgeführt werden. Im Shadow-Modus ist die Inline-Kommentar-Erzeugung von Code eingeschränkt und die Interaktion mit privilegierten Workflows ist verboten, bis ein Repository-Wartender eine anfängliche, erste Verifizierung für Erstbeiträge freigegeben hat.                   | 2     |
| AC.11.8 | Überprüfen Sie, dass KI-Review- und Assistenz-Bots einem kontinuierlichen adversarialen Testing unterliegen: Indirekte-Prompt-Injection-Corpora werden gegen den Bot über simulierte PRs, Issues und Kommentare erneut abgespielt. Die Erkennungswirksamkeit wird im Zeitverlauf erfasst, und eine Regression blockiert das Modell oder die Prompt-aktualisierung, die sie verursacht hat.                                | 3     |

Zuordnungen & Verweise:

* AC.11.1: AISVS C2.1, C2.4; OWASP LLM Top 10 (2025) LLM01; OWASP Agentic Top 10 (2026) ASI01, ASI06.
* AC.11.2: AISVS C9.7; OWASP LLM Top 10 (2025) LLM01; OWASP Agentic Top 10 (2026) ASI01.
* AC.11.3: AISVS C9.6.4; OWASP LLM Top 10 (2025) LLM05; OWASP Agentic Top 10 (2026) ASI02, ASI05.
* AC.11.4: AISVS C9.3; OWASP Agentic Top 10 (2026) ASI02, ASI03, ASI05; NIST SP 800-204D (Workload isolation).
* AC.11.5: AISVS C9.6.4; OWASP ASVS v5 V4 (Zugriffskontrolle); OWASP Agentic Top 10 (2026) ASI02, ASI03.
* AC.11.6: OWASP ASVS v5 V8 (Logging & Error Handling); OWASP LLM Top 10 (2025) LLM02; ISO/IEC 27001:2022 A.8.15, A.8.16.
* AC.11.7: GitHub Security Lab "Preventing pwn requests" Reihe (Teile 1-4); OWASP Agentic Top 10 (2026) ASI01, ASI03, ASI09; OWASP CI/CD Top 10 CICD-SEC-01.
* AC.11.8: MITRE ATLAS (Indirekte Prompt-Injection); AISVS C2.3; OWASP SAMM Security Testing (ST).

---

## AC.12 CI/CD-Pipeline-Härtung speziell für KI-Erweiterung

Zwei Arten von CI/CD-Pipeline-Kontrollen sind für diese Familie im Geltungsbereich: solche, die KI-Erweiterung _newly requires_, und diejenigen, bei denen KI-Augmentation _breaks_. Allgemeine CI/CD-Hygiene ist hier nicht im Umfang; sie wird anderweitig behandelt. Kurzlebige Anmeldeinformationen, unveränderliche Action-Pinning, Branch-Protection, SLSA-Build-Track-L3-Provenienz und Multi-Party-Produktionsfreigaben werden alle von OWASP ASVS v5 V10, den OWASP Top 10 CI/CD-Sicherheitsrisiken (CICD-SEC-01 bis CICD-SEC-10), NIST SP 800-204D und SLSA v1.2 adressiert. Anwender setzen diese Baselines um und prüfen sie anhand der zugrunde liegenden Standards. Wir wiederholen diese Bewertung hier nicht.

<!-- markdownlint-disable MD013 -->
| #       | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Ebene |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.12.1 | Überprüfen Sie, dass Workflows, die durch nicht vertrauenswürdige Beiträge ausgelöst werden (GitHub Actions`pull_request_target`, `workflow_run`, and equivalent fork-aware triggers in other CI systems) never check out, build, test, or otherwise execute untrusted code in a context that has repository write permissions or access to repository, organization, package-registry, cloud, or deployment secrets. Where a privileged follow-up step is needed, the untrusted contribution is first processed in an unprivileged`pull_request`Workflow, und es werden nur validierte passive Artefakte an einen separaten privilegierten Workflow weitergegeben. | 1     |
| AC.12.2 | Stellen Sie sicher, dass Geheimnisse, Anmeldeinformationen und Token für Pipeline-Jobs nicht in Arbeitsbereichen persistiert werden, die KI-betroffenen oder aus einer Fork stammenden nicht vertrauenswürdigen Code verarbeiten. Setzen Sie zum Beispiel`persist-credentials: false`bei der Auschecken-Funktion, wenn die Plattform dies unterstützt, und CI-Runner von zwischengespeicherten Anmeldeinformationen bereinigen, bevor die KI-Tools ausgeführt werden.                                                                                                                                                                                               | 1     |
| AC.12.3 | Stellen Sie sicher, dass keine Geheimnisse an Workflows offengelegt werden, die Code aus Forks oder von erstmaligen Mitwirkenden ausführen. Umgebungs-Schutzregeln (oder das entsprechende Äquivalent der Plattform, z. B. geschützte Variablen und Bereitstellungsfreigaben) erfordern eine manuelle Genehmigung, bevor ein Job mit Geheimnissen für diese Beiträge ausgeführt werden darf. Diese Kontrolle ist mit AC.11.7 und AC.13.2 gekoppelt. Die Durchsetzung auf Bot-Ebene gemäß AC.11.7 ersetzt nicht die hier erforderte Durchsetzung auf Plattform-Ebene.                                                                                                | 1     |
| AC.12.4 | Stellen Sie sicher, dass selbst gehostete oder persistente Runner, die von AI-Tools verwendet werden, ephemer sind (nach jedem Job zerstört), netzwerksegmentiert und von Produktionsanmeldeinformationen getrennt sind. Persistente oder lang laufende Runner verarbeiten unter keinen Umständen Fork-PRs oder von AI generierte, nicht vertrauenswürdige Artefakte.                                                                                                                                                                                                                                                                                               | 2     |
| AC.12.5 | Überprüfen Sie, dass Änderungen an Workflow-Definitionsdateien (`.github/workflows/*`, `.gitlab-ci.yml`, `Jenkinsfile`, Argo, Tekton und entsprechende) werden auf jeder PR erkannt und über einen erweiterten Prüfpfad geleitet, der einen Sicherheitsprüfer einschließt, unabhängig davon, wer der Beiträger ist, oder ob KI beteiligt war. KI-Agenten dürfen keine Umgehungsbefugnis für diesen Prüfpfad erhalten.                                                                                                                                                                                                                                               | 2     |
| AC.12.6 | Stellen Sie sicher, dass Pipeline-Audit-Logs (Workflow-Ausführungen, Secret-Zugriffe, Runner-Registrierung, Berechtigungsvergaben, Ausstellung von OIDC-Tokens) in Echtzeit an zentrales Sicherheitsmonitoring gestreamt werden. Die Erkennungsregeln sind auf AI-gestützte Bedrohungsmuster abgestimmt: Massenerstellung von Pull Requests durch neue Konten, Änderungen an Workflow-Dateien in Fork-PRs, unerwartete Secret-Zugriffe aus AI-Runner-Pools sowie ungewöhnlicher ausgehender Datenverkehr (Webhooks, Paste-Sites, Bin-Dienste) von AI-Workloads.                                                                                                     | 2     |
| AC.12.7 | Überprüfen Sie, dass Artefakte, die von nicht vertrauenswürdigen PR-Workflows erzeugt werden, als nicht vertrauenswürdige passive Daten behandelt werden, wenn ein privilegierter Folge-Workflow sie konsumiert. Der privilegierte Workflow führt niemals ausführbare Dateien, Skripte, Pakete, Caches oder generierte Workflow-Fragmente aus, die aus einem nicht vertrauenswürdigen Beitrag stammen.                                                                                                                                                                                                                                                              | 2     |
| AC.12.8 | Stellen Sie sicher, dass die Behebung eines verwundbaren Workflows das Ungültigmachen oder erneute Validieren aller PRs umfasst, die vor dem Eintreffen der Korrektur geöffnet wurden. Ohne diesen Schritt kann ein späterer Commit in derselben PR die veraltete Workflow-Definition aufgreifen und die Korrektur umgehen.                                                                                                                                                                                                                                                                                                                                         | 2     |

Zuordnungen & Verweise:

* AC.12.1: OWASP CI/CD Top 10 CICD-SEC-01, CICD-SEC-04; GitHub Security Lab "Preventing pwn requests" Reihe; NIST SP 800-204D (Pipeline-Isolation).
* AC.12.2: OWASP CI/CD Top 10 CICD-SEC-02, CICD-SEC-06; GitHub Docs (automatische Token-Authentifizierung und Berechtigungen); NIST SP 800-53r5 AC-6 (Least Privilege).
* AC.12.3: OWASP CI/CD Top 10 CICD-SEC-01; GitHub-Dokumentation (Workflow-Ausführungen aus öffentlichen Forks genehmigen; Geschützte Umgebungen); GitLab-Dokumentation (Geschützte Variablen).
* AC.12.4: OWASP CI/CD Top 10 CICD-SEC-06; NIST SP 800-204D (Runner-Isolation); ISO/IEC 27001:2022 A.8.22 (Netzwerksegmentierung).
* AC.12.5: OWASP CI/CD Top 10 CICD-SEC-01; NIST SSDF PW.7; ISO/IEC 27001:2022 A.8.32.
* AC.12.6: OWASP ASVS v5 V8 (Logging); OWASP CI/CD Top 10 CICD-SEC-10 (Insufficient Logging and Visibility); ISO/IEC 27001:2022 A.8.16.
* AC.12.7: GitHub Security Lab „Preventing pwn requests“-Reihe; OWASP CI/CD Top 10 CICD-SEC-01; NIST SP 800-204D (Cross-Workflow-Trust-Boundaries).
* AC.12.8: GitHub Security Lab "Preventing pwn requests" Teil 4 (Alvaro Munoz, 2025); OWASP CI/CD Top 10 CICD-SEC-01; NIST SSDF RV.1.

---

## AC.13 Erkennung von adversarialer KI in eingehenden Beiträgen

Die vorherigen Familien drehten sich darum, Ihre eigene KI vor Missbrauch zu schützen. Diese hier kehrt die Perspektive um. Hier ist die KI auf der Seite des Angreifers, und Sie versuchen, das Signal in eingehenden Beiträgen und Inhalten zu erkennen. Zu schützen ist vor dem Szenario, in dem ein Angreifer mithilfe von KI Fork-and-PR-Kampagnen im großen Maßstab ausführt, mit bösartigen Nutzdaten, die auf das Ziel-Repository zugeschnitten sind.

<!-- markdownlint-disable MD013 -->
| #       | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Ebene |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.13.1 | Überprüfen Sie, dass die Analysen zu Beitragsgeschwindigkeit und Mitwirkenden- Reputation Anomalien kennzeichnen: die Massenerstellung von PRs (Pull Requests) durch neu erstellte Konten, koordinierte Fork-Wellen unmittelbar vor PRs, PR-Volumen, die nicht mit menschlicher Urheberschaft übereinstimmen, sowie die Wiederverwendung von Payload-Mustern über nicht verwandte Repositories hinweg.                                                                                                                                              | 1     |
| AC.13.2 | Stellen Sie sicher, dass Pull Requests von Erst- oder Personen mit geringer Reputation die Zustimmung des Maintainers erfordern, bevor sie von privilegierten Workflows verarbeitet werden. Privilegierte Workflows umfassen hier KI-Prüf-Bots, Jobs mit Geheimnissen und Aufrufe externer Integrationen.                                                                                                                                                                                                                                           | 1     |
| AC.13.3 | Verifizieren Sie, dass automatische PR-Pipeline-Gates bekannte Indikatoren für von LLM generierte oder durch LLM unterstützte bösartige Payload-Muster erkennen: registry-konfusable oder typosquattierte Abhängigkeitsnamen, Paketreferenzen, die sich auf keine veröffentlichte Version auflösen lassen, sowie Abhängigkeiten, deren Erstellungs-, Ersteröffnungs- oder Betreuer-Änderungszeitstempel im Verhältnis zum PR anomal wirken.                                                                                                         | 2     |
| AC.13.4 | Stellen Sie sicher, dass die Erkennungsregeln mit MITRE ATT&CK (T1195 Supply Chain Compromise und CI/CD-relevante Sub-Techniques) sowie mit MITRE ATLAS-Techniken gekennzeichnet sind, für den Anwendungsfall der eingehenden Beitragsanalyse beibehalten werden und anhand aktueller Bedrohungsinformationen überprüft werden.                                                                                                                                                                                                                     | 2     |
| AC.13.5 | Stellen Sie sicher, dass bestätigte oder hochkonfidente bösartige Beiträge eine automatisierte Eindämmung auslösen: blockieren Sie den PR, isolieren Sie die Fork, setzen Sie den Beitragenden aus, benachrichtigen Sie die Betreuer und frieren Sie die betroffenen Workflow-Dateien ein. Triage-Entscheidungen fließen zurück in das Detection-Tuning.                                                                                                                                                                                            | 3     |
| AC.13.6 | Stellen Sie sicher, dass PR-Analysen strukturiertes AST-Profiling sowie stylometrische oder entropiebasierte Heuristiken umfassen, die auf die Identifizierung von LLM-generierten Code-Mustern abgestimmt sind. Die Erkennung in dieser Kategorie entwickelt sich weiterhin, daher werden kompensierende Kontrollen akzeptiert anstelle einer hochpräzisen automatisierten Erkennung: verpflichtende menschliche Prüfung bei markierten PRs, sandbox-Ausführung verdächtiger Payloads und aufgeschobenes Merge, bis zusätzliche Signale vorliegen. | 3     |

Zuordnungen & Verweise:

* AC.13.1: OWASP CI/CD Top 10 CICD-SEC-01; NIST AI RMF MANAGE; MITRE ATLAS (Reconnaissance).
* AC.13.2: GitHub-Dokumentation (Workflow-Ausführungen aus öffentlichen Forks genehmigen); OWASP CI/CD Top 10 CICD-SEC-01; NIST SSDF PW.4.
* AC.13.3: OWASP LLM Top 10 (2025) LLM03; OWASP CI/CD Top 10 CICD-SEC-03 (Missbrauch der Abhängigkeitskette); NIST SSDF PW.4.
* AC.13.4: MITRE ATT&CK T1195; MITRE ATLAS (Technologie-Katalog); OWASP SAMM Threat Assessment (TA).
* AC.13.5: NIST AI RMF MANAGE; ISO/IEC 27001:2022 A.5.25 (Bewertung von Informationssicherheitsereignissen); OWASP SAMM Incident Management (IM).
* AC.13.6: MITRE ATLAS (Erkennung von Adversarial ML-Ausgaben, Research-Edge); OWASP LLM Top 10 (2025) LLM03; NIST SSDF PW.8.

---

## AC.14 Kompromittierungs-Eindämmung & Automatisierte Remediation

Irgendwann gehen die Dinge schief. Wenn ein kompromittierter Vorfall im Umfeld von KI (ein prompt-injizierter Bot, ein offengelegtes CI-Geheimnis, ein bösartiges KI-generiertes Artefakt in einem Build) vermutet oder bestätigt wird, besteht das Ziel darin, den Schaden einzudämmen und die Wiederherstellung zu verkürzen.

<!-- markdownlint-disable MD013 -->
| #       | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Ebene |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| AC.14.1 | Verifizieren Sie, dass ein Incident-Response-Playbook für einen AI-in-pipeline-compromise vorhanden ist. Mindestens deckt es Folgendes ab: Widerruf von AI-Agent-Zugriffsberechtigungen, Rotation jedes Secrets, das mit dem kompromittierten Workflow-Run in Berührung gekommen ist, Quarantänisierung der kompromittierten Artefakte, Benachrichtigung der nachgelagerten Konsumenten, Benachrichtigung der Aufsichtsbehörden, sofern anwendbar, sowie die Aufbewahrung von Prompts, Antworten und Audit-Logs zur forensischen Untersuchung. | 1     |
| AC.14.2 | Verifizieren Sie, dass alle Geheimnisse, die einen mit einem verdächtigen PR, einem Prompt-Injection-Ereignis oder einer KI-Agent-Anomalie verbundenen Workflow-Run berührt haben, automatisch rotiert werden, und dass nachgelagerte Aussteller (Cloud-IAM, Paket-Repositories, Verwahrer von Signierschlüsseln) über die Rotation benachrichtigt werden.                                                                                                                                                                                     | 1     |
| AC.14.3 | Stellen Sie sicher, dass Identitäten von KI-Agenten (Schlüssel, Token, OIDC-Trust-Grants) schnell widerrufen und quarantänisiert werden können, mit einer Zielzeit für den Widerruf, die schriftlich festgehalten und mindestens einmal pro Jahr getestet wird.                                                                                                                                                                                                                                                                                | 2     |
| AC.14.4 | Stellen Sie sicher, dass Build-Provenance- und AI-BOM-Aufzeichnungen im Rahmen der Incident Response verwendet werden, um jedes nachgelagerte Artefakt zu identifizieren, das unter dem verdächtigen AI-Agenten oder dem kompromittierten Pipeline-Lauf erzeugt wurde, damit die Maßnahmen Rückruf, Neubuild oder Quarantäne gezielt erfolgen können.                                                                                                                                                                                          | 2     |
| AC.14.5 | Überprüfen Sie, dass die automatisierte Behebung mindestens einmal pro Jahr in Tabletop- oder Live-Fire-Übungen getestet wird. Die Szenarien umfassen einen prompt-injizierten Prüfbots, eine Fork-PR-Secret-Exfiltration und eine von KI generierte bösartige Workflow-Datei.                                                                                                                                                                                                                                                                 | 3     |

Zuordnungen & Verweise:

* AC.14.1: ISO/IEC 27001:2022 A.5.24, A.5.26; NIST AI RMF MANAGE; OWASP SAMM Incident Management (IM).
* AC.14.2: OWASP ASVS v5 V6 (Kryptografie), V14; OWASP CI/CD Top 10 CICD-SEC-06; NIST SSDF RV.2.
* AC.14.3: AISVS C9.4 (Identity Handling für AI/LLM-Dienste); NIST SP 800-207 (Zero-Trust-Architektur); ISO/IEC 27001:2022 A.5.18 (Zugriffsrechte).
* AC.14.4: OWASP SCVS (Stücklistenanalyse); CycloneDX ML-BOM-Traceability; NIST SSDF RV.1.
* AC.14.5: NIST SSDF RV.1; ISO/IEC 27001:2022 A.5.28 (Sammlung von Nachweisen); OWASP SAMM Incident Management (IM).

---

## Referenzen

### NIST

* NIST Special Publication 800-218: Rahmenwerk für die sichere Entwicklung von Software (SSDF)
v1.1
* NIST Special Publication 800-218A: Sichere Praktiken für die Entwicklung von Software für
  Generative KI und Dual-Use-Foundation-Modelle
* NIST Special Publication 800-204D: Strategien zur Integration von Software
  Supply-Chain-Sicherheit in DevSecOps CI/CD-Pipelines
* NIST Special Publication 800-207: Zero-Trust-Architektur
* NIST Special Publication 800-53 Rev. 5: Sicherheits- und Datenschutzkontrollen für
  Informationssysteme und Organisationen
* NIST AI 100-1: Rahmenwerk für Risikomanagement im Bereich Künstliche Intelligenz (KI RMF 1.0)
* NIST AI 600-1: AI-RMF-Generative-AI-Profil

### OWASP

* OWASP Application Security Verification Standard (ASVS) v5
* OWASP Software Component Verification Standard (SCVS)
* OWASP Top 10 CI/CD Sicherheitsrisiken (10 Risiken): (1) CICD-SEC-01 Unzureichend
  Flow-Control-Mechanismen, (2) CICD-SEC-02 Unzureichende Identitäts- und Zugriffsverwaltung
  Management, (3) CICD-SEC-03 Missbrauch der Abhängigkeitskette, (4) CICD-SEC-04 Vergiftet
  Pipeline Execution, (5) CICD-SEC-05 Unzureichende PBAC (Pipeline-basierte Zugriffs
  (Controls), (6) CICD-SEC-06 Unzureichende Credential-Hygiene, (7) CICD-SEC-07
  Unsichere Systemeinstellungen, (8) CICD-SEC-08 Ungelenkte Nutzung von Drittanbietern
  Services, (9) CICD-SEC-09 Unzureichende Validierung der Integrität von Artefakten, (10)
  CICD-SEC-10 Unzureichendes Logging und fehlende Transparenz
* OWASP Top 10 for Large Language Model Applications (2025): LLM01 Prompt
  Injektion, LLM02 Offenlegung sensibler Informationen, LLM03 Lieferkette, LLM05
  Unangemessene Ausgabehandhabung, LLM06 Übermäßige Handlungsbefugnis, LLM10 Unbegrenzter Verbrauch
* OWASP Top 10 für agentische Anwendungen (2026): ASI01 Agenten-Zielentführung,
  ASI02 Tool-Missbrauch und Ausnutzung, ASI03 Identitäts- und Privilegienmissbrauch, ASI04
  Agentic Supply-Chain-Komprimittierung, ASI05 Unerwartete Codeausführung, ASI06 Speicher
  und Context Poisoning, ASI07 unsichere Inter-Agenten-Kommunikation, ASI08
  Kaskadierende Ausfälle, ASI09 Ausnutzung des Vertrauens zwischen Mensch und Agent, ASI10 Rogue Agents
* OWASP LLM Prompt Injection Prevention Spickzettel
* OWASP-Leitfaden für sichere Codierungspraktiken - Kurzübersicht
* OWASP Software Assurance Maturity Model (SAMM) v2

### Supply Chain & Herkunftsnachweis

* SLSA (Supply-chain Levels for Software Artifacts) v1.2, Build-Track und Source
  Track (aktuelle genehmigte Spezifikation)
* in-toto: Ein Framework für die Integrität der Software-Lieferkette
* Sigstore und cosign: Signierung und Überprüfung von Software-Artefakten
* CycloneDX Software Bill of Materials und CycloneDX ML-BOM (Machine Learning
  Stückliste)
* SPDX Software Package Data Exchange
* CISA-Software-Bauteilliste (SBOM)-Übersicht
* OpenSSF-Best-Practices-Badge, OpenSSF-Scorecard, OpenSSF-Allstar

### Adversarial AI & Threat Intelligence

* MITRE ATLAS: Adversarial Threat Landscape für Künstliche Intelligenz Systeme
* MITRE ATT&CK (Unternehmen), einschließlich T1195 Supply-Chain-Compromise und
  CI/CD-relevante Techniken

### ISO/IEC und CISA

* ISO/IEC 42001:2023: Anforderungen an ein Managementsystem für Künstliche Intelligenz
* ISO/IEC 27001:2022 und ISO/IEC 27002:2022: Informationssicherheits-Management
* ISO/IEC 5338:2023: Prozesse des Lebenszyklus künstlicher Intelligenz-Systeme
* CISA Secure-by-Design- und Secure-by-Default-Prinzipien

### Plattform-spezifische Härtungsrichtlinien

* GitHub Security Lab: "Schützen Sie Ihre GitHub Actions und Workflows:
  „Verhindern von pwn-Anfragen“ (Teile 1-4, einschließlich Alvaro Munoz, 2025), der
  kanonische Referenz zu Fork-PR-Trigger-Ausnutzungsmustern, umgangssprachlich
  bekannt als "pwn-Anfragen"
* GitHub-Dokumentation: Security-Härtung für GitHub Actions; Workflow-Ausführungen genehmigen
  aus öffentlichen Forks; Automatische Token-Authentifizierung und -Berechtigungen; Branch
  Schutzregeln und Regelsätze
* GitLab-Dokumentation: CI/CD-Sicherheitsbest-Practices; Geschützte Variablen und
  Umgebungen
* Äquivalente Anbieterempfehlungen für Jenkins, Argo Workflows, Tekton, CircleCI und
  Azure DevOps Pipelines

