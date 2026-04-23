# Vorwort

Willkommen beim Artificial Intelligence Security Verification Standard (AISVS) Version 1.0.

## Warum AISVS existiert

KI-Systeme bringen Sicherheitsrisiken mit sich, für die herkömmliche Standards der Anwendungssicherheit nicht ausgelegt waren. Prompt Injection ermöglicht es Angreifern, Modellanweisungen durch konstruierte Eingaben zu überschreiben und ein Sprachmodell so zu einem Werkzeug für Data Exfiltration, unautorisierte Aktionen oder das Umgehen von Sicherheitsmaßnahmen zu machen. Trainingsdaten können vergiftet werden, um Backdoors zu installieren oder das Modellverhalten zu verschlechtern. Modelle können extrahiert, invertiert oder durch adversariale Eingaben manipuliert werden. Autonome Agenten können anhand von Prompt-injizierten Anweisungen, die sie nicht von legitimen unterscheiden können, Aktionen mit realen Auswirkungen ausführen. Retrieval-Pipelines können ausgenutzt werden, um vertrauliche Informationen zu leaken oder bösartigen Inhalt in den Modellkontext einzuschleusen. Und die Supply Chain für Modelle, Datasets und Frameworks stellt neuartige Integritätsherausforderungen dar, die allein durch bestehende Software-Composition-Analyse nicht gelöst werden können.

AISVS wurde erstellt, um Organisationen einen strukturierten, testbaren Satz von Sicherheitskontrollen zu bieten, der speziell für diese Risiken ausgelegt ist. Es ersetzt keine bestehenden Standards; es schließt die Lücke, die keiner von ihnen abdeckt.

## Designprinzipien

Die Norm ist in 14 Kapitel (Controls) untergliedert. Jedes Kapitel ist in thematische Abschnitte aufgeteilt, die zusammen einen ganzheitlichen Ansatz bieten, um das Kontrollziel zu erreichen. Abschnitte werden in Anforderungen unterteilt. Ein Abschnitt darf keine Anforderungen für jede Ebene bereitstellen und muss keine Anforderungen enthalten, die bereits an anderer Stelle in der Norm vorhanden sind.

Jede Anforderung muss eine einzelne Fragestellung abdecken, die in gängigen Szenarien als eine technische Einzelmaßnahme umgesetzt und geprüft werden kann. Eine Anforderung kann schrittweise strengere Kriterien auf höheren Ebenen vorsehen; sofern vorhanden, werden diese in dem Abschnitt als separate Anforderungen dargestellt. Anforderungen müssen, soweit möglich, eine klare, technologie-neutrale Sprache verwenden und zur Verdeutlichung auf allgemein bekannte Technologien als Beispiele verweisen.

Jede Anforderung in AISVS folgt diesen Prinzipien, die aus dem Namen des Standards abgeleitet sind:

* Künstliche Intelligenz. Jede Steuerungsmaßnahme arbeitet auf der KI- oder ML-Ebene (Daten, Modell, Pipeline, Agent oder Inferenz) und adressiert Risiken, die spezifisch für KI-Systeme sind, anstatt allgemeine Anwendungssicherheit. Die Norm dupliziert keine Steuerungsmaßnahmen aus anderen breiten, allgemein anerkannten Standards oder Frameworks (wie ASVS), sofern die Steuerungsmaßnahme keine einzigartigen, KI-spezifischen Implementierungsaspekte hat.
* Sicherheit. Jede Anforderung mindert direkt ein identifiziertes Risiko für Sicherheit, Privatsphäre oder Sicherheit. Kontrollen, die nur operative, Governance-, Compliance- oder geschäftliche Ziele verfolgen, fallen nicht in den Geltungsbereich.
* Verifikation. Die Anforderungen sind so formuliert, dass die Konformität objektiv durch Tests, Inspektionen oder Audits überprüft werden kann. Es muss ausreichende Implementierungsanleitung oder Werkzeugunterstützung vorhanden sein, um sowohl die Implementierung als auch die wirksame Verifikation der Anforderung zu ermöglichen; rein theoretische, subjektive oder rein aspirational formulierte Anleitungen sind ausgeschlossen.
* Standard. Alle Kapitel folgen einer konsistenten Struktur und Terminologie, um ein zusammenhängendes, navigierbares Referenzdokument zu bilden.

## So lesen Sie diese Norm

### Kapitelstruktur

Jedes der 14 Anforderungskapitel folgt demselben Aufbau:

* Control Eine kurze Aussage über das Sicherheitsziel für das Kapitel.
* Abschnitte. Anforderungen werden in zusammengehörige Abschnitte gruppiert, wobei jedem Abschnitt eine kurze Beschreibung des Verteidigungsziels beigefügt ist.
* Anforderungstabellen. Einzelne Anforderungen werden in Tabellen mit den folgenden Spalten dargestellt:

| Spalte       | Bedeutung                                                                                   |
| ------------ | ------------------------------------------------------------------------------------------- |
| *#*          | Eindeutige Anforderungskennung (z.B. 1.1.1, 9.3.2).                                         |
| Beschreibung | Der Anforderungstext beginnt immer mit „Verify that“, um die Testbarkeit hervorzuheben.     |
| Ebene        | Das Verifizierungsniveau (1, 2 oder 3), das die erforderliche Tiefe der Zusicherung angibt. |

### Anhänge

Vier Anhänge unterstützen die Kernanforderungen:

* Anhang A (Glossar) definiert die wichtigsten Begriffe und Abkürzungen, die im gesamten Standard verwendet werden.
* Anhang B (Referenzen) listet externe Standards, Forschungen und Frameworks auf, auf die in den AISVS-Anforderungen Bezug genommen wird.
* Anhang C (KI-gestützte sichere Programmierung) enthält Kontrollen für die sichere Nutzung von KI-Code-Tools während der Softwareentwicklung.
* Anhang D (AI Security Controls Inventory) ist ein Verweiskatalog jeder Abwehrtechnik in AISVS, der nach Sicherheitskontrollkategorie (Authentifizierung, Autorisierung, Verschlüsselung, Eingabevalidierung und so weiter) organisiert ist und Zuordnungen zu spezifischen Anforderungskennungen enthält.

## Geltungsbereichsgrenzen

AISVS konzentriert sich auf Sicherheitskontrollen, die spezifisch für KI- und ML-Systeme sind. Es schließt absichtlich Folgendes aus:

* Allgemeine Anwendungssicherheit. Anforderungen, die durch die [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)(wie Sitzungsverwaltung, CSRF-Schutz oder Schutz vor SQL-Injection) werden hier nicht erneut behandelt. Organisationen sollten ASVS zusammen mit AISVS anwenden.
* KI-Governance und Risikomanagement. Organisationsbezogene Governance, Risikobewertungsmethodik und Compliance-Prozesse werden besser durch Frameworks wie das NIST AI RMF und ISO/IEC 42001 adressiert.
* Herstellerspezifische Anleitungen. AISVS ist herstellerneutral. Es beschreibt, was zu prüfen ist, nicht welches Produkt zu verwenden ist.

## Danksagungen

AISVS v1.0 ist das Ergebnis einer gemeinsamen Arbeit der Projektleiter, der Mitglieder der Arbeitsgruppen und der Beiträge aus der Community. Wir danken allen, die Anforderungen, Reviews und Feedback beigesteuert haben, um diese Norm möglich zu machen. Eine vollständige Liste der Mitwirkenden ist verfügbar in der [Frontispiece](0x01-Frontispiece.md).

Durch die Einführung von AISVS können Organisationen die Sicherheitslage ihrer KI-Systeme systematisch bewerten und stärken und eine Grundlage für sichere KI-Engineering-Praktiken schaffen, die sich parallel zur Technologie selbst weiterentwickelt.

