---
title: Systemanforderungen für Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/31/2013
ms.topic: article
ms.assetid: 0951a67d-492f-41ad-9ae5-8e4cd25e3041
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 295022c45a82d18781df27604d47d58af14b4b2d
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181636"
---
# <a name="system-requirements-for-windows-server-essentials"></a>Systemanforderungen für Windows Server Essentials

>Gilt für: Windows Server 2019 Essentials, Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

  Bei der Windows Server Essentials-Server Software handelt es sich um ein 64-Bit-Betriebssystem. Tabelle 1 definiert die empfohlenen Mindesthardwareanforderungen für Windows Server Essentials. Tabelle 2 definiert zusätzliche Hardware- und Softwareanforderungen für den Server.


## <a name="table-1-system-requirements-for-windows-server-essentials"></a>Tabelle 1. System Anforderungen für Windows Server Essentials

|Komponente|Minimum|Empfohlen*|Maximum|
|---------------|-------------|-------------------|-------------|
|CPU-Socket|1,4 GHz (64-Bit-Prozessor) oder schneller für CPU mit einem Kern<br /><br /> 1,3 GHz (64-Bit-Prozessor) oder schneller für CPU mit mehreren Kernen|3,1 GHz (64-Bit-Prozessor) oder schneller für CPU mit mehreren Kernen|2 Sockets|
|Arbeitsspeicher (RAM)|2 GB<br /><br /> 4 GB, wenn Sie Windows Server Essentials als virtuellen Computer bereitstellen|16 GB|64 GB|
|Festplatten und verfügbarer Speicherplatz|160 GB Festplatte mit einer 60 GB-Systempartition||Keine Begrenzung|

 *Empfohlene Hardwareanforderungen zur Unterstützung der maximalen Anzahl an Benutzern und Geräten.

## <a name="table-2-additional-hardware-and-software-requirements-for-windows-server-essentials"></a>Tabelle 2: Zusätzliche Hardware-und Softwareanforderungen für Windows Server Essentials

|Komponente|BESCHREIBUNG|
|---------------|-----------------|
|Netzwerkadapter|Gigabit-Ethernet-Adapter (10/100/1000baseT PHY/MAC)|
|Internet|Für einige Funktionen ist möglicherweise ein Internetzugang (ggf. kostenpflichtig) oder ein Microsoft-Konto erforderlich.|
|Unterstützte Clientbetriebssysteme|Windows 8.1, Windows 8, Windows 7, Macintosh OS X, Version 10.5 bis 10.8.<br /><br /> **Hinweis:** Für einige Features sind Editionen von Professional oder höher erforderlich.<br /><br /> 1 GB verfügbarer Festplatten-Speicherplatz (ein Teil des Datenträgers wird nach der Installation freigegeben)|
|Router|Ein Router oder eine Firewall mit Unterstützung für IPv4 NAT oder IPv6|
|Zusätzliche Anforderungen|DVD-ROM-Laufwerk|

 Die tatsächlichen Anforderungen sind von der Systemkonfiguration und den zu installierenden Anwendungen und Funktionen abhängig. Die Prozessorleistung ist nicht nur von der Taktfrequenz des Prozessors abhängig, sondern auch von der Anzahl der Prozessorkerne und der Größe des Prozessorcaches. Bei den Speicherplatzanforderungen für die Systempartition handelt es sich um ungefähre Angaben. Zusätzlicher verfügbarer Speicherplatz ist ggf. erforderlich, wenn die Installation über ein Netzwerk erfolgt.

 Weitere Informationen zu den Hardwareanforderungen finden Sie im [Windows Server-Katalog](https://www.windowsservercatalog.com/).

 Die gesamte Server Hardware sollte die Anforderungen erfüllen, die für das Windows Server 2012 R2-Logo Programm für Systeme festgelegt wurden. Weitere Informationen finden Sie unter [Windows Logo-Programm](https://msdn.microsoft.com/windows/hardware/gg487403.aspx).

> [!IMPORTANT]
> Dynamische Datenträger werden in Windows Server Essentials nicht unterstützt.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Installieren von Windows Server Essentials](../install/Install-Windows-Server-Essentials.md)

-   [Systemanforderungen für Windows Server Essentials](system-requirements.md)


