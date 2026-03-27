# C8 Speicher, Einbettungen & Sicherheit von Vektor-Datenbanken

## Kontrollziel

Einbettungen und Vektorspeicher fungieren als semi-permanenter und permanenter „Speicher“ für KI-Systeme über Retrieval-Augmented Generation (RAG). Dieser Speicher kann zu einem hochriskanten Datensenke- und Datenexfiltrationspfad werden. Diese Kontrollfamilie härtet Speicherpipelines und Vektordatenbanken ab, sodass der Zugriff nach dem Prinzip der geringsten Privilegien erfolgt, Daten vor der Vektorisierung bereinigt werden, die Aufbewahrung explizit ist und Systeme widerstandsfähig gegen Einbettungsinversion, Mitgliedschaftsinferenz und Mandantenübergreifungen sind.

## C8.1 Zugriffskontrollen für Speicher- und RAG-Indizes

Durchsetzung von feingranularen Zugriffskontrollen und Geltendmachung des Umfangs zur Abfragezeit für jede Vektorsammlung.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                 | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 8.1.1 | Überprüfen Sie, ob Vektor-Einfüge-, Update-, Lösch- und Abfrageoperationen mit Steuerungen auf Namespace-/Sammlungs-/Dokumenten-Tags-Ebene (z. B. Mandanten-ID, Benutzer-ID, Datenklassifizierungslabels) durchgesetzt werden, und zwar mit einer Standard-Deny-Politik.                                     |   1   |  D/V  |
| 8.1.2 | Überprüfen Sie, ob die für Vektoroperationen verwendeten API-Anmeldedaten über eingeschränkte Berechtigungen verfügen (z. B. zulässige Sammlungen, erlaubte Aktionen, Mandantenbindung).                                                                                                                     |   1   |  D/V  |
| 8.1.3 | Stellen Sie sicher, dass Zugriffsversuche über verschiedene Bereiche hinweg (z. B. Ähnlichkeitsabfragen über verschiedene Mandanten, Namespace-Durchquerung, Umgehung von Tags) erkannt und abgelehnt werden.                                                                                                |   2   |  D/V  |
| 8.1.4 | Stellen Sie sicher, dass jedes eingelesene Dokument beim Schreiben mit Quelle, Verfasseridentität (authentifizierter Benutzer oder Systemprinzipal), Zeitstempel, Batch-ID und Version des Einbettungsmodells gekennzeichnet wird und dass diese Markierungen nach dem ersten Schreiben unveränderlich sind. |   1   |  D/V  |

## C8.2 Einbettungsbereinigung und Validierung

Inhalte vor der Vektorisierung vorab überprüfen; Speicherzugriffe als nicht vertrauenswürdige Eingaben behandeln; Aufnahme unsicherer Nutzlasten verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                               | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 8.2.1 | Stellen Sie sicher, dass regulierte Daten und sensible Felder vor der Einbettung erkannt und entsprechend der Richtlinie maskiert, tokenisiert, transformiert oder entfernt werden.                                                                                                                                        |   1   |  D/V  |
| 8.2.2 | Stellen Sie sicher, dass die Einbettungserfassung Eingaben, die erforderliche Inhaltsbeschränkungen verletzen (z. B. nicht-UTF-8, fehlerhafte Codierungen, übergroße Nutzlasten, unsichtbare ASCII-Zeichen oder ausführbare Inhalte, die dazu bestimmt sind, die Abfrage zu vergiften), ablehnt oder in Quarantäne stellt. |   1   |  D/V  |
| 8.2.3 | Stellen Sie sicher, dass Vektoren, die außerhalb der normalen Clustermuster liegen, gekennzeichnet und isoliert werden, bevor sie in Produktionsindizes aufgenommen werden.                                                                                                                                                |   2   |  D/V  |
| 8.2.4 | Stellen Sie sicher, dass die eigenen Ausgaben eines Agenten nicht automatisch ohne explizite Validierung (wie Middleware-Hooks oder authentifizierende Handler auf Speicherebene, die den Ursprungsinhalt vor dem Schreiben prüfen) in seinen vertrauenswürdigen Speicher zurückgeschrieben werden.                        |   2   |  D/V  |
| 8.2.5 | Stellen Sie sicher, dass neue Inhalte, die in den Speicher geschrieben werden, auf Widersprüche mit bereits gespeicherten Inhalten überprüft werden und dass Konflikte Alarme auslösen.                                                                                                                                    |   2   |  D/V  |

## C8.3 Speicherablauf, Widerruf & Löschung

Die Aufbewahrung muss explizit und durchsetzbar sein; Löschungen müssen auf abgeleitete Indizes und Zwischenspeicher übertragen werden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                     | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 8.3.1 | Überprüfen Sie, ob Verweilzeiten auf jeden gespeicherten Vektor und die zugehörigen Metadaten im gesamten Speichersystem angewendet werden.                                                                                                                                                                                                                                      |   1   |  D/V  |
| 8.3.2 | Stellen Sie sicher, dass nur Informationen, die für die definierte Funktion des Systems erforderlich sind, im Speicher behalten werden (wie Benutzerpräferenzen und Gesprächsentscheidungen, jedoch keine Zugangsdaten oder vollständigen Gesprächstranskripte), und dass Kontext, der über die aktuelle Sitzung hinaus nicht benötigt wird, am Ende der Sitzung verworfen wird. |   1   |  D/V  |
| 8.3.3 | Überprüfen Sie, dass Löschanfragen Vektoren, Metadaten, zwischengespeicherte Kopien und abgeleitete Indizes innerhalb einer organisationsdefinierten maximalen Zeit löschen.                                                                                                                                                                                                     |   1   |  D/V  |
| 8.3.4 | Überprüfen Sie, dass gelöschte oder abgelaufene Vektoren zuverlässig entfernt werden und nicht wiederherstellbar sind.                                                                                                                                                                                                                                                           |   2   |   D   |
| 8.3.5 | Überprüfen Sie, dass abgelaufene Vektoren innerhalb eines gemessenen und überwachten Propagationsfensters von den Abruf-Ergebnissen ausgeschlossen werden.                                                                                                                                                                                                                       |   3   |  D/V  |
| 8.3.6 | Überprüfen Sie, dass der Speicher aus Sicherheitsgründen (Quarantäne, selektive Bereinigung, vollständiger Reset) getrennt von der Löschung zur Aufbewahrungsfrist zurückgesetzt werden kann und dass Inhalte in Quarantäne für Untersuchungen aufbewahrt, aber von der Abfrage ausgeschlossen werden.                                                                           |   2   |  D/V  |

## C8.4 Verhinderung von Einbettungsumkehr und Datenleckage

Adressierung von Adressinversion, Mitgliedschaftsinferenz und Attributinferenz mit expliziter Bedrohungsmodellierung, Gegenmaßnahmen und Regressionsprüfungsschritten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                   | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 8.4.1 | Stellen Sie sicher, dass sensible Vektor-Sammlungen durch technische Kontrollen wie Anwendungsschichtverschlüsselung, Umschlagverschlüsselung mit strengen KMS-Richtlinien oder gleichwertige kompensatorische Kontrollen vor dem direkten Lesezugriff durch Infrastrukturadministratoren geschützt sind.                      |   2   |  D/V  |
| 8.4.2 | Stellen Sie sicher, dass Datenschutz-/Nutzungsziele für die Widerstandsfähigkeit gegen Einbettungslecks definiert und gemessen werden und dass Änderungen an Einbettungsmodellen, Tokenizern, Such- oder Abrufeinstellungen oder Datenschutztransformationen durch Regressionsprüfungen gegen diese Ziele kontrolliert werden. |   3   |  D/V  |

## C8.5 Umfang der Durchsetzung für benutzerspezifischen Speicher

Verhindern Sie Datenlecks zwischen verschiedenen Mandanten und Benutzern bei der Datenabrufung und der Zusammenstellung von Eingabeaufforderungen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                    | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 8.5.1 | Stellen Sie sicher, dass jede Abrufoperation in der Vektormaschinenabfrage Geltungsbereichseinschränkungen (Mandant/Benutzer/Klassifizierung) durchsetzt und diese vor der Zusammenstellung des Prompts (Post-Filter) erneut überprüft.                                                         |   1   |  D/V  |
| 8.5.2 | Überprüfen Sie, ob Vektor-Identifikatoren, Namespaces und Metadatenindexierung Kreuzbereichskollisionen verhindern und die Einzigartigkeit pro Mandant durchsetzen.                                                                                                                             |   1   |   D   |
| 8.5.3 | Stellen Sie sicher, dass Abrufergebnisse, die den Ähnlichkeitskriterien entsprechen, aber die Bereichsprüfungen nicht bestehen, verworfen werden.                                                                                                                                               |   2   |  D/V  |
| 8.5.4 | Stellen Sie sicher, dass Multi-Mandanten-Tests adversarielle Abrufversuche (aufforderungsbasiert und abfragebasiert) simulieren und nachweisen, dass keine Dokumente außerhalb des Geltungsbereichs in Aufforderungen und Ausgaben enthalten sind.                                              |   2   |   V   |
| 8.5.5 | Überprüfen Sie, dass Verschlüsselungsschlüssel und Zugriffsrichtlinien für Speicher im Arbeitsspeicher/Vektor getrennt je Mandant verwaltet werden, um kryptografische Isolation in gemeinsam genutzter Infrastruktur zu gewährleisten.                                                         |   3   |  D/V  |
| 8.5.6 | Stellen Sie sicher, dass in Multi-Agenten-Systemen der Speicherbereich jedes Agenten isoliert ist und durch Zugriffskontrolle (wie zum Beispiel durch Scoped-Authentifizierungs-Handler oder Middleware-Validierung) durchgesetzt wird und nicht nur durch organisatorische Namenskonventionen. |   2   |  D/V  |

## Quellen (empfohlene Ergänzungen)

* OWASP Foundation. OWASP Top 10 für Anwendungen mit großen Sprachmodellen (LLM) 2025. https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-v2025.pdf

