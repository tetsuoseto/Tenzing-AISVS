# C10 Modellkontextprotokoll (MCP) Sicherheit

## Kontrollziel

Sichern Sie die sichere Erkennung, Authentifizierung, Autorisierung, Übertragung und Nutzung von auf MCP basierenden Werkzeug- und Ressourcenschnittstellen, um Kontextverwirrung, nicht autorisierte Werkzeugaufrufe oder Datenexposition zwischen Mandanten zu verhindern.

---

## C10.1 Komponentenintegrität & Lieferkettensauberkeit

|   #    | Beschreibung                                                                                                                                                                                                                                              | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 10.1.1 | Stellen Sie sicher, dass MCP-Server- und Client-Komponenten nur aus vertrauenswürdigen Quellen bezogen und mittels Signaturen, Prüfungen oder sicherer Paketmetadaten verifiziert werden, wobei manipulierte oder unsignierte Versionen abgelehnt werden. |   1   |  D/V  |

---

## C10.2 Authentifizierung & Autorisierung

|   #    | Beschreibung                                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 10.2.1 | Stellen Sie sicher, dass MCP-Clients sich mithilfe des OAuth 2.1-Autorisierungsframeworks bei MCP-Servern authentifizieren und für jede Anfrage ein gültiges OAuth-Access-Token vorlegen, und dass der MCP-Server das Token gemäß den Anforderungen eines OAuth 2.1-Ressourcenservers validiert.      |   1   |  D/V  |
| 10.2.2 | Überprüfen Sie, dass MCP-Server OAuth-Zugriffstoken validieren, einschließlich der Ansprüche Aussteller, Publikum, Ablaufdatum und Berechtigungen, um sicherzustellen, dass die Tokens speziell für den jeweiligen MCP-Server ausgestellt wurden, bevor die Tool-Ausführung erlaubt wird.             |   1   |  D/V  |
| 10.2.3 | Stellen Sie sicher, dass MCP-Server über einen kontrollierten technischen Onboarding-Mechanismus registriert werden, der explizite Definitionen für Eigentümer, Umgebung und Ressourcen erfordert; nicht registrierte oder nicht auffindbare Server dürfen in der Produktion nicht aufgerufen werden. |   1   |  D/V  |
| 10.2.4 | Überprüfen Sie, ob Autorisierungsentscheidungen auf der MCP-Ebene durch die Richtlinienlogik des MCP-Servers durchgesetzt werden und dass durch das Modell erzeugte Ausgaben keinen Einfluss auf die Zugriffskontrollprüfungen haben, diese nicht außer Kraft setzen oder umgehen können.             |   1   |  D/V  |
| 10.2.5 | Stellen Sie sicher, dass MCP-Server ausschließlich als OAuth 2.1-Ressourcenserver agieren, indem sie nur von externen Autorisierungsservern ausgestellte Tokens validieren und keine Tokens oder Benutzeranmeldeinformationen speichern.                                                              |   2   |  D/V  |
| 10.2.6 | Überprüfen Sie, dass MCP`tools/list`und Ressourcenentdeckungsantworten werden basierend auf den autorisierten Berechtigungen des Endbenutzers gefiltert, sodass Agenten nur die Werkzeuge und Ressourcendefinitionen erhalten, die der Benutzer aufrufen darf.                                        |   2   |  D/V  |
| 10.2.7 | Stellen Sie sicher, dass MCP-Server bei jedem Werkzeugaufruf Zugriffskontrollen durchsetzen und überprüfen, dass das Zugriffstoken des Benutzers sowohl das angeforderte Werkzeug als auch die angegebenen spezifischen Argumentwerte autorisiert.                                                    |   2   |  D/V  |

---

## C10.3 Sicherer Transport und Schutz der Netzgrenze

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                       | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 10.3.1 | Stellen Sie sicher, dass in Produktionsumgebungen als primärer MCP-Transport authentifiziertes, verschlüsseltes, streamfähiges HTTP verwendet wird und dass alternative Transporte (z. B. stdio oder SSE) auf lokale oder streng kontrollierte Umgebungen mit expliziter Begründung beschränkt sind.               |   2   |  D/V  |
| 10.3.2 | Stellen Sie sicher, dass streamable-HTTP MCP-Transporte authentifizierte, verschlüsselte Kanäle (TLS 1.3 oder höher) mit Zertifikatvalidierung verwenden.                                                                                                                                                          |   2   |  D/V  |
| 10.3.3 | Stellen Sie sicher, dass SSE-basierte MCP-Transporte nur innerhalb privater, authentifizierter interner Kanäle verwendet werden und erzwingen Sie TLS, Authentifizierung, Schemaüberprüfung, Payload-Größenbegrenzungen und Ratenbegrenzung; SSE-Endpunkte dürfen nicht dem öffentlichen Internet ausgesetzt sein. |   2   |  D/V  |
| 10.3.4 | Überprüfen Sie, ob MCP-Server die Validierung der`Origin`und`Host`Header in allen HTTP-basierten Übertragungen (einschließlich SSE und streambarem HTTP), um DNS-Rebinding-Angriffe zu verhindern und Anfragen von nicht vertrauenswürdigen, nicht übereinstimmenden oder fehlenden Ursprüngen abzulehnen.         |   2   |  D/V  |

---

## C10.4 Schema-, Nachrichten- und Eingabevalidierung

|   #    | Beschreibung                                                                                                                                                                                                                                                                                      | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 10.4.1 | Stellen Sie sicher, dass die Antworten des MCP-Tools validiert werden, bevor sie in den Modellspeicher eingefügt werden, um Prompt-Injektionen, bösartigen Tool-Ausgaben oder Kontextmanipulationen vorzubeugen.                                                                                  |   1   |  D/V  |
| 10.4.2 | Stellen Sie sicher, dass MCP-Werkzeug- und Ressourcen-Schemas (z. B. JSON-Schemas oder Fähigkeitsbeschreibungen) mithilfe von Signaturen auf Authentizität und Integrität überprüft werden, um eine Manipulation der Schemas oder böswillige Parameteränderungen zu verhindern.                   |   2   |  D/V  |
| 10.4.3 | Stellen Sie sicher, dass alle MCP-Transporte die Integrität der Nachrichtenrahmen, eine strenge Schemaüberprüfung, maximale Nutzlastgrößen und die Ablehnung von fehlerhaften, abgeschnittenen oder vermischten Rahmen durchsetzen, um Desynchronisations- oder Injektionsangriffe zu verhindern. |   2   |  D/V  |
| 10.4.4 | Überprüfen Sie, ob MCP-Server eine strenge Eingabevalidierung für alle Funktionsaufrufe durchführen, einschließlich Typüberprüfung, Grenzwertvalidierung, Durchsetzung von Enumerationen und Ablehnung nicht erkannter oder übergroßer Parameter.                                                 |   2   |  D/V  |

---

## C10.5 Ausgehender Zugriff und Sicherheit bei der Agentenausführung

|   #    | Beschreibung                                                                                                                                                                                                                                                                               | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 10.5.1 | Stellen Sie sicher, dass MCP-Server nur ausgehende Anfragen an genehmigte interne oder externe Ziele gemäß den Prinzipien der geringsten Privilegien für den Ausgangsverkehr initiieren dürfen und keinen Zugriff auf beliebige Netzwerkknoten oder interne Cloud-Metadaten-Dienste haben. |   2   |  D/V  |
| 10.5.2 | Stellen Sie sicher, dass ausgehende MCP-Aktionen Ausführungslimits implementieren (z. B. Timeouts, Rekursionsgrenzen, Gleichzeitigkeitsbegrenzungen oder Circuit Breaker), um unbegrenzte agentengesteuerte Werkzeugaufrufe oder kaskadierende Nebeneffekte zu verhindern.                 |   2   |  D/V  |

---

## C10.6 Transportbeschränkungen & Hochrisiko-Grenzkontrollen

|   #    | Beschreibung                                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 10.6.1 | Stellen Sie sicher, dass stdio-basierte MCP-Transporte auf ko-lokalisierte, Single-Process-Entwicklungsszenarien beschränkt sind und von Shell-Ausführung, Terminal-Injektion und Prozess-Erzeugungsfähigkeiten isoliert sind; stdio darf Netzwerk- oder Multi-Tenant-Grenzen nicht überschreiten.    |   3   |  D/V  |
| 10.6.2 | Stellen Sie sicher, dass MCP-Server nur Funktionen und Ressourcen bereitstellen, die auf der Positivliste stehen, und verbieten Sie dynamische Aufrufe, reflektive Invocationen oder die Ausführung von Funktionsnamen, die durch Benutzereingaben oder modellgesteuerte Eingaben beeinflusst werden. |   3   |  D/V  |
| 10.6.3 | Überprüfen Sie, dass Mandanten-Grenzen, Umgebungsgrenzen (z. B. Dev/Test/Prod) und Datenbereichsgrenzen auf der MCP-Ebene durchgesetzt werden, um die Entdeckung von Servern oder Ressourcen zwischen Mandanten oder Umgebungen zu verhindern.                                                        |   3   |  D/V  |

---

## Literaturverzeichnis

* [Model Context Protocol (MCP) Specification](https://modelcontextprotocol.io/)
* [NIST SP 800-207: Zero Trust Architecture](https://csrc.nist.gov/publications/detail/sp/800-207/final)

