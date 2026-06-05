# Vorwort

Willkommen beim Artificial Intelligence Security Verification Standard (AISVS) Version 1.0.

## Warum AISVS existiert

KI-Systeme bringen Sicherheitsrisiken mit sich, die traditionelle Standards der Anwendungs­sicherheit nicht dazu ausgelegt waren zu adressieren. Prompt Injection ermöglicht es Angreifern, Modellinstruktionen über konstruierte Eingaben zu überschreiben und ein Sprachmodell in ein Werkzeug für Daten-Exfiltration, nicht autorisierte Aktionen oder Sicherheitsumgehung zu verwandeln. Trainingsdaten können vergiftet werden, um Backdoors zu installieren oder das Modellverhalten zu verschlechtern. Modelle können extrahiert, invertiert oder durch adversariale Eingaben manipuliert werden. Autonome Agenten können auf Basis von Prompt-injizierten Anweisungen, die sie nicht von legitimen unterscheiden können, Handlungen mit realen Auswirkungen ausführen. Retrieval-Pipelines können ausgenutzt werden, um vertrauliche Informationen zu leaken oder bösartigen Inhalt in den Modellkontext einzuschleusen. Und die Supply Chain für Modelle, Datasets und Frameworks stellt neuartige Integritätsanforderungen bereit, die eine bestehende Software-Composition-Analyse allein nicht lösen kann.

AISVS wurde erstellt, um Organisationen einen strukturierten, testbaren Satz von Sicherheitskontrollen bereitzustellen, der gezielt für diese Risiken entwickelt wurde. Es ersetzt keine bestehenden Standards; es schließt die Lücke, die keiner von ihnen abdeckt.

## Designprinzipien

Die Norm ist in 14 Kapitel (Kontrollen) untergliedert. Jedes Kapitel ist in thematische Abschnitte aufgeteilt, die zusammen einen ganzheitlichen Ansatz bieten, um das Kontrollziel zu erreichen. Abschnitte werden in Anforderungen unterteilt. Ein Abschnitt darf keine Anforderungen für jede Ebene bereitstellen und muss keine Anforderungen enthalten, die andernorts in der Norm enthalten sind.

Jede Anforderung muss eine einzelne Problemstellung adressieren, die sich in üblichen Szenarien als eine technische Maßnahme umsetzen und als solche prüfen lässt. Eine Anforderung kann schrittweise strengere Kriterien auf höheren Ebenen vorsehen; sofern vorhanden, werden diese als separate Anforderungen in dem Abschnitt dargestellt. Anforderungen müssen, soweit möglich, eine klare, technologie-neutrale Sprache verwenden und dabei, wenn als hilfreich für die Klarheit erachtet, auf allgemein bekannte Technologien als Beispiele Bezug nehmen.

Jede Anforderung in AISVS folgt diesen Grundsätzen, die aus dem Namen der Norm abgeleitet sind:

* Künstliche Intelligenz. Jede Maßnahme arbeitet auf der KI- oder ML-Ebene (Daten, Modell, Pipeline, Agent oder Inferenz) und adressiert Risiken, die spezifisch für KI-Systeme sind, statt für allgemeine Anwendungssicherheit. Die Norm dupliziert keine Maßnahmen aus anderen weit verbreiteten Standards oder Frameworks (wie ASVS), sofern die Maßnahme keine einzigartigen, KI-spezifischen Implementierungsanforderungen hat.
* Sicherheit. Jede Anforderung mindert direkt eine identifizierte Sicherheits-, Datenschutz- oder Sicherheitsrisiko. Kontrollen, die nur operative, Governance-, Compliance- oder Geschäftsziele verfolgen, sind nicht im Geltungsbereich enthalten.
* Verifizierung. Die Anforderungen sind so formuliert, dass die Erfüllung objektiv durch Tests, Inspektionen oder Audits nachgewiesen werden kann. Es müssen ausreichende Implementierungsleitlinien oder Werkzeuge vorhanden sein, um sowohl die Umsetzung als auch eine wirksame Verifizierung der Anforderung zu ermöglichen; rein theoretische, subjektive oder aufstrebende Leitlinien sind ausgeschlossen.
* Standard. Alle Kapitel folgen einer konsistenten Struktur und Terminologie, um ein kohärentes, navigierbares Referenzdokument zu bilden.

## So lesen Sie diese Norm

### Kapitelstruktur

Jedes der 14 Anforderungs-Kapitel folgt demselben Format:

* Control Eine kurze Aussage des Sicherheitsziels für das Kapitel.
* Abschnitte. Anforderungen sind in zusammenhängenden Abschnitten gruppiert, die jeweils eine kurze Beschreibung des Verteidigungsziels enthalten.
* Anforderungstabellen. Einzelne Anforderungen werden in Tabellen mit den folgenden Spalten dargestellt:

| Spalte       | Bedeutung                                                                                 |
| ------------ | ----------------------------------------------------------------------------------------- |
| *#*          | Eindeutige Anforderungskennung (z.B. 1.1.1, 9.3.2).                                       |
| Beschreibung | Der Anforderungstext beginnt stets mit „Verify that“, um die Testbarkeit hervorzuheben.   |
| Ebene        | Die Verifikationsstufe (1, 2 oder 3), die die Tiefe der erforderlichen Sicherheit angibt. |

### Anhänge

Fünf Anhänge unterstützen die Kernanforderungen:

* Anhang A (Glossar) definiert die Schlüsselbegriffe und Abkürzungen, die in der gesamten Norm verwendet werden.
* Anhang B (Referenzen) listet externe Standards, Forschung und Frameworks auf, auf die sich AISVS-Anforderungen beziehen.
* Anhang C (KI-gestütztes sicheres Programmieren) bietet Kontrollen für die sichere Nutzung von KI-Coding-Tools während der Softwareentwicklung.
* Anhang D (AI-Sicherheitskontroll-Inventar) ist eine Querverweisliste jeder Abwehrtechnik in AISVS, die nach Sicherheitskontrollkategorie (Authentifizierung, Autorisierung, Verschlüsselung, Eingabevalidierung und so weiter) organisiert ist und Zuordnungen zu bestimmten Anforderungskennungen zurück enthält.
* Anhang E (Mitwirkende) listet die Projektleiter, Mitwirkenden und Prüfer auf, die dieses Standarddokument geprägt haben.

## Grenzen des Geltungsbereichs

AISVS konzentriert sich auf Sicherheitskontrollen, die speziell für KI- und ML-Systeme sind. Es schließt absichtlich aus:

* Allgemeine Anwendungssicherheit. Von Anforderungen abgedeckte Anforderungen, die durch die [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)(dazu gehören Sitzungsverwaltung, CSRF-Schutz oder die Verhinderung von SQL-Injection) werden hier nicht erneut aufgeführt. Organisationen sollten ASVS in Verbindung mit AISVS anwenden.
* KI-Governance und Risikomanagement. Organisationsbezogene Governance, Methodik zur Risikobewertung und Compliance-Prozesse werden besser durch Frameworks wie das NIST AI RMF und die ISO/IEC 42001 adressiert.
* Herstellerspezifische Hinweise. AISVS ist herstellerneutral. Es legt fest, was zu prüfen ist, nicht welches Produkt zu verwenden ist.

## Danksagungen

AISVS v1.0 ist das Ergebnis einer kollaborativen Zusammenarbeit der Projektleitungen, der Mitglieder der Arbeitsgruppen und der Community-Beitragenden. Wir danken allen, die Anforderungen, Reviews und Feedback beigesteuert haben, um diesen Standard möglich zu machen. Eine vollständige Liste der Beitragenden ist verfügbar in der[Frontispiece](0x01-Frontispiece.md).

Durch die Einführung von AISVS können Organisationen die Sicherheitslage ihrer KI-Systeme systematisch bewerten und stärken und so eine Grundlage für sichere KI-Engineering-Praktiken schaffen, die sich parallel zur Technologie selbst weiterentwickelt.

