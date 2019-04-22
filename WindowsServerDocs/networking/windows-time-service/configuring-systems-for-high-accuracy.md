---
ms.assetid: ''
title: Konfigurieren von Systemen für hohe Genauigkeit
description: Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde erheblich verbessert.  Unter betriebsbedingungen sinnvoll, Systeme zum Verwalten von 1 ms (Millisekunden) konfiguriert werden können Genauigkeit oder höher (in Bezug auf UTC).
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: d872252180d49bd41a91e9a8eaf516b834ed242a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814671"
---
# <a name="configuring-systems-for-high-accuracy"></a>Konfigurieren von Systemen für hohe Genauigkeit
>Gilt für: Windows Server 2016 und Windows 10 Version 1607 oder höher

Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde erheblich verbessert.  Unter betriebsbedingungen sinnvoll, Systeme zum Verwalten von 1 ms (Millisekunden) konfiguriert werden können Genauigkeit oder höher (in Bezug auf UTC).

Die folgende Anleitung helfen bei der Ihre Systeme mit hohen Genauigkeit erreichen zu konfigurieren.  In diesem Artikel werden die folgenden Anforderungen:

- Unterstützte Betriebssysteme
- Systemkonfiguration 

> [!WARNING]
> **Die Genauigkeit Ziele früheren Betriebssystemen**<br>
>Windows Server 2012 R2 und kann im folgenden nicht die gleichen hoher Genauigkeit Ziele erfüllen. Diese Betriebssysteme werden für die hohe Genauigkeit nicht unterstützt.
>
>Bei diesen Versionen erfüllt der Windows-Zeitdienst die folgenden Anforderungen:
>
> - Bereitgestellt, die lange Genauigkeit um Anforderungen an die Kerberos V5-Authentifizierung zu erfüllen.
> - Lose genaue Uhrzeit bereitgestellt für die Windows-Clients und Servern, die eingebunden in eine allgemeine Active Directory-Gesamtstruktur.
>
>Größere Toleranzen unter 2012 R2 und unten befinden sich außerhalb der Entwurfsspezifikation der Windows-Zeitdienst.

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10 und Windows Server 2016-Standardkonfiguration

Während wir die Genauigkeit bis zu 1 ms unter Windows 10 oder Windows Server 2016 unterstützt, die meisten Kunden benötigen keine äußerst präzise Zeit.

Daher ist es möglich, die **Standardkonfiguration** dient als früheren Betriebssystemen die gleichen Anforderungen erfüllen, wozu die sind:

- Geben Sie die Genauigkeit erforderlichen Zeit, um Anforderungen an die Kerberos V5-Authentifizierung zu erfüllen.
- Geben Sie Lose genaue Uhrzeit für die Windows-Clients und Server, die einen allgemeinen Active Directory-Gesamtstruktur angehören.

## <a name="how-to-configure-systems-for-high-accuracy"></a>Konfigurieren von Systemen für hohe Genauigkeit

>[!IMPORTANT]
>**Hinweis zu Unterstützungsmöglichkeiten für das äußerst präzise Systeme**<br>
> Genauigkeit der Zeit umfasst die End-to-End-Verteilung der genaue Uhrzeit aus der verbindlichen Zeitquelle, das Endgerät.  Alle Elemente, die hinzugefügt wird, dass Assymetry in Messungen entlang dieses Pfads Genauigkeit negativ beeinflussen wirkt sich die Genauigkeit, die auf Ihren Geräten erreicht.
>
>Aus diesem Grund haben wir dokumentiert die [Unterstützung Grenze so konfigurieren Sie den Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](support-boundary.md) Gliederung der umgebungsanforderungen, die ebenfalls erfüllt sein müssen, um hohe Genauigkeit Ziele zu erreichen.

### <a name="operating-system-requirements"></a>Betriebssystemanforderungen

Hohe Genauigkeit-Konfigurationen erfordern, dass Windows 10 oder Windows Server 2016.  Alle Windows-Geräte in der Topologie Zeit erfüllt diese Anforderung, einschließlich der höheren Stratum Windows Time-Server, und in virtualisierte Szenarien, die Hyper-V-Hosts, auf denen die zeitkritische virtuellen Computer ausgeführt. Alle diese Geräte muss mindestens Windows 10 oder Windows Server 2016.

In der Abbildung unten sind die virtuellen Computer, die hohen Genauigkeit erfordern Windows 10 oder Windows Server 2016 ausgeführt.  Ebenso müssen die Hyper-V-Host, auf denen die virtuellen Computer befinden, und dem Upstreamserver der Zeit von Windows auch Windows Server 2016 ausführen.

![Time-Topologie – 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Bestimmen der Windows-Version**<br>
> Sie können den Befehl ausführen `winver` an einer Eingabeaufforderung aus, um zu überprüfen, ob das Betriebssystem Version 1607 (oder höher), OS Build 14393 (oder höher) wie unten dargestellt:
>
> ![Winver - 2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>Systemkonfiguration

Hohe Genauigkeit Ziele zu erreichen, ist die Systemkonfiguration erforderlich.  Es gibt eine Vielzahl von Möglichkeiten zum Ausführen dieser Konfiguration, einschließlich direkt in der Registrierung oder über Gruppenrichtlinien.  Weitere Informationen für jede dieser Einstellungen finden Sie in der Windows-Dienst technische Referenz zur – [Windows-Zeitdienst: Tools](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools).

#### <a name="windows-time-service-startup-type"></a>Windows-Zeitdienst Starttyp

Der Windows-Zeitdienst (W32Time) muss kontinuierlich ausgeführt.  Zu diesem Zweck konfigurieren Sie den Windows-Zeitdienst Starttyp "Automatisch" starten.

![Automatische Konfiguration](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>Kumulative unidirektionale Netzwerklatenz

Messung Unsicherheit und das "Rauschen durch" ausgeprägte im Netzwerk Latenz zunimmt.  Daher ist es zwingend erforderlich, dass eine Netzwerklatenz innerhalb einer angemessenen Grenze sein.  Die spezifischen Anforderungen sind abhängig von Ihrem Ziel Genauigkeit und sind die [Unterstützung Grenze so konfigurieren Sie den Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](support-boundary.md) Artikel.

Fügen Sie zum Berechnen der kumulative unidirektionale Netzwerklatenz die einzelne unidirektionale Verzögerungen zwischen Paaren von NTP-Client / Server-Knoten in der Time-Topologie, beginnend mit dem Ziel, und endet bei der High-Genauigkeit Stratum 1 Zeitquelle hinzu.

Zum Beispiel: Erwägen Sie eine Zeithierarchie für die Synchronisierung mit der eine äußerst präzise Quelle, zwei zwischengeschaltete NTP-Server A und B und dem Zielcomputer in dieser Reihenfolge aus. Die kumulative Netzwerklatenz zwischen Ziel und Quelle zu erhalten, messen den durchschnittlichen einzelne NTP-Roundtrip zwischen ein Timeout (RTTs):

- Das Ziel und die Uhrzeit Server B
- , Zeitserver B und Zeit ein
- Time-Server A und der Quelle

Diese Messung kann mit dem Posteingang w32tm.exe Tool abgerufen werden.  Gehen Sie dazu wie folgt vor:
<!-- Use PowerShell to import the CSV then average the RTT Column -->

1. Die Berechnung auf dem Ziel und die Uhrzeit Server b ausführen.
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. Führen Sie die Berechnung von Zeit Server b gegen ein (zeigt auf) Zeitserver ein.
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. Führen Sie die Berechnung von Zeitserver eine für die Quelle aus.
 
4. Als Nächstes fügen Sie, dass die durchschnittliche RoundTripDelay im vorherigen Schritt gemessen und Division durch 2, um die kumulativen netzwerkverzögerung zwischen Quelle und Ziel zu erhalten.

#### <a name="registry-settings"></a>Registrierungseinstellungen

# <a name="minpollintervaltabminpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
Konfiguriert das kleinste Intervall in log2 Sekunden, die für den Abruf von System zulässig.

|  |  | 
|---------|---------|
|Speicherort des Schlüssels an     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|Einstellung    | 6        |
|Ergebnis | Das minimale Abrufintervall ist jetzt 64 Sekunden. |

Der folgende Befehl signalisiert Windows-Zeit, um die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`


# <a name="maxpollintervaltabmaxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
Konfiguriert das größte Intervall in log2 Sekunden, die für den Abruf von System zulässig.

|  |  |  
|---------|---------|
|Speicherort des Schlüssels an     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|Einstellung    | 6        |
|Ergebnis | Das maximale Abrufintervall ist jetzt 64 Sekunden.  |

Der folgende Befehl signalisiert Windows-Zeit, um die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`

# <a name="updateintervaltabupdateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
Die Anzahl der Zeiteinheiten zwischen Phase Korrektur Anpassungen.

|  |  |  
|---------|---------|
|Speicherort des Schlüssels an     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|Einstellung    | 100        |
|Ergebnis | Die Anzahl der Zeiteinheiten zwischen Phase Korrektur Anpassungen ist jetzt 100 Ticks. |

Der folgende Befehl signalisiert Windows-Zeit, um die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`

# <a name="specialpollintervaltabspecialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
Konfiguriert das Abrufintervall in Sekunden, wenn das SpecialInterval 0 x 1-Flag aktiviert ist.

|  |  |  
|---------|---------|
|Speicherort des Schlüssels an     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|Einstellung    | 64        |
|Ergebnis | Das Abrufintervall ist jetzt 64 Sekunden. |

Der folgende Befehl neu gestartet wird, Windows-Zeit, um die aktualisierten Einstellungen zu übernehmen:

`net stop w32time && net start w32time`

# <a name="frequencycorrectratetabfrequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|Speicherort des Schlüssels an     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|Einstellung    | 2        |


---
