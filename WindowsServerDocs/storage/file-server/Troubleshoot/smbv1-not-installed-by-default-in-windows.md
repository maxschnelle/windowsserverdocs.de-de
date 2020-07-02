---
title: SMBv1 wird nicht standardmäßig unter Windows 10, Version 1709, Windows Server Version 1709 und höheren Versionen installiert.
description: Erläutert das Verhalten des SMBv1-Protokolls in Windows 10 Fall Creators Update und Windows Server, Version 1709 und höheren Versionen.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 07/01/2020
ms.openlocfilehash: 18c315a8b3562c25b5fe1c537a8922fc148e444b
ms.sourcegitcommit: c40c29683d25ed75b439451d7fa8eda9d8d9e441
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85833286"
---
# <a name="smbv1-is-not-installed-by-default-in-windows-10-version-1709-windows-server-version-1709-and-later-versions"></a>SMBv1 wird nicht standardmäßig unter Windows 10, Version 1709, Windows Server Version 1709 und höheren Versionen installiert.

## <a name="summary"></a>Zusammenfassung

In Windows 10 Fall Creators Update und Windows Server, Version 1709 (RS3) und höheren Versionen, wird das Netzwerkprotokoll Server Message Block Version 1 (SMBv1) nicht mehr standardmäßig installiert. Sie wurde ab 2007 durch SMBv2 und spätere Protokolle abgelöst. Microsoft hat das SMBv1-Protokoll in 2014 öffentlich als veraltet eingestuft. 

SMBv1 hat das folgende Verhalten in Windows 10 und Windows Server ab Version 1709 (RS3): 
 
- SMBv1 verfügt nun sowohl über Client-als auch Server-unter Funktionen, die separat deinstalliert werden können.    
- Windows 10 Enterprise, Windows 10 Education und Windows 10 pro für Arbeitsstationen enthalten standardmäßig den SMBv1-Client bzw.-Server nicht mehr standardmäßig nach einer Neuinstallation.    
- Windows Server 2016 enthält den SMBv1-Client bzw.-Server nicht mehr standardmäßig nach einer Neuinstallation.    
- Windows 10 Home und Windows 10 pro enthalten nach einer Neuinstallation nicht mehr standardmäßig den SMBv1-Server.    
- Windows 10 Home und Windows 10 pro enthalten nach einer Neuinstallation weiterhin standardmäßig den SMBv1-Client. Wenn der SMBv1-Client nicht 15 Tage lang verwendet wird (mit Ausnahme des Computers, der ausgeschaltet wird), wird er automatisch deinstalliert.    
- Bei direkten Upgrades und Insider-Flügen von Windows 10 Home und Windows 10 pro wird SMBv1 anfänglich nicht automatisch entfernt. Wenn der SMBv1-Client bzw.-Server nicht 15 Tage lang verwendet wird (außer dem Zeitpunkt, an dem der Computer ausgeschaltet ist), werden diese automatisch deinstalliert.     
- Durch direkte Upgrades und Insider-Flüge der Editionen Windows 10 Enterprise, Windows 10 Education und Windows 10 pro für Arbeitsstationen wird SMBv1 nicht automatisch entfernt. Ein Administrator muss entscheiden, SMBv1 in diesen verwalteten Umgebungen zu deinstallieren. 
- Das automatische Entfernen von SMBv1 nach 15 Tagen ist ein einmal Vorgang. Wenn ein Administrator SMBv1 erneut installiert, werden keine weiteren Versuche unternommen, ihn zu deinstallieren.
- Die Features der SMB-Version 2,02, 2,1, 3,0, 3,02 und 3.1.1 werden weiterhin vollständig unterstützt und sind standardmäßig als Teil der SMBv2-Binärdateien enthalten.    
- Da der Computer Browser Dienst auf SMBv1 basiert, wird der Dienst deinstalliert, wenn der SMBv1-Client oder-Server deinstalliert wird. Dies bedeutet, dass das Explorer-Netzwerk Windows-Computer nicht mehr über die Legacy Methode NetBIOS-Datagramm-Browsen anzeigen kann.    
- SMBv1 kann weiterhin in allen Editionen von Windows 10 und Windows Server 2016 neu installiert werden.    

SMBv1 verfügt über die folgenden zusätzlichen Verhaltensweisen in Windows 10 ab Version 1809 (RS5). Alle anderen Verhalten von Version 1709 gelten weiterhin:

- Windows 10 pro enthält den SMBv1-Client standardmäßig nicht mehr standardmäßig nach einer Neuinstallation.
- In Windows 10 Enterprise, Windows 10 Education und Windows 10 pro für Arbeitsstationen können Administratoren das automatische Entfernen von SMBv1 aktivieren, indem Sie das Feature "Automatisches Entfernen von SMB 1.0/CIFS" aktivieren.

  > [!NOTE]
  > Windows 10, Version 1803 (RS4) pro verarbeitet SMBv1 auf die gleiche Weise wie Windows 10, Version 1703 (RS2) und Windows 10, Version 1607 (RS1). Dieses Problem wurde in Windows 10, Version 1809 (RS5) behoben. Sie können SMBv1 weiterhin manuell deinstallieren. In den folgenden Szenarien wird Windows jedoch nicht automatisch deinstalliert SMBv1 nach 15 Tagen: 

-  Sie führen eine saubere Installation von Windows 10, Version 1803, durch.     
-  Sie führen ein Upgrade von Windows 10, Version 1607 oder Windows 10, Version 1703, auf Windows 10, Version 1803, direkt durch, ohne zuvor ein Upgrade auf Windows 10, Version 1709, auszuführen.     
 
Wenn Sie versuchen, eine Verbindung mit Geräten herzustellen, die nur SMBv1 unterstützen, oder wenn diese Geräte versuchen, eine Verbindung mit ihnen herzustellen, erhalten Sie möglicherweise eine der folgenden Fehlermeldungen:     

```
You can't connect to the file share because it's not secure. This share requires the obsolete SMB1 protocol, which is unsafe and could expose your system to attack.
Your system requires SMB2 or higher. For more info on resolving this issue, see: https://go.microsoft.com/fwlink/?linkid=852747  
```

```
The specified network name is no longer available.
```

```
Unspecified error 0x80004005
```

```
System Error 64
```

```
The specified server cannot perform the requested operation.
```

```
Error 58
```    

Die folgenden Ereignisse werden angezeigt, wenn ein Remote Server eine SMBv1-Verbindung von diesem Client benötigt, aber SMBv1 auf dem Client deinstalliert oder deaktiviert wurde.

```
Log Name:      Microsoft-Windows-SmbClient/Security
 Source:        Microsoft-Windows-SMBClient
 Date:          Date/Time
 Event ID:      32002
 Task Category: None
 Level:         Info
 Keywords:      (128)
 User:          NETWORK SERVICE
 Computer:      junkle.contoso.com
 Description:
 The local computer received an SMB1 negotiate response. 

Dialect: 
SecurityMode 
Server name: 

Guidance: 
SMB1 is deprecated and should not be installed nor enabled. For more information, see https://go.microsoft.com/fwlink/?linkid=852747.
```

```
Log Name:      Microsoft-Windows-SmbClient/Security
 Source:        Microsoft-Windows-SMBClient
 Date:          Date/Time
 Event ID:      32000
 Task Category: None
 Level:         Info
 Keywords:      (128)
 User:          NETWORK SERVICE
 Computer:      junkle.contoso.com
 Description: 
SMB1 negotiate response received from remote device when SMB1 cannot be negotiated by the local computer. 
Dialect: 
Server name: 

Guidance: 
The client has SMB1 disabled or uninstalled. For more information: https://go.microsoft.com/fwlink/?linkid=852747.     
```

Diese Geräte werden wahrscheinlich nicht unter Windows ausgeführt.Sie führen eher ältere Versionen von Linux, Samba oder anderen Arten von Drittanbieter Software aus, um SMB-Dienste bereitzustellen. Häufig werden diese Versionen von Linux und Samba nicht mehr unterstützt. 

> [!NOTE]
> Windows 10, Version 1709, wird auch als "Fall Creators Update" bezeichnet.   

## <a name="more-information"></a>Weitere Informationen

Um dieses Problem zu umgehen, wenden Sie sich an den Hersteller des Produkts, das nur SMBv1 unterstützt, und fordern Sie ein Software-oder Firmwareupdate an, das smbv 2,02 oder eine höhere Version unterstützt. Eine aktuelle Liste bekannter Lieferanten und deren SMBv1-Anforderungen finden Sie im folgenden Blog Artikel zum Windows-und Windows Server-speicherengineering-Team: 

[SMBv1 Product Clearinghouse](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/SMB1-Product-Clearinghouse/ba-p/426008) 
#### <a name="leasing-mode"></a>Leasing Modus

Wenn SMBv1 erforderlich ist, um Anwendungs Kompatibilität für Legacy Software Verhalten bereitzustellen, z. b. eine Anforderung zum Deaktivieren von oplocks, bietet Windows ein neues SMB-freigabeflag, das als Leasing Modus bezeichnet wird. Dieses Flag gibt an, ob eine Freigabe eine moderne SMB-Semantik, wie z. b. Leases und oplocks, deaktiviert.

Sie können eine Freigabe angeben, ohne oplocks oder Leasing zu verwenden, damit eine Legacy Anwendung mit SMBv2 oder einer höheren Version arbeiten kann. Verwenden Sie hierzu die PowerShell-Cmdlets " **New-smbshare** " oder " **Set-smbshare** " gemeinsam mit dem Parameter " **-leasingmode None**"   .

> [!NOTE]
> Sie sollten diese Option nur für Freigaben verwenden, die von einer Drittanbieter Anwendung für ältere Unterstützung benötigt werden, wenn der Hersteller feststellt, dass Sie erforderlich ist. Geben Sie nicht den Leasing Modus für Benutzerdaten Freigaben oder ca-Freigaben an, die von Dateiservern mit horizontaler Skalierung verwendet werden. Dies liegt daran, dass durch das Entfernen von oplocks und Leases in den meisten Anwendungen Instabilität und beschädigte Daten verursacht werden. Der Leasing Modus funktioniert nur im Freigabe Modus. Sie kann von jedem Client Betriebssystem verwendet werden.

#### <a name="explorer-network-browsing"></a>Explorer-Netzwerk durchsuchen

Der Computer Suchdienst basiert auf dem SMBv1-Protokoll, um den Windows Explorer-Netzwerkknoten (auch als "Netzwerkumgebung" bezeichnet) aufzufüllen. Dieses Legacy Protokoll ist lange veraltet, wird nicht weitergeleitet und verfügt über eingeschränkte Sicherheit. Da der Dienst ohne SMBv1 nicht funktionsfähig ist, wird er gleichzeitig entfernt.

Wenn Sie jedoch weiterhin den Explorer Netzwerk eingehend Home-und Small Business-Arbeitsgruppen Umgebungen verwenden müssen, um Windows-basierte Computer zu finden, können Sie die folgenden Schritte auf Ihren Windows-basierten Computern ausführen, auf denen SMBv1 nicht mehr verwendet wird: 
 
1. Starten Sie die Dienste "funktionsermittlungs-Anbieter Host" und "funktionsermittlungs-Ressourcen Veröffentlichung", und legen Sie Sie auf **automatisch (verzögerter Start)** fest.

2. Wenn Sie das Explorer-Netzwerk öffnen, aktivieren Sie die Netzwerk Ermittlung, wenn Sie dazu aufgefordert werden.    
 
Alle Windows-Geräte in diesem Subnetz, die über diese Einstellungen verfügen, werden jetzt im Netzwerk zum Durchsuchen angezeigt. Dabei wird das WS-Discovery-Protokoll verwendet. Wenden Sie sich an andere Hersteller und Hersteller, wenn Ihre Geräte nach der Anzeige der Windows-Geräte noch nicht in dieser Liste angezeigt werden. Es ist möglich, dass dieses Protokoll deaktiviert ist oder nur SMBv1 unterstützt.

> [!NOTE]
> Es wird empfohlen, dass Sie Laufwerke und Drucker zuordnen, anstatt diese Funktion zu aktivieren, die weiterhin das Suchen und Durchsuchen Ihrer Geräte erfordert. Zugeordnete Ressourcen sind leichter zu finden, erfordern weniger Schulungen und sind sicherer zu verwenden. Dies trifft vor allem dann zu, wenn diese Ressourcen automatisch über Gruppenrichtlinie bereitgestellt werden.Ein Administrator kann Drucker für den Speicherort mithilfe von IP-Adressen, Active Directory Domain Services (AD DS), Bonjour, mdns, UPnP usw. für den Speicherort konfigurieren.

Wenn Sie keine dieser Problem Umgehungen verwenden können, oder wenn der Anwendungshersteller keine unterstützten Versionen von SMB bereitstellen kann, können Sie SMBv1 manuell erneut aktivieren, indem Sie die Schritte unter [erkennen, aktivieren und Deaktivieren von SMBv1, SMBv2 und SMBv3 in Windows](detect-enable-and-disable-smbv1-v2-v3.md)ausführen.

> [!IMPORTANT]
> Es wird dringend empfohlen, SMBv1 nicht erneut zu installieren. Dies liegt daran, dass dieses ältere Protokoll bekannte Sicherheitsprobleme in Bezug auf die Ransomware und andere Schadsoftware hat.  

#### <a name="windows-server-best-practices-analyzer-messaging"></a>Best Practices Analyzer-Messaging für Windows Server

Windows Server 2012 und spätere Server Betriebssysteme enthalten einen Best Practices Analyzer (BPA) für Dateiserver. Wenn Sie die richtige Online Anleitung zum Deinstallieren von Server Message Block befolgt haben, wird durch das Ausführen dieses BPA eine widersprüchliche Warnmeldung zurückgegeben:

    Title: The SMB 1.0 file sharing protocol should be enabled
    Severity: Warning
    Date: 3/25/2020 12:38:47 PM
    Category: Configuration
    Problem: The Server Message Block 1.0 (SMB 1.0) file sharing protocol is disabled on this file server.
    Impact: SMB not in a default configuration, which could lead to less than optimal behavior.
    Resolution: Use Registry Editor to enable the SMB 1.0 protocol.

Sie sollten diese spezielle Richtlinie der BPA-Regel ignorieren, da sie veraltet ist. Wir wiederholen Folgendes: Aktivieren Sie SMB 1,0 nicht.

## <a name="references"></a>Referenzen

[Verwendung von Server Message Block nicht mehr](https://aka.ms/stopusingsmb1)
