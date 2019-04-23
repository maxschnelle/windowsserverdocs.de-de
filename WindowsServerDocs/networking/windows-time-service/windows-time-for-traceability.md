---
ms.assetid: ''
title: Windows Time zur nachverfolgung
description: In vielen Bereichen geltender werden Systeme in UTC zurückverfolgt werden.  Dies bedeutet, dass es sich bei eines Systems Offset in Bezug auf UTC nachgewiesen werden kann.
author: shortpatti
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: e25217feba45516cd0e9a3aa2bf1a2581d2087f5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838041"
---
# <a name="windows-time-for-traceability"></a>Windows Time zur nachverfolgung
>Gilt für: Windows Server 2016 Version 1709 oder höher und Windows 10 Version 1703 oder höher


In vielen Bereichen geltender werden Systeme in UTC zurückverfolgt werden.  Dies bedeutet, dass es sich bei eines Systems Offset in Bezug auf UTC nachgewiesen werden kann.  Um die Einhaltung gesetzlicher Bestimmungen Szenarien zu ermöglichen, bietet Windows 10 (Version 1703 oder höher) und Windows Server 2016 (Version 1709 oder höher) neuen Ereignisprotokolle, geben Sie ein Bild aus der Perspektive des Betriebssystems, um einen Überblick über die ausgeführten Aktionen zu bilden. die Systemuhr.  Diese Ereignisprotokolle kann werden kontinuierlich für Windows-Zeitdienst generiert und überprüft oder zur späteren Analyse archiviert werden.

Diese neuen Ereignisse aktivieren Sie die folgenden Fragen beantwortet werden:

* Die Systemuhr wurde geändert werden
* Die Taktfrequenz wurde geändert werden
* Konfiguration der Windows-Dienst wurde geändert werden

## <a name="availability"></a>Verfügbarkeit

Diese Verbesserungen sind in Windows 10 Version 1703 oder höher und Windows Server 2016 Version 1709 oder höher enthalten.

## <a name="configuration"></a>Konfiguration

Es ist keine Konfiguration erforderlich, um dieses Feature zu nutzen.  Diese Ereignisprotokolle sind standardmäßig aktiviert, und finden Sie in der Ereignisanzeige unter der **Anwendungen und Dienste Log\Microsoft\Windows\Time-Service\Operational** Kanal.


## <a name="list-of-event-logs"></a>Liste der Ereignisprotokolle

Im folgende Abschnitt wird beschrieben, für den Einsatz in den rückverfolgbarkeit protokollierten Ereignisse.

<!-- use tabs like the group policies -->
# <a name="257tab257"></a>[257](#tab/257)
Dieses Ereignis wird protokolliert, wenn der Windows-Zeitdienst (W32Time) gestartet wird, und Informationen über die aktuelle Uhrzeit, aktuelle Anzahl der Ticks, die Laufzeitkonfiguration, Zeitanbieter und aktuelle Taktfrequenz protokolliert.

|||
|---|---|
|Ereignisbeschreibung |Starten des Diensts |
|Details |Tritt beim Starten der W32time |
|Protokollierte Daten |<ul><li>Aktuelle Uhrzeit in UTC</li><li>Aktuelle Tickzähler</li><li>W32Time-Konfiguration</li><li>Anbieterkonfiguration für Zeit</li><li>Taktrate</li></ul> |
|Mechanismus zur moduleinschränkung  |Keine Dieses Ereignis wird ausgelöst, jedes Mal, wenn der Dienst gestartet wird. |

**Beispiel:**
```
W32time service has started at 2018-02-27T04:25:17.156Z (UTC), System Tick Count 3132937.
```

**Befehl:**

Diese Informationen kann auch mithilfe der folgenden Befehle abgefragt werden

*W32Time und Zeitanbieter-Konfiguration*
```
w32tm.exe /query /configuration
```

*Taktrate*
```
w32tm.exe /query /status /verbose
```


# <a name="258tab258"></a>[258](#tab/258)
Dieses Ereignis wird protokolliert, wenn der Windows-Zeitdienst (W32Time) wird beendet, und Informationen über die aktuelle Uhrzeit und -Tick-Anzahl protokolliert.

|||
|---|---|
|Ereignisbeschreibung |Beenden des Diensts |
|Details |Tritt auf, beim Herunterfahren der W32time |
|Protokollierte Daten |<ul><li>Aktuelle Uhrzeit in UTC</li><li>Aktuelle Tickzähler</li></ul> |
|Mechanismus zur moduleinschränkung  |Keine Dieses Ereignis wird ausgelöst, jedes Mal, wenn der Dienst beendet wird. |

**Beispieltext:**
`W32time service is stopping at 2018-03-01T05:42:13.944Z (UTC), System Tick Count 6370250.`

# <a name="259tab259"></a>[259](#tab/259)
Dieses Ereignis protokolliert in regelmäßigen Abständen die aktuelle Liste der Zeitquellen und der angegebenen Quelle.  Darüber hinaus wird die aktuelle Anzahl der Ticks protokolliert.  Dieses Ereignis wird nicht jedes Mal ausgelöst, wenn eine Zeitquelle ändert.  Andere Ereignisse, die weiter unten in diesem Dokument werden diese Funktionen bereitstellen.

|||
|---|---|
|Ereignisbeschreibung |NTP-Client-Anbieter periodische Status |
|Details |Liste der Zeitquellen (s) NTP-Client verwendet |
|Protokollierte Daten |<ul><li>Zeitpunkt der Verfügbarkeit der Quellen</li><li>Der ausgewählte Verweis Zeitserver zum Zeitpunkt der Protokollierung</li><li>Aktuelle Tickzähler</li></ul>  |
|Mechanismus zur moduleinschränkung  |Protokolliert alle 8 Stunden. |

**Beispieltext:** Periodische Status des NTP-Client-Anbieter:

NTP-Client erhält die Zeitdaten über die folgenden NTP-Server:

server1.Fabrikam.com, 0 x 8 (ntp.m|0x8|[::]:123 -> [IPAddress]:123)server2.fabrikam.com,0x8 (ntp.m|0x8|[::]:123 -> [IP-Adresse]: 123);  und der ausgewählte Verweis Zeitserver Server1.fabrikam.com,0x8 (ntp.m|0x8|[::]:123 -> [IP-Adresse]: 123) (RefID:0x08d6648e63). System-Taktanzahl 13187937

**Befehl** diese Informationen können auch mithilfe der folgenden Befehle abgefragt werden

*Identifizieren von Peers*
`w32tm.exe /query /peers`

# <a name="260tab260"></a>[260](#tab/260)

|||
|---|---|
|Ereignisbeschreibung |Dienstkonfiguration für die Uhrzeit und status |
|Details |W32Time-Protokolle in regelmäßigen Abständen die Konfigurations- und Statusinformationen. Dies ist das Äquivalent eines Aufrufs:<br><br>`w32tm /query /configuration /verbose`<br>ODER<br>`w32tm /query /status /verbose` |
|Mechanismus zur moduleinschränkung  |Protokolliert alle 8 Stunden. |

# <a name="261tab261"></a>[261](#tab/261)
Diese protokolliert jede Instanz, wenn Systemzeit mit SetSystemTime-API geändert wird.

|||
|---|---|
|Ereignisbeschreibung |Systemzeit festgelegt ist |
|Mechanismus zur moduleinschränkung  |Keine<br><br>Geschieht dies sollte nur selten auf Systemen mit angemessener zeitsynchronisierung und soll es jedes Mal protokolliert, wenn er vorkommt. Wir ignorieren TimeJumpAuditOffset-Einstellung bei der Protokollierung dieses Ereignis aus, da diese Einstellung bestimmt waren, Drosseln von Ereignissen im Ereignisprotokoll Windows-System. |

# <a name="262tab262"></a>[262](#tab/262)

|||
|---|---|
|Ereignisbeschreibung |System-Taktfrequenz angepasst |
|Details |System-Taktfrequenz wird ständig von W32time geändert, wenn die Uhr enge Synchronisierung wird. Wir möchten "Recht erhebliche" Anpassungen an der Taktfrequenz vorgenommen werden, ohne dass überschritten das Ereignisprotokoll zu erfassen. |
|Mechanismus zur moduleinschränkung  |Alle Anpassungen unter TimeAdjustmentAuditThreshold clock (min = 128 Teil pro million, Standard = 800 Teil pro million) werden nicht protokolliert.<br><br>Änderung 2 PPM Taktfrequenz mit aktuellen Granularität führt 120 µsek/Sekunde ändern Uhr Genauigkeit.<br><br>Bei einem synchronisierten System der Großteil der Anpassungen sind unterhalb dieser Stufe. Ggf. eine genauere nachverfolgung, diese Einstellung kann nach unten angepasst werden können Sie Leistungsindikatoren oder beides tun. |

# <a name="263tab263"></a>[263](#tab/263)

|||
|---|---|
|Ereignisbeschreibung |Ändern Sie in der Liste der geladenen Zeitanbieter "oder" Time-diensteinstellungen. |
|Details |Durch erneutes Lesen der W32time-Einstellungen kann dazu führen, dass bestimmte wichtigen Einstellungen geänderte im Arbeitsspeicher sein soll, die gesamtgenauigkeit des der Synchronisierung auswirken kann.<br><br>W32Time protokolliert jedes Vorkommen, wenn ein erneutes Lesen die Einstellungen, wodurch die potenzielle Auswirkungen auf die Synchronisierung. |
|Mechanismus zur moduleinschränkung  |Keine<br><br>Dieses Ereignis tritt nur dann, wenn ein Administrator oder gruppenrichtlinienaktualisierung ändert sich die Zeitanbieter und löst dann W32time. Jede Instanz der Änderung der Einstellungen aufzeichnen soll. |


# <a name="264tab264"></a>[264](#tab/264)

|||
|---|---|
|Ereignisbeschreibung |Ändern Sie in der Time-Quellen, die von NTP-Client verwendet |
|Details |NTP-Client zeichnet ein Ereignis mit dem aktuellen Status der Time-Server/Peers aus, wenn ein Zeit-Server/Peer Zustand ändert (**ausstehende Sync->**, **Sync -> nicht erreichbar**, oder andere Übergänge) |
|Mechanismus zur moduleinschränkung  |Max. Häufigkeit – nur einmal alle 5 Minuten auf vorübergehende Probleme und fehlerhafte anbieterimplementierung des Protokolls verhindern. |

# <a name="265tab265"></a>[265](#tab/265)

|||
|---|---|
|Ereignisbeschreibung |Time-Quelle oder das Stratum Anzahl dienständerungen |
|Details |W32Time-Zeitquelle und Stratum Anzahl sind wichtige Faktoren in Zeit nachverfolgbarkeit und alle Änderungen an diesen protokolliert werden müssen. Wenn W32time keinen Zeit hat und nicht als einer zuverlässigen Zeitquelle konfiguriert haben, dann wird die Ankündigung als einen Zeitserver angehalten, und standardmäßig reagieren auf Anforderungen mit einigen ungültigen Parametern. Dieses Ereignis ist entscheidend für die Änderungen des Ansichtszustands in einer NTP-Topologie zu verfolgen. |
|Mechanismus zur moduleinschränkung  |Keine |


# <a name="266tab266"></a>[266](#tab/266)

|||
|---|---|
|Ereignisbeschreibung |Erneute Synchronisierung wird angefordert. |
|Details |Dieser Vorgang wird ausgelöst:<ul><li>Wenn Änderungen am Netzwerk auftreten</li><li>Aus dem verbundenen Standby/Ruhezustand gibt System zurück.</li><li>Wenn wir einen längeren Zeitraum synchronisieren nicht</li><li>Administrator gibt den Resync-Befehl</li></ul>Dieser Vorgang führt zu unmittelbaren Genauigkeitsverlust differenzierte Zeitpunkt synchronisieren, da es sich bei NTP-Client, der Filter gelöscht wird. |
|Mechanismus zur moduleinschränkung  |Max. Häufigkeit - einmal alle 5 Minuten.<br><br>Es ist möglich, dass eine fehlerhafte Netzwerkkarte (oder ein Skript eine schlechte) dieser Vorgang wiederholt ausgelöst und Protokolle, die überlastet abrufen zu kann. Daher muss dieses Ereignis zu drosseln.<br><br>Beachten Sie, die genaue Uhrzeit Sync weit mehr als 5 Minuten erreichen akzeptiert und Einschränkung ist nicht verloren gehen Informationen über das ursprüngliche Ereignis, das der Genauigkeit der Zeit geführt haben.  |

---
