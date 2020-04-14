---
title: Windows-Zeitdienst für Nachverfolgbarkeit.
description: Bestimmungen in vielen Sektoren erfordern, dass Systeme bezogen auf UTC ablaufverfolgbar sind.  Dies bedeutet, dass die Abweichung eines Systems in Bezug auf die UTC nachgewiesen werden kann.
author: dcuomo
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 30952c7a15109ccdd8bcbb09d7c8dda44f716d5d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859813"
---
# <a name="windows-time-for-traceability"></a>Windows-Zeitdienst für Nachverfolgbarkeit.
>Gilt für: Windows Server 2016, Version 1709 oder höher, und Windows 10, Version 1703 oder höher


Bestimmungen in vielen Sektoren erfordern, dass Systeme bezogen auf UTC ablaufverfolgbar sind.  Dies bedeutet, dass die Abweichung eines Systems in Bezug auf die UTC nachgewiesen werden kann.  Zum Aktivieren regulatorischer Complianceszenarien bieten Windows 10 (Version 1703 oder höher) und Windows Server 2016 (Version 1709 oder höher) neue Ereignisprotokolle, um ein Bild aus der Perspektive des Betriebssystems bereitzustellen und so ein Verständnis der an der Systemuhr vorgenommenen Aktionen zu erstellen.  Diese Ereignisprotokolle werden fortlaufend für den Windows-Zeitdienst generiert und können untersucht sowie zur späteren Analyse archiviert werden.

Diese neuen Ereignisse ermöglichen die Beantwortung der folgenden Fragen:

* Wurde die Systemuhr verändert?
* Wurde die Taktfrequenz geändert?
* Wurde die Konfiguration des Windows-Zeitdiensts geändert?

## <a name="availability"></a>Verfügbarkeit

Diese Verbesserungen sind in Windows 10, Version 1703 oder höher, und Windows Server 2016, Version 1709 oder höher, enthalten.

## <a name="configuration"></a>Konfiguration

Zur Verwendung dieser Funktion ist keine Konfiguration erforderlich.  Diese Ereignisprotokolle sind standardmäßig aktiviert und befinden sich in der Ereignisanzeige unter dem Kanal **Anwendungs- und Dienstprotokolle\Microsoft\Windows\Time-Service\Operational**.


## <a name="list-of-event-logs"></a>Liste der Ereignisprotokolle

Im folgenden Abschnitt werden die Ereignisse beschrieben, die für die Verwendung in Ablaufverfolgungsszenarien protokolliert werden.

# <a name="257"></a>[257](#tab/257)
Dieses Ereignis wird protokolliert, wenn der Windows-Zeitdienst (W32Time) gestartet wird und Informationen zur aktuellen Zeit, zur aktuellen Taktanzahl, zur Laufzeitkonfiguration, zu Zeitanbietern und zur aktuellen Taktfrequenz protokolliert.

|||
|---|---|
|Ereignisbeschreibung |Dienststart |
|Details |Tritt beim Start von W32Time auf. |
|Protokollierte Daten |<ul><li>Aktuelle Zeit in UTC</li><li>Aktuelle Taktanzahl</li><li>W32Time-Konfiguration</li><li>Zeitanbieterkonfiguration</li><li>Taktfrequenz</li></ul> |
|Drosselungsmechanismus  |Keine. Dieses Ereignis wird bei jedem Start des Diensts ausgelöst. |

**Beispiel:**
```
W32time service has started at 2018-02-27T04:25:17.156Z (UTC), System Tick Count 3132937.
```

**Befehl:**

Diese Informationen können auch mithilfe der folgenden Befehle abgefragt werden.

*W32Time- und Zeitanbieterkonfiguration*
```
w32tm.exe /query /configuration
```

*Taktfrequenz*
```
w32tm.exe /query /status /verbose
```


# <a name="258"></a>[258](#tab/258)
Dieses Ereignis wird protokolliert, wenn der Windows-Zeitdienst (W32Time) beendet wird und Informationen zur aktuellen Zeit und Taktanzahl protokolliert.

|||
|---|---|
|Ereignisbeschreibung |Beendigung des Diensts |
|Details |Tritt beim Herunterfahren von W32Time auf. |
|Protokollierte Daten |<ul><li>Aktuelle Zeit in UTC</li><li>Aktuelle Taktanzahl</li></ul> |
|Drosselungsmechanismus  |Keine. Dieses Ereignis wird bei jedem Beenden des Diensts ausgelöst. |

**Beispieltext:** 
`W32time service is stopping at 2018-03-01T05:42:13.944Z (UTC), System Tick Count 6370250.`

# <a name="259"></a>[259](#tab/259)
Dieses Ereignis protokolliert regelmäßig die aktuelle Liste der Zeitquellen und die ausgewählte Zeitquelle.  Zusätzlich wird die aktuelle Taktanzahl protokolliert.  Dieses Ereignis wird nicht bei jeder Zeitquellenänderung ausgelöst.  Andere Ereignisse, die später in diesem Dokument aufgeführt sind, bieten diese Funktionalität.

|||
|---|---|
|Ereignisbeschreibung |Regelmäßiger Status des NTP-Clientanbieters |
|Details |Liste der vom NTP-Client verwendeten Zeitquellen |
|Protokollierte Daten |<ul><li>Verfügbare Zeitquellen</li><li>Der ausgewählte Referenzzeitserver zum Zeitpunkt der Protokollierung</li><li>Aktuelle Taktanzahl</li></ul>  |
|Drosselungsmechanismus  |Wird alle 8 Stunden einmal protokolliert. |

**Beispieltext:** Regelmäßiger Status des NTP-Clientanbieters:

Der NTP-Client empfängt Zeitdaten von den folgenden NTP-Servern:

server1.fabrikam.com,0x8 (ntp.m|0x8|[::]:123->[IPAddress]:123)server2.fabrikam.com,0x8 (ntp.m|0x8|[::]:123->[IPAddress]:123); und der ausgewählte Referenzzeitserver ist Server1.fabrikam.com,0x8 (ntp.m|0x8|[::]:123->[IPAddress]:123) (RefID:0x08d6648e63). Aktuelle Taktanzahl 13.187.937

**Befehl** Diese Informationen können auch mithilfe der folgenden Befehle abgefragt werden.

*Peers identifizieren*
`w32tm.exe /query /peers`

# <a name="260"></a>[260](#tab/260)

|||
|---|---|
|Ereignisbeschreibung |Konfiguration und Status des Zeitdiensts |
|Details |W32Time protokolliert regelmäßig seine Konfiguration und seinen Status. Dies entspricht dem Aufrufen von:<br><br>`w32tm /query /configuration /verbose`<br>oder<br>`w32tm /query /status /verbose` |
|Drosselungsmechanismus  |Wird alle 8 Stunden einmal protokolliert. |

# <a name="261"></a>[261](#tab/261)
Dies protokolliert jede Instanz, wenn die Systemzeit mithilfe der SetSystemTime-API geändert wird.

|||
|---|---|
|Ereignisbeschreibung |Systemzeit wird gestellt. |
|Drosselungsmechanismus  |Keine.<br><br>Dies sollte nur selten auf Systemen mit angemessener Zeitsynchronisierung erfolgen, und wir möchten dies bei jedem Auftreten protokollieren. Wir ignorieren die Einstellung „TimeJumpAuditOffset“ beim Protokollieren dieses Ereignisses, da diese Einstellung zum Drosseln von Ereignissen im Windows-Systemereignisprotokoll gedacht war. |

# <a name="262"></a>[262](#tab/262)

|||
|---|---|
|Ereignisbeschreibung |Systemtaktfrequenz angepasst |
|Details |Die Systemtaktfrequenz wird von W32Time konstant geändert, wenn die Uhr eng synchronisiert wird. Wir möchten „hinreichend signifikante“ Anpassungen erfassen, die an der Taktfrequenz vorgenommen werden, ohne das Ereignisprotokoll zu überfüllen. |
|Drosselungsmechanismus  |Alle Taktanpassungen unterhalb von „TimeAdjustmentAuditThreshold“ (Minimum = 128 ppm (Teile pro Mio.), Standardwert = 800 ppm) werden nicht protokolliert.<br><br>Eine 2 ppm-Änderung der Taktfrequenz mit der aktuellen Granularität ergibt eine 120 μs/Sek.-Änderung der Taktgenauigkeit.<br><br>Bei einem synchronisierten System liegt der Großteil der Anpassungen unterhalb dieses Niveaus. Wenn du eine genauere Nachverfolgung wünschst, kann diese Einstellung nach unten angepasst werden, oder du kannst Leistungsindikatoren verwenden oder beides. |

# <a name="263"></a>[263](#tab/263)

|||
|---|---|
|Ereignisbeschreibung |Änderung der Zeitdiensteinstellungen oder Auflisten der geladenen Zeitanbieter. |
|Details |Das erneute Lesen von W32Time-Einstellungen kann bewirken, dass bestimmte kritische Einstellungen im Arbeitsspeicher geändert werden, was sich wiederum auf die Gesamtgenauigkeit der Zeitsynchronisierung auswirken kann.<br><br>W32Time protokolliert jedes Vorkommen, wenn es seine Einstellungen erneut liest, woraus sich die potenziellen Auswirkungen auf die Zeitsynchronisierung ergeben. |
|Drosselungsmechanismus  |Keine.<br><br>Dieses Ereignis tritt nur auf, wenn ein Administrator oder eine Gruppenrichtlinienaktualisierung die Zeitanbieter ändert und dann W32Time auslöst. Wir möchten jede Instanz einer Änderung von Einstellungen aufzeichnen. |


# <a name="264"></a>[264](#tab/264)

|||
|---|---|
|Ereignisbeschreibung |Änderung an vom NTP-Client verwendeten Zeitquellen |
|Details |Der NTP-Client zeichnet ein Ereignis mit dem aktuellen Zustand der Zeitserver/Peers auf, wenn sich der Zustand eines Zeitservers/Peers ändert (**Ausstehend > Synchronisierung**, **Synchronisierung > Nicht erreichbar** oder andere Übergänge). |
|Drosselungsmechanismus  |Maximale Häufigkeit: nur einmal alle 5 Minuten, um das Protokoll vor vorübergehenden Problemen und einer fehlerhaften Anbieterimplementierung zu schützen. |

# <a name="265"></a>[265](#tab/265)

|||
|---|---|
|Ereignisbeschreibung |Änderungen an der Zeitdienstquelle oder Stratumnummer |
|Details |Zeitquelle und Stratumnummer von W32Time sind wichtige Faktoren der Zeitablaufverfolgbarkeit, und alle Änderungen daran müssen protokolliert werden. Wenn W32Time über keine Zeitquelle verfügt und Sie es nicht als zuverlässige Zeitquelle konfiguriert haben, beendet es die Ankündigung als Zeitserver und antwortet entwurfsbedingt auf Anforderungen mit einigen ungültigen Parametern. Dieses Ereignis ist kritisch, um die Zustandsänderungen in einer NTP-Topologie zu verfolgen. |
|Drosselungsmechanismus  |Keine. |


# <a name="266"></a>[266](#tab/266)

|||
|---|---|
|Ereignisbeschreibung |Erneute Synchronisierung der Zeit wird angefordert |
|Details |Dieser Vorgang wird in folgenden Fällen ausgelöst:<ul><li>Netzwerkänderungen</li><li>Rückkehr des Systems aus dem verbundenen Standbymodus/Ruhezustand</li><li>Es wurde länger keine Synchronisierung vorgenommen.</li><li>Administrator sendet den resync-Befehl.</li></ul>Dieser Vorgang führt zu einem sofortigen Verlust der fein aufgelösten Zeitsynchronisierungsgenauigkeit, da der NTP-Client dadurch seine Filter löscht. |
|Drosselungsmechanismus  |Max. Häufigkeit: einmal alle 5 Minuten.<br><br>Es ist möglich, dass eine fehlerhafte Netzwerkkarte (oder ein schlecht geschriebenes Skript) diesen Vorgang wiederholt auslöst und dies zum Überlaufen der Protokolle führt. Hieraus resultiert die Notwendigkeit zur Drosselung dieses Ereignisses.<br><br>Beachte, dass es wesentlich länger als 5 Minuten dauert, um die genaue Zeitsynchronisierung zu erzielen, und bei der Drosselung gehen keine Informationen zum ursprünglichen Ereignis verloren, das zum Verlust der Zeitgenauigkeit geführt hat.  |

---
