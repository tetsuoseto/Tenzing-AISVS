# Anhang A: Glossar

Dieses umfassende Glossar bietet Definitionen wichtiger KI-, ML- und Sicherheitsbegriffe, die im AISVS verwendet werden, um Klarheit und ein gemeinsames Verständnis sicherzustellen.

* Adapter – ein leichtgewichtiges Modul (z.B. LoRA, QLoRA), das zu einem vortrainierten Modell hinzugefügt wird, um sein Verhalten für eine bestimmte Aufgabe zu spezialisieren, ohne die ursprünglichen Gewichte zu verändern.

* Adversarial Example – Eine Eingabe, die gezielt erstellt wurde, um ein KI-Modell dazu zu bringen, einen Fehler zu machen, oft durch das Hinzufügen subtiler Perturbationen, die für Menschen unbemerkt sind.

* Adversarial Robustness – die Fähigkeit eines Modells, seine Leistung aufrechtzuerhalten und sich dagegen zu wehren, von absichtlich konstruierten, bösartigen Eingaben getäuscht oder manipuliert zu werden, die darauf ausgelegt sind, Fehler zu verursachen.

* Adversarial Training – Eine Trainingsmethode, die Trainingsdaten durch adversariale Beispiele ergänzt, um die Robustheit des Modells gegen Störangriffen zu verbessern.

* Agent – Ein KI-Software-System, das Schlussfolgerungen, Planung und Speicher nutzt, um Ziele zu verfolgen und Aufgaben im Auftrag von Nutzern zu erledigen, mit einem Maß an Autonomie, um Entscheidungen zu treffen, zu lernen und sich anzupassen. Wird auch als Agentic AI bezeichnet.

* KI-BOM (KI-Bill of Materials) – Ein strukturierter Datensatz aller Komponenten in einem KI-System, einschließlich Modellen, Datensätzen, Gewichten, Hyperparametern, Frameworks und Lizenzen. Kann SPDX- oder CycloneDX-Formate verwenden. Unterscheidet sich von einer herkömmlichen SBOM dadurch, dass sie modellbezogene Artefakte über Software-Abhängigkeiten hinaus abdeckt.

* AppArmor – ein Linux-Kernel-Sicherheitsmodul, das Programmfähigkeiten über pro-Programm-Sicherheitsprofile einschränkt und zum Sandboxing von KI-Workloads verwendet wird.

* Aufmerksamkeitskarte – eine Visualisierung, welche Teile einer Eingabe ein Transformer-Modell bei der Erzeugung eines Outputs berücksichtigt, verwendet als Werkzeug für Interpretierbarkeit.

* Attributbasierte Zugriffskontrolle (ABAC) – Ein Zugriffskontrollparadigma, bei dem Autorisierungsentscheidungen auf Attributen des Benutzers, der Ressource, der Aktion und der Umgebung beruhen und zur Abfragezeit ausgewertet werden.

* Backdoor-Angriff – Eine Art von Data-Poisoning-Angriff, bei dem das Modell darauf trainiert wird, auf bestimmte Trigger in einer bestimmten Weise zu reagieren, während es sich ansonsten normal verhält.

* Bias – Systematische Fehler in den Ausgaben von KI-Modellen, die zu unfairen oder diskriminierenden Ergebnissen für bestimmte Gruppen oder in bestimmten Kontexten führen können.

* Bias-Ausnutzung – Eine Angriffstechnik, die bekannte Verzerrungen (Biases) in KI-Modellen ausnutzt, um Ausgaben oder Ergebnisse zu manipulieren.

* Blue-Green-Deployment – Eine Deployment-Strategie, die zwei identische Produktionsumgebungen (Blue und Green) betreibt und so einen sofortigen Rollback ermöglicht, indem der Datenverkehr zwischen ihnen umgeschaltet wird.

* Byzantinische Fehlertoleranz – die Fähigkeit eines verteilten Systems, Konsens zu erzielen und auch dann korrekt weiter zu funktionieren, wenn einige Knoten ausfallen oder böswillig handeln.

* Canary-Deployment – Eine Bereitstellungsstrategie, bei der schrittweise ein kleiner Prozentsatz des Datenverkehrs an eine neue Modellversion weitergeleitet wird, um Probleme zu erkennen, bevor die vollständige Einführung erfolgt.

* Cedar – eine Open-Source-Richtlinien- und Bewertungs-Engine für präzise Berechtigungen, ursprünglich von Amazon entwickelt. Wird zur Implementierung von ABAC für KI-Systeme verwendet.

* Zertifizierte Robustheit - eine formale mathematische Garantie, dass sich die Vorhersage eines Modells innerhalb einer vorgegebenen Störgrenzen-Umgebung um eine Eingabe nicht ändert, verifiziert durch Techniken wie die Intervall-Grenzen-Propagation.

* Chain of Thought – eine Technik zur Verbesserung des Denkens in Sprachmodellen, indem Zwischendenkschritte erzeugt werden, bevor eine endgültige Antwort ausgegeben wird.

* CI/CD (Continuous Integration / Continuous Deployment) – Eine Software-Engineering-Praxis, die das automatische Erstellen, Testen und Bereitstellen von Code-Änderungen steuert und in KI-Systemen für die Bereitstellung von Modellen und Pipelines verwendet wird.

* Schutzschalter – Ein Mechanismus, der den Betrieb eines KI-Systems automatisch stoppt, wenn bestimmte Risikoschwellen überschritten werden, wie z.B. außer Kontrolle geratene Agent-Schleifen oder Budgeterschöpfung.

* CMP (Consent Management Platform) – Ein System, das Benutzer-Zustimmungseinstellungen verfolgt, einschließlich Opt-in-Status, Zweck und Aufbewahrungszeitraum, und die Durchsetzung von Zustimmungentscheidungen über Datenverarbeitungs-Pipelines hinweg sicherstellt.

* Konzeptdrift – eine Änderung der statistischen Beziehung zwischen Modelleingaben und -ausgaben über die Zeit, wodurch Modellvorhersagen weniger genau werden, auch wenn die Eingabeverteilungen stabil bleiben.

* Confidential Computing – ein Sicherheitsparadigma, das Daten während der Verarbeitung schützt, indem Berechnungen in hardwaregestützten vertrauenswürdigen Ausführungsumgebungen durchgeführt werden und sichergestellt wird, dass Code und Daten verschlüsselt und vom Host isoliert bleiben.

* Vertrauliche Inferenz – Ein Inferenzdienst, der AI-Modelle innerhalb einer vertrauenswürdigen Ausführungsumgebung (TEE) ausführt und sicherstellt, dass Modellgewichte und Inferenzdaten verschlüsselt, versiegelt und vor unbefugtem Zugriff oder Manipulation geschützt bleiben.

* Gegenfaktische Erklärung – Eine Interpretierbarkeits-Technik, die eine Modellentscheidung erklärt, indem sie die minimalen Änderungen an den Eingabemerkmalen beschreibt, die das Vorhersageergebnis ändern würden.

* Covert Channel – ein unbeabsichtigter Kommunikationspfad, der ausgenutzt werden kann, um Informationen unter Verstoß gegen die Sicherheitsrichtlinie zu übertragen, z.B. durch Zeitverhalten- oder Ressourcen-Nutzungsmuster in gemeinsam genutzter KI-Infrastruktur.

* CycloneDX – Ein offener Standard für Software- und KI-Bill-of-Materials, der die Erfassung von Komponentenbeständen, das Tracking von Schwachstellen und die Einhaltung von Lizenzen unterstützt.

* DAG (gerichteter azyklischer Graph) – eine Graphstruktur mit gerichteten Kanten und ohne Zyklen, die in KI-Systemen verwendet wird, um Agenten-Entscheidungspfade, Schlussfolgerungsspuren und Workflow-Abhängigkeiten darzustellen.

* Datenaugmentation – Eine Technik, die modifizierte Kopien der Trainingsdaten erstellt (z. B. durch Rotation, Rauschen oder Paraphrasierung), um die Vielfalt des Datensatzes zu erhöhen und die Robustheit des Modells zu verbessern.

* Data Drift – eine Veränderung der statistischen Verteilung der Modell-Eingabedaten im Zeitverlauf im Vergleich zu den Daten, auf denen das Modell trainiert wurde, die potenziell die Qualität von Vorhersagen verschlechtern kann.

* Datenleckage – Unbeabsichtigte Offenlegung sensibler Informationen durch AI-Modellausgaben oder -verhalten.

* Datenvergiftung – die gezielte Manipulation von Trainingsdaten, um die Integrität des Modells zu beeinträchtigen, häufig um Hintertüren zu installieren oder die Leistung zu verschlechtern.

* Defense-in-Depth – Eine Sicherheitsstrategie, die mehrere unabhängige Schutzmaßnahmen in Schichten kombiniert, sodass, wenn eine Schutzebene ausfällt, die anderen weiterhin Schutz bieten.

* Defensive Distillation – Eine Trainingsmethode, bei der ein Modell anhand der weichen Wahrscheinlichkeitsausgaben eines anderen Modells trainiert wird, um Entscheidungsgrenzen zu glätten und die Anfälligkeit gegenüber adversarialen Störungen zu reduzieren.

* Differential Privacy – Ein mathematisch rigoroser Rahmen zum Veröffentlichen statistischer Informationen über Datensätze unter gleichzeitiger Wahrung der Privatsphäre einzelner Datensubjekte, quantifiziert durch ein Privacy-Budget von epsilon (ε).

* DoS (Denial of Service) – Ein Angriff, der versucht, ein System unzugänglich zu machen, indem es mit Anfragen überflutet oder seine Ressourcen erschöpft werden.

* DPIA (Datenschutz-Folgenabschätzung) – Eine formale Bewertung, die gemäß Vorschriften wie der DSGVO erforderlich ist, um Risiken für personenbezogene Daten zu bewerten und zu mindern, bevor die Verarbeitung beginnt.

* DP-SGD (Differenziell Private Stochastic Gradient Descent) – Ein Trainingsalgorithmus, der kalibriertes Rauschen zu Gradientenaktualisierungen während des Modelltrainings hinzufügt, um formale Garantien für differenzielle Privatsphäre bereitzustellen.

* DRTM (Dynamic Root of Trust for Measurement) – ein Hardware-Mechanismus, der zur Laufzeit einen vertrauenswürdigen Ausführungseinstiegspunkt herstellt und damit die Integritätsprüfung von KI-Beschleuniger-Workloads ermöglicht.

* Einbettungen – Dichte Vektor-Darstellungen von Daten (Text, Bilder usw.), die in einem hochdimensionalen Raum semantische Bedeutung erfassen.

* Erklärbarkeit – Die Fähigkeit eines KI-Systems, mithilfe von Techniken wie SHAP, LIME, Aufmerksamkeitskarten (attention maps) und Gegenfaktoren-Erklärungen (counterfactual explanations) menschlich verständliche Gründe für seine Entscheidungen und Vorhersagen bereitzustellen. Wird auch als Explainable AI (XAI) bezeichnet.

* Feature-Attribution – Eine Interpretierbarkeitsmethode, die Wichtigkeitsscores einzelnen Eingabemerkmalen zuweist und ihre Beiträge zu einer bestimmten Modellvorhersage angibt.

* Federated Learning – ein maschinelles Lernverfahren, bei dem Modelle über mehrere dezentrale Geräte hinweg trainiert werden, die lokale Datensamples besitzen, ohne dass die Daten selbst ausgetauscht werden.

* Feinabstimmung – der Prozess, bei dem ein vortrainiertes Modell auf einem kleineren, aufgabenbezogenen Datensatz weiter trainiert wird, um es für einen bestimmten Anwendungsfall anzupassen.

* FIPS 140-3 – ein US-Regierungsstandard, der Sicherheitsanforderungen für kryptografische Module definiert, wobei Level 3 einen physikalischen Manipulationsschutz und eine identitätsbasierte Authentifizierung erfordert.

* Schutzvorrichtungen - Einschränkungen, die implementiert wurden, um zu verhindern, dass KI-Systeme schädliche, voreingenommene oder anderweitig unerwünschte Ausgaben erzeugen.

* Halluzination – Ein Phänomen, bei dem ein KI-Modell falsche oder irreführende Informationen erzeugt, die nicht durch seine Trainingsdaten, den abgerufenen Kontext oder die tatsächliche Realität gestützt sind.

* Homoglyph – ein Zeichen, das visuell einem anderen Zeichen aus einem anderen Schriftsystem oder einer anderen Kodierung ähnelt (z.B. kyrillisches „а“ vs. lateinisches „a“), das in Angriffen ausgenutzt wird, um eine textbasierte Eingabevalidierung zu umgehen.

* HSM (Hardware-Sicherheitsmodul) – Ein dediziertes physisches Gerät, das kryptografische Schlüssel in einer manipulationssicheren Umgebung verwaltet, verarbeitet und speichert.

* Human-in-the-Loop (HITL) – Systeme, die so konzipiert sind, dass sie in entscheidenden Entscheidungspunkten eine menschliche Aufsicht, Verifizierung oder Intervention erfordern.

* Infrastructure as Code (IaC) – Verwaltung und Bereitstellung von Infrastruktur per Code statt manueller Prozesse, wodurch Sicherheits-Scans und konsistente Deployments ermöglicht werden.

* Intervall-Propagationsmethode (Interval-Bound Propagation) – Eine formale Verifikationstechnik, die Schranken durch neuronale Netzwerk-Schichten propagiert, um zu bescheinigen, dass Modellvorhersagen robust sind innerhalb festgelegter Bereiche für Eingabeperturbationen.

* Jailbreak – Techniken zur Umgehung von Sicherheits-Schutzmaßnahmen in KI-Systemen, insbesondere in großen Sprachmodellen, um verbotene Inhalte zu erzeugen.

* JWT (JSON Web Token) – Ein kompaktes, eigenständiges Token-Format zum sicheren Übertragen von Identitäts- und Autorisierungs-Claims zwischen Parteien, signiert, um die Integrität sicherzustellen.

* k-Anonymität – Eine Datenschutz-Eigenschaft, bei der jeder Datensatz in einem Datensatz hinsichtlich bestimmter identifizierender Attribute von mindestens k-1 anderen Datensätzen nicht unterscheidbar ist.

* KMS (Key Management Service) – Ein verwalteter Dienst zum Erstellen, Speichern, Rotieren und Verwalten des Zugriffs auf kryptografische Schlüssel, die zum Schutz von Daten und Artefakten verwendet werden.

* l-Diversität – eine Datenschutz-Eigenschaft, die k-Anonymität erweitert und erfordert, dass jede Äquivalenzklasse mindestens l unterschiedliche Werte für sensible Attribute enthält, um Attribut-Offenlegung zu verhindern.

* Least Privilege – Das Sicherheitsprinzip, das nur die minimal erforderlichen Zugriffrechte für Benutzer und Prozesse gewährt.

* LIME (Local Interpretable Model-agnostic Explanations) – eine Methode, um die Vorhersagen eines beliebigen Machine-Learning-Klassifizierers zu erklären, indem er lokal durch ein interpretierbares Modell angenähert wird.

* Verknüpfungsangriff – Ein Angriff, der quasi-identifizierende Merkmale über mehrere Datensätze kombiniert, um Personen erneut zu identifizieren, deren Daten angeblich anonymisiert wurden.

* Maschinelles Unlearning – Techniken, um den Einfluss bestimmter Trainingsdaten aus einem trainierten Modell zu entfernen und Löschanfragen von betroffenen Datenobjekten sowie die Einhaltung regulatorischer Anforderungen zu unterstützen.

* MCP (Model Context Protocol) – Ein Protokoll, das es KI-Modellen und Agenten ermöglicht, auf externe Tools, Datenquellen und Ressourcen zuzugreifen, indem strukturierte, typisierte Anfragen und Antworten über einen definierten Transport ausgetauscht werden.

* Membership Inference Attack – Ein Angriff, der darauf abzielt, festzustellen, ob ein bestimmter Datenpunkt für das Training eines Machine-Learning-Modells verwendet wurde.

* MIG (Multi-Instance GPU) – eine NVIDIA-Technologie, die eine einzelne GPU in mehrere isolierte Instanzen aufteilt, wobei jede Instanz über dedizierten Speicher und Rechenressourcen für sichere Multi-Tenant-Workloads verfügt.

* MITRE ATLAS – Adversarial Threat Landscape für Künstliche-Intelligenz-Systeme; eine Wissensdatenbank mit adversarialen Taktiken und Techniken gegen Künstliche-Intelligenz-Systeme.

* Model Card – Ein Dokument, das standardisierte Informationen über die Leistung, Einschränkungen, vorgesehenen Verwendungen und ethischen Überlegungen eines KI-Modells bereitstellt, um Transparenz und eine verantwortungsvolle KI-Entwicklung zu fördern.

* Modell-Extraktion – Ein Angriff, bei dem ein Gegner wiederholt ein Zielmodell abfragt, um eine funktional ähnliche Kopie ohne Autorisierung zu erstellen. Wird auch als Modellstehlen oder Modellraub bezeichnet.

* Modellinversion – ein Angriff, der versucht, Trainingsdaten zu rekonstruieren, indem er Modellausgaben analysiert.

* Model-Lifecycle-Management – Der Prozess der Überwachung aller Phasen der Existenz eines KI-Modells, einschließlich Design, Entwicklung, Bereitstellung, Monitoring, Wartung und der eventualen Außerbetriebnahme.

* Modellvergiftung – Das Einführen von Schwachstellen oder Hintertüren direkt in ein Modell während des Trainingsprozesses.

* mTLS (gegenseitiges TLS) – Eine TLS-Konfiguration, bei der sich sowohl Client als auch Server gegenseitig mithilfe von Zertifikaten authentifizieren und so eine bidirektionale Identitätsprüfung für die Kommunikation von Dienst zu Dienst sicherstellen.

* Multi-Agenten-System – Ein System, das aus mehreren miteinander interagierenden KI-Agenten besteht, wobei jeder Agent möglicherweise über unterschiedliche Fähigkeiten und Ziele verfügt.

* NFC (Normalform zusammengesetzt) – Eine Unicode-Normalisierungsform, die Zeichen dekomponiert und dann zu einer kanonischen Darstellung wieder zusammensetzt, um Umgehungsangriffe auf Basis von Codierungen zu verhindern.

* NVLink – Eine Hochbandbreiten-Interconnect-Technologie für die GPU-zu-GPU-Kommunikation, die in Multi-Tenant-AI-Umgebungen eine Authentifizierung und Verschlüsselung erfordert.

* OAuth 2.1 – Ein Autorisierungs-Framework, das OAuth 2.0 Best Practices in einer einzigen Spezifikation zusammenführt und in AISVS als erforderlicher Authentifizierungsmechanismus für MCP-Clients und -Server verwendet wird.

* OIDC (OpenID Connect) – eine Identitätsebene, die auf OAuth 2.0 basiert und Clients ermöglicht, die Benutzeridentität anhand der Authentifizierung zu verifizieren, die von einem Autorisierungsserver durchgeführt wurde.

* OPA (Open Policy Agent) – Eine Open-Source, allgemeine Policy-Engine, die Autorisierungs- und Admission-Control-Richtlinien auswertet, die in Rego geschrieben sind, und eine einheitliche Policy-Durchsetzung über Anwendungen, APIs und Infrastruktur hinweg ermöglicht.

* PII (personenbezogene Daten) – alle Informationen, die verwendet werden können, um eine bestimmte Person zu identifizieren, zu kontaktieren oder ihren Aufenthaltsort zu bestimmen, entweder allein oder in Kombination mit anderen Daten.

* Policy-as-Code – die Praxis, Sicherheits- und Compliance-Richtlinien in maschinenlesbarem Code zu definieren, der versionierbar, testbar und automatisch in CI/CD-Pipelines durchsetzbar ist.

* Datenschutzfreundliches Machine Learning (PPML) – Techniken und Methoden, um ML-Modelle zu trainieren und bereitzustellen und dabei die Privatsphäre der Trainingsdaten zu schützen.

* Prompt-Injection – Ein Angriff, bei dem schädliche Anweisungen in Eingaben eingebettet werden, um das beabsichtigte Verhalten eines Modells zu überschreiben.

* RAG (Retrieval-Augmented Generation) – Eine Technik, die große Sprachmodelle verbessert, indem vor der Generierung einer Antwort relevante Informationen aus externen Wissensquellen abgerufen werden.

* RBAC (rollenbasierte Zugriffskontrolle) – Ein Zugriffskontrollmodell, bei dem Berechtigungen Rollen zugewiesen werden, anstatt einzelnen Benutzern, und Benutzer Zugriff erhalten, indem sie den entsprechenden Rollen zugewiesen werden.

* Red-Teaming – Die Praxis, aktiv KI-Systeme zu testen, indem man Angriffe durch simulierte Angreiferstrategien nachbildet, um Schwachstellen zu identifizieren.

* Re-Identifikationsrisiko – Die Wahrscheinlichkeit, dass eine Person anhand eines angeblich anonymisierten Datensatzes identifiziert werden kann, gemessen anhand festgelegter Schwellenwerte.

* Remote-Atestation – Ein Mechanismus, bei dem eine vertrauenswürdige Ausführungsumgebung kryptografischen Nachweis gegenüber einer entfernten Partei liefert, dass spezifischer Code in einer echten, nicht veränderten TEE ausgeführt wird.

* RLHF (Reinforcement Learning from Human Feedback) – Eine Trainingsmethode, bei der ein Modell mit menschlichen Präferenzurteilen als Belohnungssignal feinjustiert wird, um die Ausrichtung an menschlichen Werten und Sicherheitsanforderungen zu verbessern.

* SAML (Security Assertion Markup Language) – Ein XML-basiertes Standardformat zum Austausch von Authentifizierungs- und Autorisierungsdaten zwischen Identitätsanbietern und Dienstanbietern.

* SBOM (Software Bill of Materials) – Ein formaler Datensatz, der die Details und Lieferketten-Beziehungen der Softwarekomponenten enthält, die zum Aufbau einer Anwendung verwendet werden. Siehe auch AI BOM für modell-spezifische Artefakte.

* Secure Boot - Eine Firmware-Sicherheitsfunktion, die die kryptografische Signatur jeder Komponente in der Boot-Kette vor der Ausführung überprüft und dadurch das Laden nicht autorisierter oder manipulierten Software verhindert.

* Sichere Multi-Party-Berechnung (SMPC) – eine kryptografische Technik, die es mehreren Parteien ermöglicht, gemeinsam eine Funktion über ihren privaten Eingaben zu berechnen, ohne diese Eingaben einander offenzulegen.

* seccomp (Secure Computing Mode) – Eine Linux-Kernel-Funktion, die die zulässigen Systemaufrufe eines Prozesses einschränkt, eingesetzt um KI-Workloads zu sandboxen und die Angriffsfläche zu verringern.

* SELinux (Security-Enhanced Linux) – ein Linux-Kernel-Sicherheitsmodul, das obligatorische Zugriffskontrollen mithilfe von Sicherheitsrichtlinien bereitstellt und zur Durchsetzung einer fein abgestuften Prozessisolierung für KI-Workloads verwendet wird.

* Schattenmodell – Ein von einem Angreifer trainiertes Modell, das das Verhalten eines Zielmodells nachahmen soll. Es wird in Membership-Inference-Angriffen eingesetzt und dient als Grundlage zur Bewertung der Wirksamkeit des maschinellen Vergessens.

* SHAP (SHapley Additive exPlanations) – Ein spieltheoretischer Ansatz zur Erklärung der Ausgabe jedes Machine-Learning-Modells, indem die Beiträge jedes Merkmals zur Vorhersage berechnet werden.

* Seitenkanalangriff – Ein Angriff, der Informationen aus einem System durch indirekte Beobachtung physikalischer Eigenschaften wie Timing, Stromverbrauch, elektromagnetische Emissionen oder Cache-Verhalten extrahiert, statt Schwachstellen in Software auszunutzen.

* SIEM (Security Information and Event Management) – Eine Plattform, die Sicherheitsereignisdaten aus mehreren Quellen aggregiert, korreliert und analysiert, um Bedrohungen zu erkennen, Incident Response zu unterstützen und Compliance-Anforderungen zu erfüllen.

* SPDX (Software Package Data Exchange) – Ein offener Standard für die Kommunikation von Informationen zu Software- und AI-Komponenten-Bauteillisten, einschließlich Herkunft der Komponenten, Lizenzierung und Sicherheitsreferenzen.

* SSE (Server-Sent Events) – Eine Web-Technologie, die es einem Server ermöglicht, in Echtzeit-Updates an einen Client über eine HTTP-Verbindung zu übertragen, und die als Transportmechanismus in MCP verwendet wird.

* Steganografie – die Praxis, Daten in anderen Medien (Bildern, Audio, Video) zu verstecken, sodass dies für Beobachter nicht erkennbar ist. Wird als Angriffsmittel genutzt, um Payloads an Content-Filter vorbei zu schmuggeln.

* stdio (Standard Input/Output) – Ein Prozess-Kommunikationsmechanismus mit standardisierten Eingabe-, Ausgabe- und Fehler-Streams, der in MCP als lokaler Nur-Transport verwendet wird und auf die Kommunikation innerhalb eines einzelnen Prozesses auf demselben Rechner beschränkt ist.

* Starke Authentifizierung – Authentifizierung, die sich gegen das Ausspähen von Zugangsdaten und Replay-Angriffe wehrt, indem mindestens zwei Faktoren (Wissen, Besitz, Inhärenz) sowie phishingresistente Mechanismen wie FIDO2/WebAuthn, zustellungsbasierte Dienstauthentifizierung mit Zertifikaten oder kurzlebige Tokens erforderlich sind.

* Supply-Chain-Angriff – Kompromittierung eines Systems durch das gezielte Angreifen weniger sicherer Elemente in seiner Lieferkette, wie z. B. Drittanbieter-Bibliotheken, Datensätze oder vortrainierte Modelle.

* Synthetische Daten – künstlich erzeugte Daten, die die statistischen Eigenschaften echter Daten bewahren, aber keine tatsächlichen einzelnen Datensätze enthalten; sie werden verwendet, um den Datenschutz während des Modelltrainings und -tests zu schützen.

* TEE (Trusted Execution Environment) – eine hardwareisolierte Verarbeitungumgebung, die Vertraulichkeit und Integritätsgarantien für Code und Daten bereitstellt und diese vor dem Host-Betriebssystem und anderen Mandanten schützt.

* Temperaturskalierung – Eine Post-hoc-Kalibrierungstechnik, die die Konfidenzwerte der Modellausgaben so anpasst, dass sie die wahren Vorhersagewahrscheinlichkeiten genauer widerspiegeln.

* TLS (Transport Layer Security) – Ein kryptografisches Protokoll, das Ende-zu-Ende-Verschlüsselung, Authentifizierung und Integrität für Daten bereitstellt, die über ein Netzwerk übertragen werden. AISVS erfordert TLS 1.3 oder höher.

* Tokenizer – Eine Komponente, die Rohtext in eine Sequenz von Tokens (Subwords, Wörter oder Zeichen) umwandelt, die ein Sprachmodell als Eingabe verarbeiten kann.

* TPM (Trusted Platform Module) – Ein dedizierter Hardware-Chip, der kryptografische Funktionen bereitstellt, einschließlich sicherer Schlüsselgenerierung, -speicherung und Messung der Plattformintegrität.

* Transfer Learning – Eine Technik, bei der ein für eine Aufgabe entwickeltes Modell als Ausgangspunkt für ein Modell für eine zweite Aufgabe wiederverwendet wird.

* Vektor-Datenbank – Eine spezialisierte Datenbank, die entwickelt wurde, um hochdimensionale Vektoren (Embeddings) zu speichern und effiziente Ähnlichkeitssuchen durchzuführen.

* VRAM (Video Random Access Memory) – Speicher auf einer GPU zum Speichern von Modellgewichten, Aktivierungen und Zwischenauswertungen während der AI-Inferenz und des Trainings, der zwischen Mandanten-Workloads zurückgesetzt werden muss.

* Sicherheitslücken-Scannen – Automatisierte Tools, die bekannte Sicherheitslücken in Softwarekomponenten identifizieren, einschließlich KI-Frameworks und Abhängigkeiten.

* WASM (WebAssembly) – Ein portables Binär-Anweisungsformat, das die isolierte Ausführung von Code ermöglicht und als Isolationsmechanismus für KI-Tools und Plugins verwendet wird.

* Wasserzeichen – Techniken zum Einbetten unauffälliger Marker in KI-generierten Inhalten oder Modellgewichten, um die Herkunft nachzuverfolgen, nicht autorisierte Kopien zu erkennen oder KI-generierte Medien zu identifizieren.

* WORM (Write-Once-Read-Many) – eine Speichertechnologie, die die Änderung oder Löschung von Daten verhindert, nachdem sie geschrieben wurden, eingesetzt für manipulationssichere Audit-Logs und Backup-Schutz.

* Zero-Day-Schwachstelle – eine zuvor unbekannte Schwachstelle, die Angreifer ausnutzen können, bevor Entwickler einen Patch erstellen und bereitstellen.

* Zero-Trust – Ein Sicherheitsmodell, das keine implizite Vertrauenswürdigkeit für irgendeinen Benutzer, ein Gerät oder ein Netzwerk annimmt und eine kontinuierliche Verifizierung der Identität und Autorisierung für jede Zugriffsanfrage erfordert.

