---
ms.assetid: ''
title: Konfigurieren von Systemen für hohe Genauigkeit
description: Die Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde wesentlich verbessert.  Unter angemessenen Betriebsbedingungen können Systeme so konfiguriert werden, dass Sie eine Genauigkeit von 1 ms (Millisekunden) oder eine bessere Genauigkeit (in Bezug auf die UTC) erhalten.
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: b7cd256fdbbdbe7432e5b5d5b16254314132560f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405200"
---
# <a name="configuring-systems-for-high-accuracy"></a>Konfigurieren von Systemen für hohe Genauigkeit
>Gilt für: Windows Server 2016 und Windows 10, Version 1607 oder höher

Die Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde wesentlich verbessert.  Unter angemessenen Betriebsbedingungen können Systeme so konfiguriert werden, dass Sie eine Genauigkeit von 1 ms (Millisekunden) oder eine bessere Genauigkeit (in Bezug auf die UTC) erhalten.

Anhand der folgenden Anleitungen können Sie Ihre Systeme so konfigurieren, dass eine hohe Genauigkeit erzielt wird.  In diesem Artikel werden die folgenden Anforderungen behandelt:

- Unterstützte Betriebssysteme
- Systemkonfiguration 

> [!WARNING]
> **Vorherige Genauigkeits Ziele für Betriebssysteme**<br>
>Windows Server 2012 R2 und höher können nicht die gleichen hohen Genauigkeits Ziele erfüllen. Diese Betriebssysteme werden für hohe Genauigkeit nicht unterstützt.
>
>In diesen Versionen erfüllt der Windows-Zeit Dienst die folgenden Anforderungen:
>
> - Die erforderliche Zeit Genauigkeit wurde bereitgestellt, um die Authentifizierungsanforderungen der Kerberos-Version 5 zu erfüllen.
> - Bietet eine lose genaue Zeit für Windows-Clients und-Server, die mit einer allgemeinen Active Directory Gesamtstruktur verknüpft sind.
>
>Höhere Toleranzen in 2012 R2 und niedriger sind außerhalb der Entwurfs Spezifikation des Windows-Zeit Dienstanbieter.

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10-und Windows Server 2016-Standardkonfiguration

Während wir die Genauigkeit von bis zu 1 MS unter Windows 10 oder Windows Server 2016 unterstützen, benötigen die meisten Kunden keine sehr genaue Zeit.

Daher ist die **Standardkonfiguration** für die Erfüllung der gleichen Anforderungen wie für vorherige Betriebssysteme gedacht, für die Folgendes gilt:

- Geben Sie die erforderliche Zeit Genauigkeit an, um die Authentifizierungsanforderungen der Kerberos-Version 5 zu erfüllen.
- Geben Sie für Windows-Clients und-Server, die einer gemeinsamen Active Directory Gesamtstruktur angehören, eine lose Zeitangabe

## <a name="how-to-configure-systems-for-high-accuracy"></a>Konfigurieren von Systemen für hohe Genauigkeit

>[!IMPORTANT]
>**Hinweis zur Unterstützung von streng präzisen Systemen**<br>
> Die Zeit Genauigkeit umfasst die End-to-End-Verteilung der exakten Zeit zwischen der autorisierenden Zeit Quelle und dem Endgerät.  Alle Elemente, die assymetry in Messungen entlang dieses Pfades hinzufügen, wirken sich negativ auf die Genauigkeit aus, die auf Ihren Geräten erreicht werden kann.
>
>Aus diesem Grund haben wir die [Unterstützungs Grenze zum Konfigurieren des Windows-Zeit diensdienstanbieter für Umgebungen mit hoher Genauigkeit](support-boundary.md) dokumentiert, in denen die Umgebungs Anforderungen beschrieben werden, die ebenfalls erfüllt sein müssen, um hochwertige Ziele zu erreichen.

### <a name="operating-system-requirements"></a>Betriebssystemanforderungen

Konfigurationen mit hoher Genauigkeit erfordern Windows 10 oder Windows Server 2016.  Alle Windows-Geräte in der Zeit Topologie müssen diese Anforderung erfüllen, einschließlich der höheren Windows-Zeitserver und der Hyper-V-Hosts, auf denen die Zeit empfindlichen virtuellen Maschinen ausgeführt werden. Alle diese Geräte müssen mindestens Windows 10 oder Windows Server 2016 sein.

In der unten gezeigten Abbildung werden die virtuellen Computer, die eine hohe Genauigkeit erfordern, Windows 10 oder Windows Server 2016 ausführen.  Ebenso muss der Hyper-V-Host, auf dem sich die virtuellen Computer befinden, und der Upstream-Windows-Zeitserver auch Windows Server 2016 ausführen.

![Zeit Topologie-1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Ermitteln der Windows-Version**<br>
> Sie können den Befehl `winver` an einer Eingabeaufforderung ausführen, um zu überprüfen, ob die Betriebssystemversion 1607 (oder höher) und der OS-Build 14393 (oder höher) ist, wie unten dargestellt:
>
> ![Winver-2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>Systemkonfiguration

Das erreichen von Zielen mit hoher Genauigkeit erfordert eine Systemkonfiguration.  Es gibt eine Vielzahl von Möglichkeiten, diese Konfiguration auszuführen, einschließlich direkt in der Registrierung oder über die Gruppenrichtlinie.  Weitere Informationen zu den einzelnen Einstellungen finden Sie in der technischen Referenz für den Windows-Zeit Dienst – [Windows-Zeit Dienst Tools](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools).

#### <a name="windows-time-service-startup-type"></a>Starttyp für Windows-Zeit Dienst

Der Windows-Zeit Dienst (W32Time) muss fortlaufend ausgeführt werden.  Zu diesem Zweck konfigurieren Sie den Starttyp des Windows-Zeit diensdienstanbieter auf "automatisch starten".

![Automatische Konfiguration](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>Kumulative unidirektionale Netzwerk Latenz

Messung der Messung und "Rauschen" bei steigender Netzwerk Latenz.  Daher ist es zwingend erforderlich, dass eine Netzwerk Latenz innerhalb einer angemessenen Grenze liegt.  Die spezifischen Anforderungen sind von der Zielgenauigkeit abhängig und werden im Artikel [unterstützte Grenzen zum Konfigurieren des Windows-Zeit Dienstanbieter für hochwertige Umgebungen](support-boundary.md) beschrieben.

Fügen Sie zum Berechnen der kumulativen unidirektionalen Netzwerk Latenz die einzelnen unidirektionalen Verzögerungen zwischen Paaren von NTP-Client-Server-Knoten in der Zeit Topologie hinzu, beginnend mit dem Ziel und enden bei der hochpräzisen Stratum 1-Zeit Quelle.

Zum Beispiel: Stellen Sie sich eine Zeit Synchronisierungs Hierarchie mit einer äußerst exakten Quelle, zwei zwischengeschalteten NTP-Servern a und B sowie den Zielcomputer in dieser Reihenfolge vor. Um die kumulative Netzwerk Latenz Zwischenziel und Quelle zu ermitteln, Messen Sie die durchschnittlichen einzelnen NTP-Roundtrip-Zeiten (RTTS) zwischen den folgenden Werten:

- Der Ziel-und Uhrzeit Server B
- Zeitserver B und Zeitserver a
- Zeitserver A und die Quelle

Diese Messung kann mithilfe des Posteingangs Tools W32tm. exe abgerufen werden.  Gehen Sie dazu wie folgt vor:

1. Führen Sie die Berechnung auf dem Ziel-und Uhrzeit Server B aus.
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. Führen Sie die Berechnung von Time Server b mit (gezeigt durch) Zeitserver a aus.
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. Führen Sie die Berechnung von Time Server a für die Quelle aus.
 
4. Fügen Sie als nächstes die durchschnittliche roundtripdelay hinzu, die im vorherigen Schritt gemessen wurde, und Dividieren Sie durch 2, um die kumulative Netzwerkverzögerung Zwischenziel und Quelle zu erhalten.

#### <a name="registry-settings"></a>Registrierungseinstellungen

# <a name="minpollintervaltabminpollinterval"></a>[Minpollinterval](#tab/MinPollInterval)
Konfiguriert das kleinste Intervall in log2 Sekunden, das für den System Abruf zulässig ist.

|  |  | 
|---------|---------|
|Schlüssel Speicherort     | HKLM: \ system\currentcontrolset\services\w32time\config        |
|Einstellung    | 6        |
|Ergebnis | Das minimale Abruf Intervall beträgt nun 64 Sekunden. |

Der folgende Befehl signalisiert der Windows-Zeit, die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`


# <a name="maxpollintervaltabmaxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
Konfiguriert das größte Intervall in log2 Sekunden, das für den System Abruf zulässig ist.

|  |  |  
|---------|---------|
|Schlüssel Speicherort     | HKLM: \ system\currentcontrolset\services\w32time\config        |
|Einstellung    | 6        |
|Ergebnis | Das maximale Abruf Intervall beträgt nun 64 Sekunden.  |

Der folgende Befehl signalisiert der Windows-Zeit, die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`

# <a name="updateintervaltabupdateinterval"></a>[Updateingeterval](#tab/UpdateInterval)
Die Anzahl der Takt Intervalle zwischen den Phasenkorrektur Anpassungen.

|  |  |  
|---------|---------|
|Schlüssel Speicherort     | HKLM: \ system\currentcontrolset\services\w32time\config       |
|Einstellung    | 100        |
|Ergebnis | Die Anzahl der Takt Einheiten zwischen den Anpassungen der Phasenkorrektur beträgt nun 100 Ticks. |

Der folgende Befehl signalisiert der Windows-Zeit, die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`

# <a name="specialpollintervaltabspecialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
Konfiguriert das Abruf Intervall in Sekunden, wenn das SpecialInterval-Flag 0x1 aktiviert ist.

|  |  |  
|---------|---------|
|Schlüssel Speicherort     | HKLM: \ system\currentcontrolset\services\w32time\timeproviders\ntpclient        |
|Einstellung    | 64        |
|Ergebnis | Das Abruf Intervall beträgt nun 64 Sekunden. |

Mit dem folgenden Befehl wird die Windows-Zeit neu gestartet, um die aktualisierten Einstellungen zu übernehmen:

`net stop w32time && net start w32time`

# <a name="frequencycorrectratetabfrequencycorrectrate"></a>[Frequendcycorrectrate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|Schlüssel Speicherort     | HKLM: \ system\currentcontrolset\services\w32time\config      |
|Einstellung    | 2        |


---
