# C14 Menschliche Aufsicht und Vertrauen

## Kontrollziel

Stellen Sie sicher, dass Menschen eine effektive Kontrolle über KI-Systeme behalten, durch zuverlässige Abschaltmechanismen und sanfte Degradationspfade, durch eine explizite Richtlinie, die festlegt, welche KI-Entscheidungen und Agentenaktionen eine menschliche Genehmigung erfordern, sowie durch eine unabhängige Audit-Spur für menschliche Eingriffe in der Aufsicht.

Dieses Kapitel konzentriert sich auf Kontrollen, die für die menschliche Aufsicht über KI-Systeme spezifisch sind: Not-Aus-Schalter (Kill-switch) und Mechanismen für Zwischenzustände, die sich auf die Laufzeitstruktur von KI beziehen (Modellinferenz, Agenten-Laufzeiten, Tool-/MCP-Server, Retrieval-Connectoren), die Richtlinie, die KI-Entscheidungen und Agentenaktionen als hohes Risiko einstuft, das Systemverhalten, wenn kein menschlicher Genehmiger innerhalb des erforderlichen Zeitrahmens verfügbar ist, sowie die Protokollierung von durch Menschen initiierten Überschreibungsereignissen.

---

## C14.1 Kill-Switch & Override-Mechanismen

Stellen Sie Abschalt- oder Rollback-Pfade bereit, wenn ein unsicheres Verhalten des KI-Systems beobachtet wird, und stellen Sie sicher, dass diese Mechanismen im Laufe der Zeit funktionsfähig bleiben.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.1.1 | Stellen Sie sicher, dass ein manuelles Kill-Switch-Mechanismus vorhanden ist, um die Inferenz von KI-Modellen und deren Ausgaben sofort zu stoppen.                                                                                                                                                                                                                                                                                                                                                                                                      |   1   |
| 14.1.2 | Verifizieren Sie, dass Kill-Switch- und Zwischenzustandsmechanismen in einer definierten Frequenz ausgeübt werden, und dass jeder Test bestätigt, dass das System den Zielzustand innerhalb der dokumentierten Reaktionszeit erreicht sowie dass alle abhängigen Komponenten (z.B. Agent-Laufzeiten, Tool-/MCP-Server, Retrieval-Connectoren) wie spezifiziert in die jeweiligen Zustände übergehen.                                                                                                                                                     |   2   |
| 14.1.3 | Stellen Sie sicher, dass das System zwischen dem Volleinsatz und der vollständigen Abschaltung mindestens zwei Zwischenbetriebszustände erreichen kann (z.B. das Deaktivieren bestimmter Tools oder MCP-Server, das Entfernen einer Retrieval-Quelle, das Umschalten auf ein sichereres oder kleineres Modell, das Erzwingen des Nur-Lese-Modus für Agents) und dass jeder Zustand definierte Eintrittsauslöser hat und unabhängig voneinander verlassen werden kann, ohne dass ein vollständiger Systemneustart oder eine Abschaltung erforderlich ist. |   2   |
| 14.1.4 | Verifizieren Sie, dass Override- und Kill-Switch-Befehle für autonome Agenten über einen Out-of-Band-Kanal (z.B. Infrastruktur-Steuerungen, Hypervisor-Level-Signale, Isolierung auf Netzwerkebene) übermittelt werden, der architektonisch vom Agentenlaufzeitumfeld getrennt ist, sodass Befehle weiterhin durchsetzbar bleiben, selbst wenn die Agentenlaufzeit kompromittiert oder manipuliert wurde.                                                                                                                                                |   2   |

---

## C14.2 Menschliche-in-die-Schleife-Entscheidungs-Checkpoints

Definieren Sie, welche AI-Entscheidungen und Agentenaktionen eine menschliche Genehmigung erfordern, damit Laufzeit-Gates sie durchsetzen können, und definieren Sie das Systemverhalten, wenn die Genehmigung nicht rechtzeitig bereitgestellt wird.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                            | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.2.1 | Überprüfen Sie, dass eine dokumentierte Richtlinie zur menschlichen Aufsicht festlegt, welche KI-Entscheidungen und Agentenaktionen als Hochrisiko eingestuft werden, welche Kriterien für diese Feststellung verwendet werden und welche Genehmigungsbefugnis vor der Ausführung erforderlich ist.                                                     |   1   |
| 14.2.2 | Überprüfen Sie, dass das System, wenn ein Human-Approval-Gate (gemäß C14.2.1 und C9.2) innerhalb der definierten Approval-Time-to-Live nicht erfüllt wird, eine dokumentierte Standardaktion anwendet, die fail-closed ist (blockiert die ausstehende Aktion).                                                                                          |   2   |
| 14.2.3 | Verifizieren Sie, dass jede Abweichung von der fail-closed-Vorgabe für die Ablaufzeit (TTL) eines Genehmigers ausdrücklich in der Richtlinie zur menschlichen Aufsicht (C14.2.1) autorisiert ist und dass diese Abweichung selbst als risikoreiche Richtlinienentscheidung eingestuft wird, die eine Genehmigungsbefugnis zur Unterzeichnung erfordert. |   2   |

---

## C14.3 Protokollierung von Eingriffen menschlicher Aufsicht

Erfassen Sie von Menschen eingeleitete Überwachungsereignisse, sodass Überschreibungs- und Modusänderungsaktionen unabhängig prüf- und rekonstruierbar sind.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                       | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 14.3.1 | Stellen Sie sicher, dass Kill-Switch-Aktivierungen, Übergänge in einem Zwischenbetriebszustand und Override-Befehle mit der Identität des Operators, dem verwendeten Kanal (einschließlich der Information, ob der Out-of-Band-Kanal gemäß C14.1.4 aufgerufen wurde), dem auslösenden Trigger oder der Begründung, dem vorherigen und dem resultierenden Systemzustand sowie dem Zeitstempel protokolliert werden. |   1   |

## Referenzen

* [MITRE ATLAS: Human In-the-Loop for AI Agent Actions](https://atlas.mitre.org/mitigations/AML.M0029)
* [NIST AI 100-1: AI Risk Management Framework (AI RMF 1.0)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf)
* [NIST AI 600-1: Generative AI Profile (AI RMF Companion)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)
* [ISO/IEC 42001:2023 Artificial Intelligence Management System](https://www.iso.org/standard/42001)
* [ISO/IEC 23894:2023 Artificial Intelligence Risk Management Guidance](https://www.iso.org/standard/77304.html)
* [Regulation (EU) 2024/1689 (EU AI Act), Article 14: Human Oversight](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)
* [OECD Recommendation on Artificial Intelligence](https://legalinstruments.oecd.org/en/instruments/OECD-LEGAL-0449)
* [OWASP Top 10 for LLM Applications 2025: LLM06 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)
* [OWASP AI Exchange: Human Oversight Controls](https://owaspai.org/)

