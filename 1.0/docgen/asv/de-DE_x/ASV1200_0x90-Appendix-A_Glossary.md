# Anhang A: Glossar

Dieses umfassende Glossar bietet Definitionen wichtiger KI-, ML- und Sicherheitsbegriffe, die im Verlauf der AISVS verwendet werden, um Klarheit und ein gemeinsames Verständnis sicherzustellen.

* Adapter – Ein leichtgewichtiges Modul (z. B. LoRA, QLoRA), das zu einem vortrainierten Modell hinzugefügt wird, um sein Verhalten auf eine spezifische Aufgabe zu spezialisieren, ohne die ursprünglichen Gewichte zu verändern.

* Beispiel für ein adversarialer Angriff – Eine Eingabe, die absichtlich so gestaltet wurde, dass ein KI-Modell einen Fehler macht, oft durch das Hinzufügen subtiler Perturbationen, die für Menschen nicht wahrnehmbar sind.

* Adversarial Robustheit – die Fähigkeit eines Modells, seine Leistung beizubehalten und sich gegen das Vortäuschen oder Manipulieren durch absichtlich konstruierte, bösartige Eingaben zu wehren, die darauf abzielen, Fehler zu verursachen.

* Adversarial Training – Eine Trainingsmethode, die Trainingsdaten durch adversariale Beispiele erweitert, um die Robustheit des Modells gegen Perturbationsangriffe zu verbessern.

* Agent – Ein KI-Software-System, das auf Schlussfolgern, Planen und Speichern setzt, um Ziele zu verfolgen und Aufgaben im Auftrag von Nutzern zu erledigen, mit einem gewissen Maß an Autonomie, um Entscheidungen zu treffen, zu lernen und sich anzupassen. Wird auch als Agentic AI bezeichnet.

* KI-BOM (KI-Bill of Materials) – ein strukturierter Datensatz aller Komponenten in einem KI-System, einschließlich Modelle, Datensätze, Gewichte, Hyperparameter, Frameworks und Lizenzen. Kann den Formaten SPDX oder CycloneDX folgen. Unterscheidet sich von einem herkömmlichen SBOM dadurch, dass es model-spezifische Artefakte über Software-Abhängigkeiten hinaus abdeckt. Wird außerdem als AIBOM oder MBOM (Model Bill of Materials) bezeichnet.

* AppArmor – Ein Linux-Kernel-Sicherheitsmodul, das Programmfähigkeiten durch pro Programm definierte Sicherheitsprofile einschränkt und zur Isolierung (Sandboxing) von AI-Workloads verwendet wird.

* Aufmerksamkeitskarte – Eine Visualisierung, auf welche Teile einer Eingabe ein Transformer-Modell achtet, wenn es eine Ausgabe erzeugt; verwendet als Werkzeug für Interpretierbarkeit.

* Attributbasierte Zugriffskontrolle (ABAC) – Ein Zugriffssteuerungsparadigma, bei dem Autorisierungsentscheidungen auf Attributen des Benutzers, der Ressource, der Aktion und der Umgebung basieren und zur Abfragezeit ausgewertet werden.

* Backdoor-Angriff – Eine Art von Data-Poisoning-Angriff, bei dem das Modell darauf trainiert wird, auf bestimmte Trigger in einer spezifischen Weise zu reagieren, während es ansonsten normal funktioniert.

* Voreingenommenheit – Systematische Fehler in den Ausgaben von KI-Modellen, die zu unfairen oder diskriminierenden Ergebnissen für bestimmte Gruppen oder in bestimmten Kontexten führen können.

* Bias-Exploitation – Eine Angriffstechnik, die bekannte Verzerrungen in KI-Modellen ausnutzt, um Ausgaben oder Ergebnisse zu manipulieren.

* Blue-Green-Deployment – Eine Bereitstellungsstrategie, die zwei identische Produktionsumgebungen (Blue und Green) ausführt und dadurch einen sofortigen Rollback ermöglicht, indem der Datenverkehr zwischen ihnen umgeschaltet wird.

* Byzantinische Fehlertoleranz – Die Fähigkeit eines verteilten Systems, einen Konsens zu erreichen und den korrekten Betrieb fortzusetzen, auch wenn einige Knoten ausfallen oder sich böswillig verhalten.

* Canary Deployment – Eine Bereitstellungsstrategie, bei der schrittweise ein kleiner Prozentsatz des Traffics an eine neue Modellversion weitergeleitet wird, um Probleme zu erkennen, bevor die vollständige Einführung erfolgt.

* Cedar – Eine Open-Source-Policy-Sprache und ein Evaluations-Engine für feingranulare Berechtigungen, ursprünglich von Amazon erstellt. Wird bei der Implementierung von ABAC für KI-Systeme verwendet.

* Zertifizierte Robustheit – eine formale mathematische Zusicherung, dass sich die Vorhersage eines Modells innerhalb einer vorgegebenen Störungsgrenze um eine Eingabe nicht ändert, verifiziert durch Techniken wie Intervall-Grenzen-Propagation.

* Ketten-Thought – eine Technik zur Verbesserung des Denkens in Sprachmodellen, indem zwischengeschaltete Gedankenschritte generiert werden, bevor eine endgültige Antwort ausgegeben wird.

* CI/CD (Continuous Integration / Continuous Deployment) – Eine Software-Engineering-Praxis, die den automatisierten Build, das Testen und das Bereitstellen von Code-Änderungen steuert, eingesetzt in KI-Systemen für die Bereitstellung von Modellen und Pipelines.

* Leistungsschalter – Ein Mechanismus, der die Systemoperationen eines KI-Systems automatisch stoppt, wenn bestimmte Risikoschwellen überschritten werden, z. B. bei Endlosschleifen von Agenten oder einer Erschöpfung des Budgets.

* CMP (Consent Management Platform) – Ein System, das die Einwilligungseinstellungen der Nutzer verfolgt, einschließlich Opt-in-Status, Zweck und Aufbewahrungsfrist, und Einwilligungsentscheidungen über Data-Processing-Pipelines hinweg durchsetzt.

* Concept Drift – eine Veränderung der statistischen Beziehung zwischen Modell-Eingaben und -Ausgaben über die Zeit, wodurch Modellvorhersagen weniger genau werden können, auch wenn die Eingabeverteilungen stabil bleiben.

* Confidential Computing – ein Sicherheitsparadigma, das Daten bei der Nutzung schützt, indem die Berechnung innerhalb von durch Hardware erzwungenen vertrauenswürdigen Ausführungsumgebungen erfolgt und sichergestellt wird, dass Code und Daten verschlüsselt bleiben und vom Host isoliert sind.

* Vertrauliche Inferenz – ein Inferenzdienst, der KI-Modelle in einer sicheren Ausführungsumgebung (TEE) ausführt und sicherstellt, dass Modellgewichte und Inferenzdaten verschlüsselt, versiegelt und vor unbefugtem Zugriff oder Manipulation geschützt bleiben.

* Verfassungs-KI – ein Trainingsansatz, bei dem ein Modell durch eine Reihe schriftlicher Prinzipien (eine „Verfassung“) geleitet wird und darauf trainiert wird, seine eigenen Ausgaben zu kritisieren und zu überarbeiten, um die Richtlinienkonformität sicherzustellen, wobei ein Selbstkritikprozess als Alternative oder Ergänzung zu menschlichem Feedback verwendet wird. Siehe auch: RLHF.

* Kontextfenster – Die maximale Menge an Text (gemessen in Tokens), die ein Sprachmodell in einem einzelnen Inferenzaufruf verarbeiten kann, einschließlich Systemprompt, Verlauf der Unterhaltung, abgerufener Dokumente und Tool-Ausgaben. Das Kontextfenster definiert, welche Informationen dem Modell zur Inferenzzeit zur Verfügung stehen, und ist eine endliche Ressource, die erschöpft oder durch prägende (adversariale) Eingaben manipuliert werden kann.

* Gegenfaktische Erklärung – Eine Interpretierbarkeits-Technik, die eine Modellentscheidung erklärt, indem sie die minimalen Änderungen an den Eingabe-Features beschreibt, die die Vorhersage ändern würden.

* Covert Channel – Ein unbeabsichtigter Kommunikationspfad, der ausgenutzt werden kann, um Informationen unter Verstoß gegen die Sicherheitsrichtlinie zu übertragen, zum Beispiel durch Timing- oder Ressourcen-Nutzungsmuster in gemeinsam genutzter AI-Infrastruktur.

* CycloneDX – Ein offener Standard für Software- und KI-Produkt-Assets (Bill of Materials), der die Verwaltung von Komponentenbeständen, das Nachverfolgen von Schwachstellen und die Lizenz-Compliance unterstützt.

* DAG (gerichteter azyklischer Graph) – eine Graphstruktur mit gerichteten Kanten und ohne Zyklen, die in KI-Systemen verwendet wird, um Agenten-Entscheidungspfade, Schlussfolgerungsspurenn und Workflow-Abhängigkeiten darzustellen.

* Datenaugmentation – Eine Technik, die modifizierte Kopien von Trainingsdaten erstellt (z.B. durch Rotation, Rauschhinzufügung oder Umschreiben), um die Datenvielfalt des Datensatzes zu erhöhen und die Robustheit des Modells zu verbessern.

* Data Drift – eine Veränderung der statistischen Verteilung der Modell-Eingabedaten über die Zeit im Vergleich zu den Daten, auf denen das Modell trainiert wurde, die möglicherweise die Qualität der Vorhersagen beeinträchtigt.

* Datenleckage – Unbeabsichtigte Offenlegung sensibler Informationen durch KI-Modellausgaben oder -verhalten.

* Datenherkunft – die dokumentierte Kette der Herkunft, Transformation und Bewegung von Daten durch den Lebenszyklus eines KI-Systems, von der Erfassung über Vorverarbeitung, Training, Feinabstimmung, Einbettung und Inferenz. Die Herkunftsaufzeichnungen erfassen die Quellidentität, Transformationen, Zeitstempel und verantwortliche Parteien und ermöglichen Nachvollziehbarkeit sowie das Entfernen von Daten, deren Herkunft nicht verifiziert werden kann.

* Datenminimierung - Das Prinzip, nur die für einen definierten und dokumentierten Zweck erforderlichen Mindestdaten zu erheben, zu verarbeiten und aufzubewahren. In KI-Systemen erstreckt sich dies auf die Auswahl der Trainingsdaten, das Feature Engineering, den Aufbau des Kontextfensters, die Einbeziehung von Retrieval-Chunks sowie auf Richtlinien zur Speicherung von Speicher- und Embedding-Daten.

* Datenvergiftung – Die absichtliche Manipulation von Trainingsdaten, um die Integrität des Modells zu beeinträchtigen, oft um Hintertüren zu installieren oder die Leistung zu verschlechtern.

* Defense-in-Depth – Eine Sicherheitsstrategie, die mehrere unabhängige Sicherheitskontrollen in Schichten kombiniert, sodass, wenn eine Ebene fehlschlägt, die anderen weiterhin Schutz bieten.

* Defensive Distillation – eine Trainingsmethode, bei der ein Modell auf den weichen Wahrscheinlichkeitsausgaben eines anderen Modells trainiert wird, um Entscheidungsgrenzen zu glätten und die Anfälligkeit für adversarielle Störungen zu verringern.

* Differential Privacy – ein mathematisch präziser Rahmen zur Bereitstellung statistischer Informationen über Datensätze unter dem Schutz der Privatsphäre einzelner Datenpersonen, quantifiziert durch ein Privacy-Budget epsilon (ε).

* DoS (Denial of Service) – Ein Angriff, der versucht, ein System unzugänglich zu machen, indem es mit Anfragen überflutet oder seine Ressourcen erschöpft werden.

* Herabstufung (Antwort) – Zurückgeben einer Modellantwort, die weniger spezifisch, weniger personalisiert oder anderweitig in ihrem Umfang reduziert ist, wenn eine vollständige Verarbeitung eine Autorisierungs- oder Einwilligungsgrenze überschreiten würde. Beispiele hierfür sind das Filtern von Abruf-Teilen, die aus nicht-einwilligenden betroffenen Personen stammen, das Unterdrücken personalisierter Felder oder das Zurückgeben einer generischen Antwort anstelle einer Antwort, die in materieller Weise auf eingeschränkten Daten beruht. Verweigerung ist stets eine zulässige Herabstufung. Zulässige Herabstufungsverhaltensweisen sollten pro Inferenzpfad dokumentiert werden.

* DPIA (Datenschutz-Folgenabschätzung) – Eine formale Bewertung, die gemäß Vorschriften wie der DSGVO erforderlich ist, um Risiken für personenbezogene Daten vor Beginn der Verarbeitung zu bewerten und zu mindern.

* DP-SGD (Differentially Private Stochastic Gradient Descent) – Ein Trainingsalgorithmus, der während des Modelltrainings kalibriertes Rauschen zu Gradientenaktualisierungen hinzufügt, um formale Differential Privacy-Garantien bereitzustellen.

* DRTM (Dynamic Root of Trust for Measurement) – Ein Hardware-Mechanismus, der einen vertrauenswürdigen Ausführungseinstieg zur Laufzeit herstellt und dadurch eine Integritätsprüfung von KI-Beschleuniger-Workloads ermöglicht.

* Einbettungen - Dichte Vektorrepräsentationen von Daten (Text, Bilder usw.), die semantische Bedeutung in einem hochdimensionalen Raum erfassen.

* Einbettungsinversion - eine Angriffstechnik, die einen ungefähren Klartextinhalt aus Vektor-Einbettungen rekonstruiert und potenziell sensible Informationen offenlegt, die als durch die Einbettungstransformation geschützt angenommen wurden. Verwandt: MITRE ATLAS AML.T0024.001. Siehe auch: Modelleinsicht.

* Exfiltration – die unbefugte Übertragung von Daten außerhalb eines Systems oder Sicherheitsbereichs. In KI-Systemen umfassen Exfiltrationspfade Modelloutputs, verdeckte Kanäle in generierten Inhalten, Nebeneffekte von Tools sowie Speicher- oder Einbettungs-Leckagen.

* Erklärbarkeit – Die Fähigkeit eines KI-Systems, mithilfe von Techniken wie SHAP, LIME, Attention-Maps und kontrafaktischen Erklärungen menschenverständliche Gründe für seine Entscheidungen und Vorhersagen bereitzustellen. Wird auch als Explainable AI (XAI) bezeichnet.

* Fail-Closed / Fail-Open – Fail-closed beschreibt ein System, das bei einem Fehler oder einem Ausfall einer Komponente standardmäßig in einem sicheren, gesperrten Zustand verbleibt und so eine unkontrollierte Ausführung verhindert. Fail-open beschreibt das Gegenteil: Der Betrieb läuft bei einem Fehler uneingeschränkt weiter. AISVS verlangt, dass AI-Komponenten mit Sicherheits- oder Autorisierungsverantwortung fail closed.

* Feature Attribution – Eine Interpretierbarkeitsmethode, die Wichtigkeitsscores für einzelne Eingabemerkmale zuweist und deren Beitrag zu einer bestimmten Modellvorhersage angibt.

* Federated Learning – ein maschinelles Lernverfahren, bei dem Modelle über mehrere dezentrale Geräte hinweg trainiert werden, die lokale Datensamples halten, ohne dass die Daten selbst ausgetauscht werden.

* Feinabstimmung – Der Prozess, bei dem ein vortrainiertes Modell auf einem kleineren, aufgabenbezogenen Datensatz weitertrainiert wird, um es für einen bestimmten Anwendungsfall anzupassen.

* FIPS 140-3 – ein US-Regierungsstandard, der Sicherheitsanforderungen für kryptografische Module definiert, wobei Level 3 physische Manipulationssicherheit und identitätsbasiertes Authentifizieren erfordert.

* Schutzgeländer – Einschränkungen, die implementiert wurden, um zu verhindern, dass KI-Systeme schädliche, voreingenommene oder anderweitig unerwünschte Ausgaben erzeugen.

* Halluzination – ein Phänomen, bei dem ein KI-Modell falsche oder irreführende Informationen erzeugt, die nicht in seinen Trainingsdaten, abgerufenen Kontexten oder der faktischen Realität verankert sind.

* Homoglyph – ein Zeichen, das visuell einem anderen Zeichen aus einem anderen Schriftsystem oder einer anderen Kodierung ähnelt (z. B. kyrillisch „а“ vs. lateinisch „a“), ausgenutzt in Angriffen, um textbasierte Eingabevalidierung zu umgehen.

* HSM (Hardware-Sicherheitsmodul) – ein dediziertes physisches Gerät, das kryptografische Schlüssel in einer manipulationssicheren Umgebung verwaltet, verarbeitet und speichert.

* Human-in-the-Loop (HITL) – Systeme, die so konzipiert sind, dass an entscheidenden Entscheidungspunkten eine menschliche Aufsicht, Verifizierung oder Intervention erforderlich ist.

* Infrastructure as Code (IaC) – Verwaltung und Bereitstellung von Infrastruktur über Code statt manueller Prozesse, wodurch Security-Scans und konsistente Deployments ermöglicht werden.

* Intervall-gebundene Propagation – eine formale Verifikationstechnik, die Schranken durch neuronale Netzwerk-Schichten propagiert, um zu bescheinigen, dass Modellvorhersagen robust gegenüber vorgegebenen Eingabestörungen innerhalb definierter zulässiger Perturbationsbereiche sind.

* Jailbreak – Techniken, die eingesetzt werden, um Sicherheits-Schutzvorrichtungen in KI-Systemen, insbesondere in großen Sprachmodellen, zu umgehen und verbotene Inhalte zu erzeugen.

* JIT (Just-in-Time) Privileged Access – Eine Sicherheitsmaßnahme, bei der erhöhte Berechtigungen nur für ein kurzes, fest definiertes Zeitfenster gewährt werden, wenn sie für eine bestimmte Aufgabe erforderlich sind, und anschließend automatisch entzogen werden, wodurch die dauerhafte Berechtigungsfreigabe minimiert wird.

* JWT (JSON Web Token) – Ein kompakter, eigenständiger Token-Formattyp zur sicheren Übertragung von Identitäts- und Autorisierungsansprüchen zwischen Parteien, signiert, um die Integrität sicherzustellen.

* k-Anonymität – Eine Datenschutz-Eigenschaft, bei der jeder Datensatz in einem Datensatz gegenüber mindestens k-1 anderen Datensätzen bezüglich bestimmter identifizierender Attribute nicht unterscheidbar ist.

* Kill-Switch – ein Mechanismus, um die Inferenz von KI-Modellen, die Ausführung von Agenten oder die Ausgabe des Systems auf Befehl oder als Reaktion auf einen Sicherheitsauslöser sofort zu stoppen. Kill-Switches für autonome Agenten müssen über einen Kanal bereitgestellt werden, auf den die Agenten-Laufzeitumgebung nicht zugreifen oder den sie nicht unterdrücken kann, sodass ein kompromittierter Agent seine eigene Abschaltung nicht blockieren kann. Siehe auch C14.1.

* KMS (Key Management Service) – Ein verwalteter Dienst zum Erstellen, Speichern, Rotieren und Steuern des Zugriffs auf kryptografische Schlüssel, die verwendet werden, um Daten und Artefakte zu schützen.

* l-Diversität – eine Datenschutz-Eigenschaft, die k-Anonymität erweitert und erfordert, dass jede Äquivalenzklasse mindestens l unterschiedliche Werte für sensible Attribute enthält, um eine Offenlegung von Attributen zu verhindern.

* Least Privilege – Das Sicherheitsprinzip, das nur die notwendigen Mindestzugriffsrechte für Benutzer und Prozesse gewährt.

* LIME (Local Interpretable Model-agnostic Explanations) – Eine Technik, um die Vorhersagen eines beliebigen Machine-Learning-Klassifikators zu erklären, indem er lokal durch ein interpretierbares Modell angenähert wird.

* Verknüpfungsangriff – Ein Angriff, der quasi-identifizierende Merkmale über mehrere Datensätze hinweg kombiniert, um Personen wiederzuerkennen, deren Daten angeblich anonymisiert wurden.

* Machine Unlearning – Techniken zum Entfernen des Einflusses spezifischer Trainingsdaten aus einem trainierten Modell, zur Unterstützung von Datenlöschungsanfragen von Betroffenen und zur Einhaltung regulatorischer Anforderungen.

* Many-Shot Jailbreaking – Eine Angriffstechnik, die eine große Anzahl gefälschter Benutzer-Modell-Austauschpaare in das Kontextfenster einbettet, um das scheinbare Verhaltensmuster des Modells zu verschieben und seine Sicherheits-Leitplanken durch kumulierte In-Context-Beispiele zu umgehen.

* MCP (Model Context Protocol) – Ein Protokoll, das es KI-Modellen und Agenten ermöglicht, über einen definierten Transport durch den Austausch strukturierter, typisierter Anfragen und Antworten auf externe Tools, Datenquellen und Ressourcen zuzugreifen.

* Mitgliedschafts-Inferrenzangriff – Ein Angriff, der darauf abzielt festzustellen, ob ein bestimmter Datenpunkt für das Training eines maschinellen Lernmodells verwendet wurde.

* MIG (Multi-Instance GPU) – Eine NVIDIA-Technologie, die eine einzelne GPU in mehrere isolierte Instanzen aufteilt, jeweils mit dediziertem Speicher und Rechenressourcen für sichere Multi-Tenant-Workloads.

* MITRE ATLAS – Adversarial Threat Landscape für Künstliche-Intelligenz-Systeme; eine Wissensdatenbank für Adversarial Taktiken und Techniken gegen KI-Systeme.

* Modellkarte – Ein Dokument, das standardisierte Informationen über die Leistung, Einschränkungen, beabsichtigten Verwendungen und ethischen Überlegungen eines KI-Modells bereitstellt, um Transparenz und eine verantwortungsvolle KI-Entwicklung zu fördern.

* Modell-Extraktion – Ein Angriff, bei dem ein Angreifer das Zielmodell wiederholt abfragt, um eine funktional ähnliche Kopie ohne Berechtigung zu erstellen. Wird auch als Modell-Diebstahl oder Modellraub bezeichnet.

* Model-Inversion – ein Angriff, der versucht, Trainingsdaten durch die Analyse von Modell-Ausgaben zu rekonstruieren.

* Model-Lifecycle-Management – Der Prozess, bei der alle Phasen der Existenz eines KI-Modells überwacht werden, einschließlich Design, Entwicklung, Deployment, Monitoring, Wartung und dem letztendlichen Rückzug.

* Modellvergiftung – Das Einführen von Schwachstellen oder Hintertüren direkt in ein Modell während des Trainingsprozesses.

* mTLS (gegenseitiges TLS) – eine TLS-Konfiguration, bei der sowohl Client als auch Server sich gegenseitig mithilfe von Zertifikaten authentifizieren und so eine bidirektionale Identitätsprüfung für die dienst-zu-dienst-Kommunikation sicherstellen.

* Multi-Agenten-System – Ein System, das aus mehreren interagierenden KI-Agents besteht, wobei jeder Agent möglicherweise unterschiedliche Fähigkeiten und Ziele hat.

* NFC (Normalform C) – eine Unicode-Normalisierungsform, die Zeichen zerlegt und anschließend zu einer kanonischen Darstellung wieder zusammensetzt, um Umgehungsangriffe aufgrund von Kodierungsunterschieden zu verhindern.

* Nichtabstreitbarkeit – eine Sicherheitseigenschaft, die sicherstellt, dass eine Partei nicht glaubwürdig abstreiten kann, eine Aktion ausgeführt zu haben. In KI-Systemen wird dies durch kryptografische Signaturen von Agentenaktionen und Einträgen in Prüfprotokollen erreicht, wodurch die Zuordnung von Entscheidungen zu bestimmten Prinzipalen ermöglicht wird.

* NVLink – Eine Hochbandbreiten-Interconnect-Technologie für die GPU-zu-GPU-Kommunikation, die in Multi-Tenant-AI-Umgebungen eine Authentifizierung und Verschlüsselung erfordert.

* OAuth 2.1 – Ein Autorisierungs-Framework, das OAuth 2.0-Best Practices in einer einzelnen Spezifikation bündelt, das in AISVS als erforderlicher Authentifizierungsmechanismus für MCP-Clients und -Server verwendet wird.

* OIDC (OpenID Connect) – eine Identitätsschicht, die auf OAuth 2.0 aufbaut und Clients ermöglicht, die Benutzeridentität anhand der vom Autorisierungsserver durchgeführten Authentifizierung zu verifizieren.

* OPA (Open Policy Agent) – eine Open-Source-Policy-Engine für allgemeine Zwecke, die Autorisierungs- und Admission-Control-Richtlinien auswertet, die in Rego geschrieben sind, und die eine einheitliche Policy-Durchsetzung über Anwendungen, APIs und Infrastruktur hinweg ermöglicht.

* PDP (Policy Decision Point) – eine Komponente in einer Policy-Durchsetzungsarchitektur, die Autorisierungsanfragen anhand definierter Policies bewertet und eine Erlaubnis- oder Verweigerungsentscheidung zurückgibt. In agentischen KI-Systemen ist das PDP von der Ausführungsumgebung des Agents isoliert, um zu verhindern, dass ein kompromittierter Agent seine eigenen Autorisierungsentscheidungen beeinflusst. Siehe auch C9.7, C5.5.

* PII (Personenbezogene Daten) – Alle Informationen, die dazu verwendet werden können, eine bestimmte Person zu identifizieren, zu kontaktieren oder ihren Aufenthaltsort zu lokalisieren, entweder allein oder in Kombination mit anderen Daten.

* Policy-as-Code – die Praxis, Sicherheits- und Compliance-Richtlinien in maschinenlesbarem Code zu definieren, der versionierbar, testbar und automatisch in CI/CD-Pipelines durchsetzbar ist.

* Privacy-Preserving Machine Learning (PPML) – Techniken und Methoden zum Trainieren und Bereitstellen von ML-Modellen unter Wahrung der Privatsphäre der Trainingsdaten.

* Prompt-Injection – ein Angriff, bei dem bösartige Anweisungen in Eingaben eingebettet werden, um das beabsichtigte Verhalten eines Modells zu überschreiben.

* Prompt-Vorlage – ein strukturiertes Textmuster, das verwendet wird, um Prompts zu erstellen, die an ein KI-Modell übermittelt werden; es enthält feste Anweisungen, variable Platzhalter für Benutzereingaben und Formatierungsanweisungen. Prompt-Vorlagen sind KI-spezifische Konfigurationsartefakte, die einer Versionsverwaltung, einem Schutz der Integrität und Zugriffskontrollen entsprechen müssen, wie sie für Quellcode gelten.

* Quantisierung – eine Post-Training-Kompressionstechnik, die die Präzision der Modellgewichte reduziert (z.B. von 32-bit auf 8-bit oder 4-bit Integer), um den Speicherbedarf und die Inferenz-Latenz zu verringern. Die Quantisierung kann das Modellverhalten verändern, wodurch Sicherheits- und Robustheitseigenschaften nach der Anwendung erneut bewertet werden müssen.

* RAG (Retrieval-Augmented Generation) – Eine Technik, die große Sprachmodelle verbessert, indem sie relevante Informationen aus externen Wissensquellen abruft, bevor eine Antwort generiert wird.

* RBAC (rollenbasierte Zugriffskontrolle) – Ein Zugriffssteuerungsmodell, bei dem Berechtigungen Rollen statt einzelnen Benutzern zugewiesen werden, und Benutzer Zugriff erhalten, indem ihnen die entsprechenden Rollen zugewiesen werden.

* Red-Teaming – Die Praxis, KI-Systeme aktiv zu testen, indem man einschlägige Angriffe simuliert, um Schwachstellen zu identifizieren.

* Re-Identifizierungsrisiko – Die Wahrscheinlichkeit, dass eine Person aus einem angeblich anonymisierten Datensatz identifiziert werden kann, gemessen anhand definierter Schwellenwerte.

* Remote Attestation – Ein Mechanismus, bei dem eine Trusted-Execution-Environment (TEE) einem entfernten Kommunikationspartner einen kryptografischen Nachweis bereitstellt, dass auf einem echten, unverändertem TEE spezifischer Code ausgeführt wird.

* Reward Model – Ein Machine-Learning-Modell, das trainiert wurde, um menschliche Präferenzbewertungen für KI-Ausgaben vorherzusagen und als stellvertretendes Reward-Signal in RLHF-Trainingspipelines verwendet wird. Da Reward Models ML-Artefakte sind, sind sie anfällig für Data-Poisoning-Angriffe, die die Ergebnisse des Alignment-Trainings unterlaufen können.

* RLHF (Reinforcement Learning from Human Feedback) – Eine Trainingsmethode, bei der ein Modell mithilfe menschlicher Präferenzbewertungen als Belohnungssignal feinjustiert wird, um die Ausrichtung an menschlichen Werten und Sicherheitsanforderungen zu verbessern.

* SAML (Security Assertion Markup Language) – ein XML-basiertes Standardformat zum Austausch von Authentifizierungs- und Autorisierungsdaten zwischen Identitätsanbietern und Diensteanbietern.

* Sandboxing – Eine Isolierungstechnik, die einen Prozess oder eine Komponente in einer kontrollierten Umgebung einschränkt, mit eingeschränktem Dateisystemzugriff, eingeschränktem Netzwerk-Egress und Berechtigungen für Systemaufrufe. In KI-Systemen wird Sandboxing eingesetzt, um die Ausführung von Tools und Plugins, KI-Workloads und Inferenz von Drittanbieter-Modellen zu kapseln, um unautorisierten Host-Zugriff oder Kontamination zwischen Mandanten zu verhindern.

* SBOM (Software Bill of Materials) – Eine formale Aufzeichnung, die die Details und Lieferkettenbeziehungen der Software-Komponenten enthält, die beim Aufbau einer Anwendung verwendet werden. Siehe auch AI BOM für modellbezogene Artefakte.

* SCVS (Software Component Verification Standard) – Ein OWASP-Framework zur Überprüfung der Sicherheits-Eigenschaften von Softwarekomponenten, das von AISVS als Referenz für Supply-Chain-Integritätskontrollen genutzt wird, die auf KI-Frameworks, -Bibliotheken und Modellabhängigkeiten anwendbar sind.

* Secure Boot – eine Firmware-Sicherheitsfunktion, die die kryptografische Signatur jeder Komponente in der Boot-Kette vor der Ausführung überprüft und so verhindert, dass nicht autorisierte oder manipulierte Software geladen wird.

* Sichere Multi-Party-Berechnung (Secure Multi-Party Computation, SMPC) – eine kryptografische Technik, die es mehreren Parteien ermöglicht, gemeinsam eine Funktion über ihre privaten Eingaben zu berechnen, ohne diese Eingaben einander offenzulegen.

* seccomp (Secure Computing Mode) – eine Funktion des Linux-Kernels, die die Systemaufrufe einschränkt, die ein Prozess ausführen kann, verwendet, um AI-Workloads zu sandboxen und die Angriffsfläche zu reduzieren.

* SELinux (Security-Enhanced Linux) – ein Linux-Kernel-Sicherheitsmodul, das obligatorische Zugriffskontrollen mithilfe von Sicherheitsrichtlinien bereitstellt und zur Durchsetzung einer feingranularen Prozessisolation für AI-Workloads eingesetzt wird.

* Shadow Deployment – Ein Bereitstellungsmuster, bei dem eine neue Modellversion eine Kopie des Live-Produktionsverkehrs zusammen mit der aktuellen Version erhält, ohne Endbenutzern Antworten auszuliefern, wodurch ein Verhaltenvergleich und eine Sicherheitsvalidierung vor der Freigabe ermöglicht werden.

* Schattenmodell – ein Modell, das von einem Angreifer trainiert wird, um das Verhalten eines Zielmodells nachzuahmen; wird in Membership-Inference-Angriffen eingesetzt und als Referenz für die Bewertung der Wirksamkeit des Machine-Unlearning verwendet.

* SHAP (SHapley Additive exPlanations) – ein spieltheoretischer Ansatz, um die Ausgabe jedes Machine-Learning-Modells zu erklären, indem der Beitrag jedes Merkmals zur Vorhersage berechnet wird.

* Seitenkanalangriff – Ein Angriff, der Informationen aus einem System durch indirekte Beobachtung physikalischer Eigenschaften wie Zeitverhalten, Leistungsaufnahme, elektromagnetische Ausstrahlungen oder Cache-Verhalten extrahiert, anstatt Software-Schwachstellen auszunutzen.

* SIEM (Security Information and Event Management) – Eine Plattform, die Sicherheitsereignisdaten von mehreren Quellen aggregiert, korreliert und analysiert, um Bedrohungen zu erkennen, den Incident Response zu unterstützen und die Anforderungen an die Compliance zu erfüllen.

* SLSA (Supply-chain Levels for Software Artifacts) – Ein Sicherheitsframework, das inkrementelle Stufen von Supply-Chain-Integritätsgarantien definiert, von grundlegender Dokumentation des Build-Prozesses bis hin zu vollständig reproduzierbaren, hermetisch abgedichteten Builds mit authentifizierter Artefakt-Provenienz. Wird von AISVS für Kontrollen zur AI-Modell- und Artefakt-Supply-Chain referenziert.

* SOC (Security Operations Center) – Ein Team oder eine Einrichtung, das bzw. die für die Überwachung, Erkennung, Analyse und Reaktion auf Sicherheitsvorfälle zuständig ist. In AISVS verwenden SOC-Teams AI-Sicherheitsereignisprotokolle zur Korrelation, Triage und Incident Response.

* SPDX (Software Package Data Exchange) – ein offener Standard für die Kommunikation von Informationen zu Software- und KI-Komponenten-Bill-of-Materials, einschließlich Herkunft der Komponenten, Lizenzierung und Sicherheitsreferenzen.

* SSE (Server-Sent Events) – Eine Web-Technologie, die es einem Server ermöglicht, Echtzeit-Updates an einen Client über eine HTTP-Verbindung zu übertragen, und die als Transportmechanismus in MCP verwendet wird.

* Steganografie – die Praxis, Daten in anderen Medien (Bilder, Audio, Video) so zu verbergen, dass es für Beobachter nicht erkennbar ist, und die als Angriffsvektor verwendet wird, um Nutzdaten an Inhaltsfiltern vorbei zu schmuggeln.

* stdio (Standard Input/Output) – ein Prozess-Kommunikationsmechanismus, der Standard-Eingabe, Standard-Ausgabe und Fehler-Streams verwendet. In MCP wird dies als lokal-only Transport eingesetzt, der auf die Kommunikation innerhalb eines einzelnen Prozesses auf demselben Rechner beschränkt ist.

* Starke Authentifizierung – Authentifizierung, die sich gegen das Abgreifen von Zugangsdaten und Replay-Angriffe wappnet, indem mindestens zwei Faktoren (Wissen, Besitz, Inhärenz) erforderlich sind, sowie phishing-resistente Mechanismen wie FIDO2/WebAuthn, zuständigkeitsbasierte Dienstauthentifizierung mit Zertifikaten oder kurzlebige Tokens.

* Supply-Chain-Angriff – Kompromittierung eines Systems, indem weniger sichere Elemente in seiner Lieferkette angegriffen werden, wie z. B. Drittanbieter-Bibliotheken, Datensätze oder vortrainierte Modelle.

* Synthetische Daten – künstlich erzeugte Daten, die die statistischen Eigenschaften realer Daten beibehalten, aber keine tatsächlichen einzelnen Datensätze enthalten; werden zum Schutz der Privatsphäre während des Modelltrainings und -tests verwendet.

* TEE (Trusted Execution Environment) – eine hardwareisolierte Verarbeitungumgebung, die Vertraulichkeit- und Integritätsgarantien für Code und Daten bereitstellt und diese vor dem Host-Betriebssystem und anderen Mandanten schützt.

* Temperaturskalierung – eine Post-hoc-Kalibrierungstechnik, die die Konfidenzwerte der Modellausgaben so anpasst, dass sie die tatsächlichen Vorhersagewahrscheinlichkeiten besser widerspiegeln.

* TLS (Transport Layer Security) – Ein kryptografisches Protokoll, das Ende-zu-Ende-Verschlüsselung, Authentifizierung und Integrität für über ein Netzwerk übertragene Daten bereitstellt. AISVS erfordert TLS 1.3 oder höher.

* Tokenizer – Eine Komponente, die Rohtext in eine Folge von Tokens (Subwords, Wörter oder Zeichen) umwandelt, die ein Sprachmodell als Eingabe verarbeiten kann.

* TPM (Trusted Platform Module) – Ein dedizierter Hardware-Chip, der kryptografische Funktionen bereitstellt, einschließlich sicherer Schlüsselgenerierung, -speicherung und Messung der Plattformintegrität.

* Transferlernen – Eine Technik, bei der ein für eine Aufgabe entwickeltes Modell als Ausgangspunkt wiederverwendet wird, um ein Modell für eine zweite Aufgabe zu trainieren.

* Vektor-Datenbank – Eine spezialisierte Datenbank zur Speicherung hochdimensionaler Vektoren (Embeddings) und zur Durchführung effizienter Ähnlichkeitssuchen.

* VRAM (Video Random Access Memory) – Speicher auf einer GPU zum Speichern von Modellgewichten, Aktivierungen und Zwischenergebnissen während der KI-Inferenz und des Trainings, wobei zwischen den Mandanten-Workloads eine Rücksetzung auf Null erforderlich ist.

* Schwachstellen-Scanning – Automatisierte Tools, die bekannte Sicherheitslücken in Softwarekomponenten identifizieren, einschließlich KI-Frameworks und Abhängigkeiten.

* WASM (WebAssembly) – Ein portables binäres Instruktionsformat, das die Ausführung von Code in einer Sandbox ermöglicht und als Isolationsmechanismus für KI-Tools und Plugins eingesetzt wird.

* Wasserzeichen – Techniken, um unauffällige Marker in KI-generierten Inhalten oder Modellgewichten einzubetten, um die Herkunft nachzuverfolgen, nicht autorisierte Kopien zu erkennen oder KI-generierte Medien zu identifizieren.

* WORM (Write-Once-Read-Many) – eine Speichertechnologie, die die nachträgliche Änderung oder Löschung von Daten nach dem Schreiben verhindert und für manipulationssichere Audit-Logs sowie Schutz vor Backups verwendet wird.

* Zero-Day-Schwachstelle – eine zuvor unbekannte Schwachstelle, die Angreifer ausnutzen können, bevor Entwickler eine Problembehebung erstellen und bereitstellen.

* Zero-Trust – Ein Sicherheitsmodell, das für keinen Benutzer, kein Gerät und kein Netzwerk implizites Vertrauen voraussetzt und für jede Zugriffsanforderung eine kontinuierliche Überprüfung der Identität und Berechtigung erfordert.

