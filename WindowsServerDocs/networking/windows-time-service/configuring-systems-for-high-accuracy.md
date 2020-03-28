---
ms.assetid: ''
title: Konfigurieren von Systemen für hohe Genauigkeit
description: Die Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde erheblich verbessert.  Unter angemessenen Betriebsbedingungen können Systeme so konfiguriert werden, dass sie eine Genauigkeit von 1 ms (Millisekunden) oder besser (in Bezug auf die UTC) aufrechterhalten.
author: eross-msft
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 8cdded0eb0dc663d352011fb1a6765a2ed358764
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315034"
---
# <a name="configuring-systems-for-high-accuracy"></a>Konfigurieren von Systemen für hohe Genauigkeit
>Gilt für: Windows Server 2016 und Windows 10, Version 1607 oder höher

Die Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde erheblich verbessert.  Unter angemessenen Betriebsbedingungen können Systeme so konfiguriert werden, dass sie eine Genauigkeit von 1 ms (Millisekunden) oder besser (in Bezug auf die UTC) aufrechterhalten.

Anhand der folgenden Anleitungen kannst du deine Systeme so konfigurieren, dass eine hohe Genauigkeit erzielt wird.  In diesem Artikel werden die folgenden Anforderungen behandelt:

- Unterstützte Betriebssysteme
- Systemkonfiguration 

> [!WARNING]
> **Genauigkeitsziele früherer Betriebssysteme**<br>
>Windows Server 2012 R2 und niedriger können nicht dieselben hohen Genauigkeitsziele erfüllen. Diese Betriebssysteme werden nicht für hohe Genauigkeit unterstützt.
>
>In diesen Versionen erfüllt der Windows-Zeitdienst die folgenden Anforderungen:
>
> - hat die notwendige Zeitgenauigkeit bereitgestellt, um die Authentifizierungsanforderungen von Kerberos, Version 5, zu erfüllen.
> - hat Windows-Clients und -Servern, die einer gemeinsamen Active Directory-Gesamtstruktur beigetreten sind, eine lose Zeit bereitgestellt.
>
>Höhere Toleranzen in 2012 R2 und niedriger liegen außerhalb der Entwurfsspezifikation des Windows-Zeitdiensts.

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Standardkonfiguration von Windows 10 und Windows Server 2016

Wir unterstützen zwar eine Genauigkeit von bis zu 1 ms unter Windows 10 oder Windows Server 2016, doch die Mehrheit unserer Kunden benötigt keine hochpräzise Zeit.

Daher ist die **Standardkonfiguration** darauf ausgelegt, dieselben Anforderungen zu erfüllen wie vorherige Betriebssysteme, die wie folgt lauten:

- Bereitstellen der notwendigen Zeitgenauigkeit, um die Authentifizierungsanforderungen von Kerberos, Version 5, zu erfüllen.
- Bereitstellen einer losen Zeit für Windows-Clients und -Server, die einer gemeinsamen Active Directory-Gesamtstruktur beigetreten sind.

## <a name="how-to-configure-systems-for-high-accuracy"></a>Konfigurieren von Systemen für hohe Genauigkeit

>[!IMPORTANT]
>**Hinweis zur Unterstützbarkeit von hochpräzisen Systemen**<br>
> Die Zeitgenauigkeit umfasst die End-to-End-Verteilung der exakten Zeit von der autoritativen Zeitquelle bis zum Endgerät.  Alles, was entlang dieses Pfads bei Messungen Asymmetrien einführt, wirkt sich negativ auf die Genauigkeit aus, was wiederum auf die auf Ihren Geräten erreichbare Genauigkeit auswirkt.
>
>Aus diesem Grund haben wir die [Supportgrenze zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md) dokumentiert, worin die Umgebungsanforderungen dargelegt werden, die außerdem erfüllt sein müssen, um hohe Genauigkeitsziele zu erreichen.

### <a name="operating-system-requirements"></a>Betriebssystemanforderungen

Konfigurationen mit hoher Genauigkeit erfordern Windows 10 oder Windows Server 2016.  Alle Windows-Geräte in der Zeittopologie müssen diese Anforderung erfüllen, einschließlich der Windows-Zeitserver auf höheren Strata, sowie bei virtualisierten Szenarien die Hyper-V-Hosts, auf denen die zeitempfindlichen virtuellen Computer ausgeführt werden. Alle diese Geräte müssen mindestens Windows 10 oder Windows Server 2016 ausführen.

In der unten gezeigten Abbildung werden die virtuellen Computer, die hohe Genauigkeit benötigen, unter Windows 10 oder Windows Server 2016 ausgeführt.  Ebenso müssen auch der Hyper-V-Host, auf dem sich die virtuellen Computer befinden, sowie der Upstream-Windows-Zeitserver ebenfalls Windows Server 2016 ausführen.

![Zeittopologie – 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Ermitteln der Windows-Version**<br>
> Du kannst den Befehl `winver` an einer Eingabeaufforderung ausführen, um zu überprüfen, ob die Betriebssystemversion 1607 (oder höher) und der BS-Build 14393 (oder höher) ist, wie unten dargestellt:
>
> ![Winver – 2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>Systemkonfiguration

Das Erreichen hoher Genauigkeitsziele erfordert eine Systemkonfiguration.  Es gibt eine Reihe unterschiedlicher Möglichkeiten, diese Konfiguration vorzunehmen, einschließlich direkt in der Registrierung oder über eine Gruppenrichtlinie.  Weitere Informationen zu den einzelnen Einstellungen findest du in der „Technischen Referenz zum Windows-Zeitdienst“ – [Windows-Zeitdiensttools](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools).

#### <a name="windows-time-service-startup-type"></a>Starttyp des Windows-Zeitdiensts

Der Windows-Zeitdienst (W32Time) muss ständig ausgeführt werden.  Konfiguriere hierzu den Starttyp des Windows-Zeitdiensts für einen „Automatisch“en Start.

![Automatische Konfiguration](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>Kumulative unidirektionale Netzwerklatenz

Mit steigender Netzwerklatenz schleichen sich Messunsicherheiten und Störungen (Rauschen) ein.  Daher ist es zwingend erforderlich, dass sich eine Netzwerklatenz innerhalb angemessener Grenze bewegt.  Die spezifischen Anforderungen hängen von deiner Zielgenauigkeit ab und werden in dem Artikel [Supportgrenze zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md) dargelegt.

Um die kumulative unidirektionale Netzwerklatenz zu berechnen, addiere die einzelnen unidirektionalen Verzögerungen zwischen Paaren von NTP-Client-Server-Knoten in der Zeittopologie, beginnend mit dem Ziel und endend an der hochpräzisen Zeitquelle in Stratum 1.

Beispiel: Stell dir eine Zeitsynchronisierungshierarchie mit einer hochpräzisen Quelle, zwei zwischengeschalteten NTP-Servern A und B sowie dem Zielcomputer in dieser Reihenfolge vor. Um die kumulative Netzwerklatenz zwischen Ziel und Quelle zu ermitteln, misst du die durchschnittlichen einzelnen NTP-Roundtripzeiten (RTTs) zwischen:

- Ziel und Zeitserver B
- Zeitserver B und Zeitserver A
- Zeitserver A und Quelle

Diese Messung kann mithilfe des im Lieferumfang enthaltenen Tools „w32tm.exe“ vorgenommen werden.  Aufgabe:

1. Führe die Berechnung vom Ziel zum Zeitserver B durch.
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. Führe die Berechnung vom Zeitserver B zum Zeitserver A (darauf verwiesen) durch.
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. Führe die Berechnung vom Zeitserver A zur Quelle durch.
 
4. Addiere als Nächstes die im vorherigen Schritt gemessene, durchschnittliche RoundTripDelay hinzu und teile durch 2, um die kumulative Netzwerkverzögerung zwischen Ziel und Quelle zu erhalten.

#### <a name="registry-settings"></a>Registrierungseinstellungen

# <a name="minpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
Konfiguriert das kleinste Intervall in log2 Sekunden, das für den Systemabruf zulässig ist.

|  |  | 
|---------|---------|
|Ort des Schlüssels     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|Einstellung    | 6        |
|Resultate | Das minimale Abrufintervall ist jetzt 64 Sekunden. |

Mit dem folgenden Befehl wird Windows-Zeit signalisiert, die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`


# <a name="maxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
Konfiguriert das größte Intervall in log2 Sekunden, das für den Systemabruf zulässig ist.

|  |  |  
|---------|---------|
|Ort des Schlüssels     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|Einstellung    | 6        |
|Resultate | Das maximale Abrufintervall ist jetzt 64 Sekunden.  |

Mit dem folgenden Befehl wird Windows-Zeit signalisiert, die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`

# <a name="updateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
Die Anzahl der Zeiteinheiten zwischen Phasenkorrekturanpassungen.

|  |  |  
|---------|---------|
|Ort des Schlüssels     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|Einstellung    | 100        |
|Resultate | Die Anzahl der Zeiteinheiten zwischen Phasenkorrekturanpassungen ist jetzt 100 Einheiten. |

Mit dem folgenden Befehl wird Windows-Zeit signalisiert, die aktualisierten Einstellungen zu übernehmen:

`w32tm /config /update`

# <a name="specialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
Konfiguriert das Abrufintervall in Sekunden, wenn das Kennzeichen „SpecialInterval 0x1“ aktiviert ist.

|  |  |  
|---------|---------|
|Ort des Schlüssels     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|Einstellung    | 64        |
|Resultate | Das Abrufintervall ist jetzt 64 Sekunden. |

Mit dem folgenden Befehl wird Windows-Zeit neu gestartet, um die aktualisierten Einstellungen zu übernehmen:

`net stop w32time && net start w32time`

# <a name="frequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|Ort des Schlüssels     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|Einstellung    | 2        |


---
