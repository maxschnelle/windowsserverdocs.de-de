---
title: Installieren des Servers mit Desktopdarstellung
description: 'Erläutert, wie Sie eine Installation des Servers mit Desktopdarstellung erhalten und durchführen '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 01/18/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b38b8a0-4dfc-4130-be00-fc58bba99595
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: eb2e5be2ed19fe7cd64f6c6bd64ca9afafd93bff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812311"
---
# <a name="install-server-with-desktop-experience"></a>Installieren des Servers mit Desktopdarstellung
> Gilt für: Windows Server 2016
  

Bei der Installation von Windows Server 2016 mithilfe des Setup-Assistenten können Sie zwischen **Windows Server 2016** und **Windows Server (Server mit Desktopdarstellung)** wählen. Die Option „Server mit Desktopdarstellung“ ist das Äquivalent der in Windows Server 2012 R2 verfügbaren vollständigen Installationsoption mit dem Feature „Desktopdarstellung“ in Windows Server 2016. Wenn Sie im Setup-Assistenten keine Auswahl treffen, wird **Windows Server 2016** installiert. Dies ist die **Server Core**-Installationsoption.

Die Option „Server mit Desktopdarstellung“ installiert die Standardbenutzeroberfläche und alle Tools, einschließlich Kundenerfahrungsfeatures, die in Windows Server 2012 R2 eine separate Installation erforderten. Serverrollen und Features werden mit dem Server-Manager oder anderen Methoden installiert. Im Vergleich zur Option „Server Core“ erfordert diese Option mehr Speicherplatz auf dem Datenträger, und hat höhere Wartungsanforderungen. Daher empfiehlt es sich, die Server Core-Installation auszuwählen, sofern Sie die zusätzlichen Benutzeroberflächenelemente oder grafischen Verwaltungstools nicht unbedingt benötigen, die in der Option „Server mit Desktopdarstellung“ enthalten sind. Wenn Sie den Eindruck haben, dass Sie ohne die zusätzlichen Elemente arbeiten können, rufen Sie [Installieren von Server Core](Getting-Started-with-Server-Core.md) auf. Eine noch einfachere Option finden Sie unter [Installieren von Nano Server](Getting-Started-with-Nano-Server.md).

>[!NOTE]
>
>Im Gegensatz zu einigen früheren Versionen von Windows Server ist eine Konvertierung zwischen Server Core und Servern mit Desktopdarstellung nach der Installation nicht möglich. Wenn Sie Server mit Desktopdarstellung installieren und später Server Core verwenden möchten, sollten Sie eine Neuinstallation durchführen.

**Benutzeroberfläche:** standardmäßige grafische Benutzeroberfläche („Servergrafikshell“). Die Servergrafikshell enthält die neue Windows 10-Shell. Die standardmäßig mit dieser Option installierten spezifischen Windows-Features sind User-Interfaces-Infra, Server-GUI-Shell, Server-GUI-Mgmt-Infra, InkAndHandwritingServices, ServerMediaFoundation und Desktopdarstellung. Diese Features werden zwar im Server-Manager in dieser Version angezeigt, doch ihre Deinstallierung wird nicht unterstützt, und sie werden in zukünftigen Versionen nicht verfügbar sein.

**Lokales Installieren, Konfigurieren und Deinstallieren von Serverrollen:** mit Server-Manager oder Windows PowerShell

**Installieren, Konfigurieren und Deinstallieren von Serverrollen im Remotemodus:** mit Server-Manager, Remoteserver, RSAT oder Windows PowerShell

**Microsoft Management Console: installiert**

## <a name="installation-scenarios"></a>Installationsszenarios

### <a name="evaluation"></a>Bewertung
Sie erhalten eine für 180 Tage lizenzierte Evaluierungskopie von Windows Server unter [Windows Server-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016). Wählen Sie die **Windows Server 2016 | 64-Bit-ISO-Option** zum Download aus, oder besuchen Sie **Windows Server 2016 | Virtual Lab**.

> [!IMPORTANT]  
> Für ältere Versionen von Windows Server 2016 als 14393.0.161119-1705.RS1_REFRESH können Sie diese Konvertierung aus der Test- in die Einzelhandelsversion nur mit Windows Server 2016 ausführen, das unter Verwendung der Option „Desktopdarstellung“ installiert wurde (und nicht mit der Server Core-Option). Ab Version 14393.0.161119-1705. RS1_REFRESH können Sie Testversionen unabhängig von der verwendeten Installationsoption in Einzelhandelsversionen konvertieren.


### <a name="clean-installation"></a>Neuinstallation

Um die Installationsoption „Server mit Desktopdarstellung“ von den Medium zu installieren, legen Sie das Installationsmedium in ein Laufwerk ein, starten Sie den Computer neu, und führen Sie „Setup.exe“ aus. Wählen Sie im angezeigten Assistenten **Windows Server (Server mit Desktopdarstellung)** (Standard oder Datacenter) aus, und schließen Sie den Assistenten ab.

### <a name="upgrade"></a>Upgrade/Aktualisieren
Bei einem**Upgrade** wechseln Sie vom vorhandenen Betriebssystem zu einer neueren Version und verwenden dabei die gleiche Hardware.

Wenn Sie bereits über eine vollständige Installation des entsprechenden Windows Server-Produkts verfügen, können Sie ein Upgrade auf eine Installation von Server mit Desktopdarstellung der entsprechenden Version von Windows Server 2016 durchführen, wie unten angegeben.

> [!IMPORTANT]  
> In dieser Version funktioniert das Upgrade am Besten auf virtuellen Computern, auf denen keine spezifischen OEM-Hardwaretreiber für ein erfolgreiches Upgrade benötigt werden. Andernfalls ist Migration die empfohlene Option.  

- Direkte Upgrades von 32-Bit-Architekturen auf 64-Bit-Architekturen werden nicht unterstützt. Alle Editionen von Windows Server 2016 sind ausschließlich 64-Bit-Versionen.
- Direkte Upgrades von einer Sprache auf eine andere werden nicht unterstützt.
- Wenn der Server ein Domänencontroller ist, finden Sie unter [Aktualisieren von Domänencontrollern auf Windows Server 2012 R2 und Windows Server 2012](https://technet.microsoft.com/library/hh994618.aspx) wichtige Informationen.
- Upgrades von Vorabversionen (Previews) von Windows Server 2016 werden nicht unterstützt. Führen Sie eine Neuinstallation von Windows Server 2016 durch.
- Upgrades, bei denen von einer Server Core-Installation zu einem Server mit grafischer Benutzeroberfläche (oder umgekehrt) gewechselt wird, werden nicht unterstützt.

Wenn Ihre aktuelle Version nicht in der linken Spalte aufgeführt ist, wird ein Upgrade auf diese Version von Windows Server 2016 nicht unterstützt.

Werden in der rechten Spalte mehrere Editionen angezeigt, wird das Upgrade auf **alle** Editionen von derselben Startversion unterstützt.

|Ausgeführte Edition:|Zieleditionen:|  
|-------------------|----------|  
|Windows Server2012 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server2012R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Arbeitsgruppe unter Windows Storage Server 2012 R2|Windows Storage Server 2016 Workgroup|

Viele weitere Optionen für den Wechsel zu Windows Server 2016, z.B. die Konvertierung der Lizenz zwischen Volumenlizenzversionen, Testversionen und anderen, finden Sie unter [Upgrade Options (Aktualisierungsoptionen)](Supported-Upgrade-Paths.md).

### <a name="migration"></a>Migration
**Migration** bezeichnet den Wechsel von Ihrem bestehenden Betriebssystem zu Windows Server 2016 durch Neuinstallation auf einer anderen Hardware oder einem anderen virtuellen Computer und anschließendem Transfer der Workloads des älteren Servers auf den neuen Server. Ausführliche Informationen zur Migration, die abhängig von den installierten Serverrollen stark variieren kann, finden Sie unter [Windows Server Installation, Upgrade, and Migration (Windows Server-Installation, -Upgrade und -Migration)](https://technet.microsoft.com/windowsserver/dn458795).

Die Fähigkeit zur Migration unterscheidet sich bei verschiedenen Serverrollen. Das folgende Raster veranschaulicht Ihre Optionen für Serverrollen-Upgrades und Migration speziell für den Wechsel zu Windows Server 2016. Einzelne Migrationshandbücher finden Sie unter [Migrieren von Rollen und Features in Windows Server](https://technet.microsoft.com/windowsserver/jj554790.aspx). Weitere Informationen zu Installation und Upgrades finden Sie unter [Windows Server Installation, Upgrade, and Migration (Windows Server-Installation, -Upgrade und -Migration)](https://technet.microsoft.com/windowsserver/dn458795).

|Serverrolle|Upgrade von Windows Server 2012 R2 möglich?|Upgrade von Windows Server 2012 möglich?|Wird die Migration unterstützt?|Kann die Migration ohne Downtime abgeschlossen werden?|  
|-------------------|----------|--------------|--------------|----------|  
|Active Directory-Zertifikatdienste| Ja|    Ja|    Ja|    Nein|
|Active Directory Domain Services|  Ja|    Ja|    Ja|    Ja|
|Active Directory-Verbunddienste (AD FS)|  Nein| Nein| Ja|    Nein (neue Knoten müssen zur Farm hinzugefügt werden)|
|Active Directory Lightweight Directory Services|   Ja|    Ja|    Ja|    Ja|
|Active Directory-Rechteverwaltungsdienste|   Ja|    Ja|    Ja|    Nein|
|Failovercluster|Ja mit dem Prozess [Cluster OS Rolling Upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade), der Pause-Drain und Evict von Knoten, Upgrade auf Windows Server 2016 und das wieder Zusammenführen von Knoten zu einem ursprünglichen Cluster umfasst. Ja, wenn der Server für ein Upgrade vom Cluster entfernt und dann zu einem anderen Cluster hinzugefügt wird.|Nicht wenn der Server Teil eines Clusters ist. Ja, wenn der Server für ein Upgrade vom Cluster entfernt und dann zu einem anderen Cluster hinzugefügt wird.  |Ja|Nicht für Windows Server 2012-Failovercluster. Ja, für Windows Server 2012 R2-Failovercluster mit virtuellen Hyper-V Computern, oder für Windows Server 2012 R2-Failovercluster, die die Rolle des Dateiservers mit horizontaler Skalierung ausführen. Weitere Informationen finden Sie unter [Cluster OS Rolling Upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade).|
|Datei- und Speicherdienste| Ja|    Ja|    Variiert je nach Sub-Feature|  Nein|
|Druck- und Faxdienste|    Nein| Nein| Ja (Printbrm.exe)| Nein|
|Remotedesktopdienste|   Ja, für alle untergeordneten Rollen. Die Farm im gemischten Modus wird jedoch nicht unterstützt|   Ja, für alle untergeordneten Rollen. Die Farm im gemischten Modus wird jedoch nicht unterstützt|   Ja|    Nein|
|Webserver (IIS)|  Ja|    Ja|    Ja|    Nein|
|Windows Server Essentials-Umgebung|  Ja|    N/V – neues Feature|  Ja|    Nein|
|Windows Server Update Services|    Ja|    Ja|    Ja|    Nein|
|Arbeitsordner|  Ja|    Ja|    Ja|    Ja, vom Cluster WS 2012 R2, wenn [Cluster OS Rolling Upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) ausgeführt wird.|

> [!IMPORTANT]  
> Sobald die Installation abgeschlossen ist und alle Serverrollen und Features, die Sie benötigen, installiert sind, suchen und installieren Sie verfügbare Updates für Windows Server 2016 mithilfe von Windows Update oder anderen Update-Methoden.

---------------------------------------
Wenn Sie eine andere Option zur Installation benötigen, oder wenn die Installation abgeschlossen ist und Sie bereit sind, spezifische Workloads bereitzustellen, können Sie [zur Windows Server 2016-Hauptseite zurückkehren](Windows-Server-2016.md).