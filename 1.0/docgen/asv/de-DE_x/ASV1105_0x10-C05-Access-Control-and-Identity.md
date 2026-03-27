# C5 Zugriffskontrolle & Identität für KI-Komponenten & Benutzer

## Kontrollziel

Effektive Zugriffskontrolle für KI-Systeme erfordert ein robustes Identitätsmanagement, kontextbewusste Autorisierung und Laufzeitdurchsetzung nach Zero-Trust-Prinzipien. Diese Kontrollen stellen sicher, dass Menschen, Dienste und autonome Agenten nur innerhalb ausdrücklich gewährter Bereiche mit Modellen, Daten und Rechenressourcen interagieren, mit kontinuierlicher Überprüfung und Audit-Fähigkeiten.

---

## C5.1 Identitätsverwaltung & Authentifizierung

Stellen Sie für alle Entitäten, die mit KI-Systemen interagieren, verifizierte Identitäten mit einer Authentifizierungsstärke her, die dem Risikoniveau angemessen ist.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 5.1.1 | Stellen Sie sicher, dass alle menschlichen Benutzer und Dienstprinzipale sich über einen zentralisierten Identitätsanbieter mit branchenüblichen Föderationsprotokollen (z. B. OIDC, SAML) authentifizieren.                                                                                                                          |   1   |  D/V  |
| 5.1.2 | Stellen Sie sicher, dass für risikoreiche Vorgänge (Modelldeployment, Gewichtsexport, Zugriff auf Trainingsdaten, Änderungen der Produktionskonfiguration) eine Multi-Faktor-Authentifizierung oder eine Step-up-Authentifizierung mit Sitzungsneuverifikation erforderlich ist.                                                      |   2   |  D/V  |
| 5.1.3 | Stellen Sie sicher, dass KI-Agenten in föderierten oder Multi-System-Implementierungen sich über kurzlebige, kryptographisch signierte Authentifizierungstoken (z. B. signierte JWT-Assertions) authentifizieren, deren maximale Lebensdauer dem Risikoniveau entspricht und die einen kryptographischen Herkunftsnachweis enthalten. |   3   |  D/V  |

---

## C5.2 Autorisierung & Richtlinie

Implementieren Sie Zugriffskontrollen für alle KI-Ressourcen mit expliziten Berechtigungsmodellen und Prüfpfaden.

|   #   | Beschreibung                                                                                                                                                                                                                             | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 5.2.1 | Überprüfen Sie, ob jede KI-Ressource (Datensätze, Modelle, Endpunkte, Vektorsammlungen, Einbettungsindizes, Recheninstanzen) Zugriffskontrollen (z. B. RBAC, ABAC) mit expliziten Allow-Listen und Standard-Deny-Richtlinien durchsetzt. |   1   |  D/V  |
| 5.2.2 | Stellen Sie sicher, dass alle Änderungen der Zugriffskontrolle mit Zeitstempeln, Akteur-Identitäten, Ressourcenkennungen und Berechtigungsänderungen protokolliert werden.                                                               |   1   |   V   |
| 5.2.3 | Überprüfen Sie, dass Zugriffskontroll-Protokolle unveränderlich gespeichert werden und Manipulationen erkennbar sind.                                                                                                                    |   2   |   V   |
| 5.2.4 | Verifizieren Sie, dass Datenklassifizierungslabels (PII, PHI, proprietär usw.) automatisch auf abgeleitete Ressourcen (Embeddings, Prompt-Caches, Modellausgaben) übertragen werden.                                                     |   2   |   D   |
| 5.2.5 | Überprüfen Sie, dass unautorisierte Zugriffsversuche und Ereignisse der Privilegienerweiterung Echtzeitwarnungen mit kontextuellen Metadaten auslösen.                                                                                   |   2   |  D/V  |
| 5.2.6 | Stellen Sie sicher, dass Autorisierungsentscheidungen an einen dedizierten Policy Decision Point (z. B. OPA, Cedar oder gleichwertig) ausgelagert werden.                                                                                |   3   |  D/V  |
| 5.2.7 | Stellen Sie sicher, dass Richtlinien dynamische Attribute zur Laufzeit auswerten, einschließlich Benutzerrolle oder -gruppe, Ressourcenkategorie, Anfragekontext, Mandantentrennung und zeitlicher Beschränkungen.                       |   3   |  D/V  |
| 5.2.8 | Überprüfen Sie, ob die TTL-Werte des Richtlinien-Caches basierend auf der Sensitivität der Ressourcen definiert sind, mit kürzeren TTLs für hochsensible Ressourcen, und ob Funktionen zur Cache-Invalidierung vorhanden sind.           |   3   |  D/V  |

---

## C5.3 Sicherheitsdurchsetzung zur Abfragezeit

Durchsetzung der Autorisierung auf der Datenzugriffsschicht, um unautorisierte Datenabfragen durch KI-Anfragen zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                                                           | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 5.3.1 | Stellen Sie sicher, dass alle Datenbankabfragen (z. B. Vektordatenbanken, SQL-Datenbanken, Suchindizes) obligatorische Sicherheitsfilter (Mandanten-ID, Sensitivitätskennzeichnungen, Benutzerbereich) enthalten, die auf der Datenzugriffs-Ebene durchgesetzt werden. |   1   |  D/V  |
| 5.3.2 | Überprüfen Sie, dass fehlgeschlagene Autorisierungsbewertungen Abfragen sofort abbrechen und explizite Autorisierungsfehlercodes zurückgeben.                                                                                                                          |   1   |   D   |
| 5.3.3 | Stellen Sie sicher, dass für alle Datenspeicher, die sensible Daten enthalten und von KI-Systemen verwendet werden, zeilenbasierte Sicherheitsrichtlinien und feldbasierte Maskierung mit Richtlinienvererbung aktiviert sind.                                         |   2   |  D/V  |
| 5.3.4 | Stellen Sie sicher, dass Abfrage-Wiederholungsmechanismen Autorisierungsrichtlinien neu bewerten, um dynamische Berechtigungsänderungen innerhalb aktiver Sitzungen zu berücksichtigen.                                                                                |   3   |  D/V  |

---

## C5.4 Ausgabefilterung & Datenverlustprävention

Setzen Sie Nachbearbeitungskontrollen ein, um unbefugte Datenoffenlegung in KI-generierten Inhalten zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                | Ebene | Rolle |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 5.4.1 | Überprüfen Sie, ob Nach-Inferenz-Filtermechanismen nicht autorisierte personenbezogene Daten (PII), klassifizierte Informationen und proprietäre Daten scannen und schwärzen, bevor Inhalte an Anforderer geliefert werden. |   1   |  D/V  |
| 5.4.2 | Überprüfen Sie, ob Zitate, Verweise und Quellenangaben in den Modellausgaben anhand der Berechtigungen des Anrufers validiert werden, und entfernen Sie diese, falls ein unbefugter Zugriff festgestellt wird.              |   2   |  D/V  |
| 5.4.3 | Überprüfen Sie, ob die Einschränkungen im Ausgabeformat (bereinigte Dokumente, metadatenfreie Bilder, genehmigte Dateitypen) entsprechend den Benutzerberechtigungsstufen und Datenklassifikationen durchgesetzt werden.    |   2   |   D   |

---

## C5.5 Mehrmandanten-Isolation

Sicherstellung logischer und kryptografischer Isolation zwischen Mandanten in gemeinsamer KI-Infrastruktur.

|   #   | Beschreibung                                                                                                                                                                                                                | Ebene | Rolle |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 5.5.1 | Überprüfen Sie, ob Netzwerkrichtlinien Standard-Verweigerungsregeln für die Kommunikation zwischen Mandanten implementieren.                                                                                                |   2   |   D   |
| 5.5.2 | Stellen Sie sicher, dass jede API-Anfrage eine authentifizierte Mandantenkennung enthält, die kryptografisch gegen den Sitzungs kontext und die Benutzerberechtigungen validiert wird.                                      |   1   |  D/V  |
| 5.5.3 | Stellen Sie sicher, dass Speicherbereiche, Einbettungsspeicher, Cache-Einträge und temporäre Dateien pro Mandant namespace-getrennt sind und bei Löschung des Mandanten oder Beendigung der Sitzung sicher gelöscht werden. |   2   |  D/V  |
| 5.5.4 | Stellen Sie sicher, dass die Verschlüsselungsschlüssel pro Mandant eindeutig sind, mit Unterstützung für kundengeführte Schlüssel (CMK) und kryptografischer Isolation zwischen den Datenbanken der Mandanten.              |   3   |   D   |

---

## C5.6 Autorisierung autonomer Agenten

Kontrollieren Sie Berechtigungen für KI-Agenten und autonome Systeme durch definierte Berechtigungs-Tokens und kontinuierliche Autorisierung.

|   #   | Beschreibung                                                                                                                                                                                                                                       | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 5.6.1 | Stellen Sie sicher, dass autonome Agenten gebündelte Berechtigungstoken erhalten, die ausdrücklich die erlaubten Aktionen, zugänglichen Ressourcen, Zeitgrenzen und Betriebsbeschränkungen auflisten.                                              |   1   |  D/V  |
| 5.6.2 | Überprüfen Sie, dass risikoreiche Funktionen (Dateisystemzugriff, Codeausführung, externe API-Aufrufe, Finanztransaktionen) standardmäßig deaktiviert sind und eine ausdrückliche Genehmigung erfordern.                                           |   1   |  D/V  |
| 5.6.3 | Stellen Sie sicher, dass Fähigkeitstoken an Benutzersitzungen gebunden sind, eine kryptografische Integritätssicherung enthalten und nicht über Sitzungen hinweg gespeichert oder wiederverwendet werden können.                                   |   2   |   D   |
| 5.6.4 | Stellen Sie sicher, dass von Agenten initiierte Aktionen eine Autorisierung durch einen Policy Decision Point durchlaufen, der kontextbezogene Attribute bewertet (z. B. Benutzeridentität, Ressourcenempfindlichkeit, Aktionstyp, Umweltkontext). |   3   |   V   |

---

## Literaturverzeichnis

* [NIST SP 800-162: Guide to Attribute Based Access Control (ABAC)](https://csrc.nist.gov/pubs/sp/800/162/final)
* [NIST SP 800-207: Zero Trust Architecture](https://csrc.nist.gov/pubs/sp/800/207/final)
* [NIST SP 800-63-3: Digital Identity Guidelines](https://csrc.nist.gov/pubs/sp/800/63/3/final)
* [NIST IR 8360: Machine Learning for Access Control Policy Verification](https://csrc.nist.gov/pubs/ir/8360/final)

