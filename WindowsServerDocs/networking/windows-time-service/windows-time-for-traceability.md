---
ms.assetid: ''
title: Windows-Zeit für die Rückverfolgbarkeit
description: Für Vorschriften in vielen Sektoren ist es erforderlich, dass Systeme für die UTC in der UTC-  Dies bedeutet, dass der Offset eines Systems in Bezug auf die UTC bestätigt werden kann.
author: shortpatti
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 161188eccdd848cf50be1a4485beeb58935f643a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871777"
---
# <a name="windows-time-for-traceability"></a>Windows-Zeit für die Rückverfolgbarkeit
>Gilt für: Windows Server 2016 Version 1709 oder höher und Windows 10, Version 1703 oder höher


Für Vorschriften in vielen Sektoren ist es erforderlich, dass Systeme für die UTC in der UTC-  Dies bedeutet, dass der Offset eines Systems in Bezug auf die UTC bestätigt werden kann.  Zum Aktivieren von Szenarien für die Einhaltung gesetzlicher Bestimmungen werden von Windows 10 (Version 1703 oder höher) und Windows Server 2016 (Version 1709 oder höher) neue Ereignisprotokolle bereitgestellt, um ein Bild aus der Perspektive des Betriebssystems bereitzustellen und ein Verständnis der Aktionen zu bilden, die auf die Systemuhr.  Diese Ereignisprotokolle werden fortlaufend für den Windows-Zeit Dienst generiert und können zur späteren Analyse überprüft oder archiviert werden.

Diese neuen Ereignisse ermöglichen es, die folgenden Fragen zu beantworten:

* Wurde die Systemuhr geändert
* Wurde die Taktfrequenz geändert.
* Wurde die Windows-Zeit Dienst Konfiguration geändert

## <a name="availability"></a>Verfügbarkeit

Diese Verbesserungen sind in Windows 10, Version 1703 oder höher, und Windows Server 2016, Version 1709 oder höher, enthalten.

## <a name="configuration"></a>Konfiguration

Zur Umsetzung dieses Features ist keine Konfiguration erforderlich.  Diese Ereignisprotokolle sind standardmäßig aktiviert und befinden sich in der Ereignisanzeige unter dem Channel **Applications and Services log\microsoft\windows\time-service\operational** .


## <a name="list-of-event-logs"></a>Liste der Ereignisprotokolle

Im folgenden Abschnitt werden die Ereignisse beschrieben, die für die Verwendung in nach Verfolgungs Szenarien protokolliert werden.

# <a name="257tab257"></a>[257](#tab/257)
Dieses Ereignis wird protokolliert, wenn der Windows-Zeit Dienst (W32Time) gestartet wird und Informationen zur aktuellen Zeit, zur aktuellen Takt Anzahl, zur Laufzeitkonfiguration, zu Zeit Anbietern und zur aktuellen Taktrate protokolliert.

|||
|---|---|
|Ereignisbeschreibung |Dienst Start |
|Details |Tritt beim Start von W32Time auf |
|Protokollierte Daten |<ul><li>Aktuelle Uhrzeit in UTC</li><li>Aktuelle Tick-Anzahl</li><li>W32Time-Konfiguration</li><li>Zeit Anbieter Konfiguration</li><li>Taktfrequenz</li></ul> |
|Drosselungs Mechanismus  |Keine Dieses Ereignis wird jedes Mal ausgelöst, wenn der Dienst gestartet wird. |

**Beispiel:**
```
W32time service has started at 2018-02-27T04:25:17.156Z (UTC), System Tick Count 3132937.
```

**Befehl:**

Diese Informationen können auch mithilfe der folgenden Befehle abgefragt werden:

*W32Time-und Zeit Anbieter Konfiguration*
```
w32tm.exe /query /configuration
```

*Taktfrequenz*
```
w32tm.exe /query /status /verbose
```


# <a name="258tab258"></a>[258](#tab/258)
Dieses Ereignis wird protokolliert, wenn der Windows-Zeit Dienst (W32Time) beendet wird und Informationen zur aktuellen Zeit und Takt Anzahl protokolliert.

|||
|---|---|
|Ereignisbeschreibung |Dienst Beendigung |
|Details |Tritt bei W32Time Herunterfahren auf. |
|Protokollierte Daten |<ul><li>Aktuelle Uhrzeit in UTC</li><li>Aktuelle Tick-Anzahl</li></ul> |
|Drosselungs Mechanismus  |Keine Dieses Ereignis wird jedes Mal ausgelöst, wenn der Dienst beendet wird. |

**Beispiel Text:** 
`W32time service is stopping at 2018-03-01T05:42:13.944Z (UTC), System Tick Count 6370250.`

# <a name="259tab259"></a>[259](#tab/259)
Dieses Ereignis protokolliert regelmäßig die aktuelle Liste der Zeitquellen und die gewählte Zeit Quelle.  Außerdem wird die aktuelle Takt Anzahl protokolliert.  Dieses Ereignis wird nicht jedes Mal ausgelöst, wenn sich eine Zeit Quelle ändert.  Andere Ereignisse, die später in diesem Dokument aufgeführt werden, stellen diese Funktionalität bereit.

|||
|---|---|
|Ereignisbeschreibung |Regelmäßiger NTP-Client Anbieter Status |
|Details |Liste der vom NTP-Client verwendeten Zeitquellen (n) |
|Protokollierte Daten |<ul><li>Verfügbare Zeitquellen</li><li>Der ausgewählte Verweis Zeitserver zum Zeitpunkt der Protokollierung.</li><li>Aktuelle Tick-Anzahl</li></ul>  |
|Drosselungs Mechanismus  |Wird alle 8 Stunden protokolliert. |

**Beispiel Text:** Periodischer Status des NTP-Client Anbieters:

Der NTP-Client empfängt Zeit Daten von den folgenden NTP-Servern:

Server1. fabrikam. com, 0x8 (NTP. m | 0x8 | [::]: 123-> [IPAddress]: 123) Server2. fabrikam. com, 0x8 (NTP. m | 0x8 | [::]: 123-> [IPAddress]: 123);  der ausgewählte Verweis Zeitserver lautet Server1. fabrikam. com, 0x8 (NTP. m | 0x8 | [::]: 123-> [IPAddress]: 123) (refid: 0x08d6648e63). System Takt Anzahl 13187937

**Befehl** Diese Informationen können auch mithilfe der folgenden Befehle abgefragt werden:

*Identifizieren von Peers*
`w32tm.exe /query /peers`

# <a name="260tab260"></a>[260](#tab/260)

|||
|---|---|
|Ereignisbeschreibung |Zeit Dienst Konfiguration und-Status |
|Details |W32Time protokolliert die Konfiguration und den Status in regelmäßigen Abständen. Dies entspricht dem Aufruf von:<br><br>`w32tm /query /configuration /verbose`<br>oder<br>`w32tm /query /status /verbose` |
|Drosselungs Mechanismus  |Wird alle 8 Stunden protokolliert. |

# <a name="261tab261"></a>[261](#tab/261)
Dadurch wird jede Instanz protokolliert, wenn die System Zeit mithilfe der SetSystemTime-API geändert wird.

|||
|---|---|
|Ereignisbeschreibung |System Zeit ist festgelegt |
|Drosselungs Mechanismus  |Keine<br><br>Dies sollte nur selten auf Systemen mit angemessener Zeitsynchronisierung erfolgen, und wir möchten diese bei jedem Auftreten protokollieren. Beim Protokollieren dieses Ereignisses wird die timejumpauditoffset-Einstellung ignoriert, da diese Einstellung dazu gedacht war, Ereignisse im Windows-System Ereignisprotokoll zu drosseln. |

# <a name="262tab262"></a>[262](#tab/262)

|||
|---|---|
|Ereignisbeschreibung |System Taktfrequenz angepasst |
|Details |Die System Taktfrequenz wird von W32Time ständig geändert, wenn die Uhr in der Synchronisierung geschlossen wird. Wir möchten "ziemlich bedeutende" Anpassungen an der Taktfrequenz erfassen, ohne das Ereignisprotokoll zu überschreiten. |
|Drosselungs Mechanismus  |Alle Takt Anpassungen unterhalb von timeanpassungs mentauditthreshold (min = 128 Teil pro Million, Standardwert = 800 Teil pro Million) werden nicht protokolliert.<br><br>2 ppm Änderung in der Taktfrequenz mit der aktuellen Granularität ergibt 120 μs/Sek. Änderung der Takt Genauigkeit.<br><br>Bei einem synchronisierten System liegt der Großteil der Anpassungen unter dieser Ebene. Wenn Sie eine genauere Nachverfolgung wünschen, kann diese Einstellung nach unten angepasst werden, oder Sie können PerfCounters verwenden, oder Sie können beides tun. |

# <a name="263tab263"></a>[263](#tab/263)

|||
|---|---|
|Ereignisbeschreibung |Ändern Sie die Zeit Dienst Einstellungen oder die Liste der geladenen Zeit Anbieter. |
|Details |Das erneute Lesen von W32Time-Einstellungen kann bewirken, dass bestimmte kritische Einstellungen im Arbeitsspeicher geändert werden, was sich auf die Gesamtgenauigkeit der Zeitsynchronisierung auswirken kann.<br><br>W32Time protokolliert jedes Vorkommen, wenn die Einstellungen erneut gelesen werden, wodurch sich die möglichen Auswirkungen auf die Zeitsynchronisierung ergeben. |
|Drosselungs Mechanismus  |Keine<br><br>Dieses Ereignis tritt nur auf, wenn ein Administrator-oder ein GP-Update die Zeit Anbieter ändert und dann W32Time auslöst. Wir möchten jede Instanz der Änderung von Einstellungen aufzeichnen. |


# <a name="264tab264"></a>[264](#tab/264)

|||
|---|---|
|Ereignisbeschreibung |Änderung der vom NTP-Client verwendeten Zeit Quelle (n) |
|Details |Der NTP-Client zeichnet ein Ereignis mit dem aktuellen Zustand der Zeitserver/Peers auf, wenn sich der Status eines Zeit Servers/Peers ändert (**ausstehende > Synchronisierung**, **Synchronisierungs > nicht erreichbar**oder andere Übergänge). |
|Drosselungs Mechanismus  |Maximale Häufigkeit – nur einmal alle 5 Minuten, um das Protokoll vor vorübergehenden Problemen und einer ungültigen Anbieter Implementierung zu schützen. |

# <a name="265tab265"></a>[265](#tab/265)

|||
|---|---|
|Ereignisbeschreibung |Änderungen an der Zeit Dienst Quelle oder der Stratum-Nummer |
|Details |W32Time Time Source und Stratum Number sind wichtige Faktoren bei der Zeit Rückverfolgbarkeit, und alle Änderungen an diesen müssen protokolliert werden. Wenn W32Time über keine Zeit Quelle verfügt und Sie nicht als zuverlässige Zeit Quelle konfiguriert haben, wird die Ankündigung als Zeitserver beendet, und Entwurfs bedingt Antworten auf Anforderungen mit einigen ungültigen Parametern. Dieses Ereignis ist wichtig, um die Statusänderungen in einer NTP-Topologie zu verfolgen. |
|Drosselungs Mechanismus  |Keine |


# <a name="266tab266"></a>[266](#tab/266)

|||
|---|---|
|Ereignisbeschreibung |Die erneute Synchronisierung der Zeit wird angefordert. |
|Details |Dieser Vorgang wird ausgelöst:<ul><li>Wenn Netzwerk Änderungen auftreten</li><li>System gibt aus dem verbundenen Standbymodus/Ruhezustand zurück</li><li>Wenn die Synchronisierung für einen längeren Zeitraum nicht durchgesetzt wurde</li><li>Administrator gibt den Resync-Befehl aus.</li></ul>Dieser Vorgang führt zu einem sofortigen Verlust der Genauigkeit für differenzierte Zeitsynchronisierung, da der NTP-Client seine Filter löscht. |
|Drosselungs Mechanismus  |Maximale Häufigkeit: alle 5 Minuten.<br><br>Es ist möglich, dass eine fehlerhafte Netzwerkkarte (oder ein schlechtes Skript) diesen Vorgang wiederholt auslöst und die Protokolle überlastet werden. Daher muss dieses Ereignis eingeschränkt werden.<br><br>Beachten Sie, dass die genaue Zeitsynchronisierung wesentlich mehr als 5 Minuten dauert und die Drosselung keine Informationen zum ursprünglichen Ereignis verliert, die zu einem Verlust der Zeit Genauigkeit geführt haben.  |

---
