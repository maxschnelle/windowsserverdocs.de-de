---
title: Hardwareanforderungen für den Zielcomputer
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c20b06b9-ce0d-4c20-bf49-257c3f5dc01b
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 1672c8168dd206c166ca44392ca290ebb311dcc6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623518"
---
# <a name="hardware-requirements-for-the-target-computer"></a>Hardwareanforderungen für den Zielcomputer

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieser Abschnitt enthält die Hardwareanforderungen für Windows Server Essentials.

## <a name="hardware-requirements-for-windows-server-essentials"></a>Hardware Anforderungen für Windows Server Essentials
 Sie müssen Windows Server Essentials auf dem Zielcomputer installieren, der die in der folgenden Tabelle aufgeführten Anforderungen erfüllt.

### <a name="table-1--system-requirements-for-windows-server-essentials"></a>Tabelle 1: System Anforderungen für Windows Server Essentials

|Komponente|Minimum|Empfohlen*|Maximum|
|---------------|-------------|-------------------|-------------|
|CPU-Socket|1,4 GHz (64-Bit-Prozessor) oder schneller für CPU mit einem Kern<br /><br /> 1,3 GHz (64-Bit-Prozessor) oder schneller für CPU mit mehreren Kernen|3,1 GHz (64-Bit-Prozessor) oder schneller für CPU mit mehreren Kernen|2 Sockets|
|Arbeitsspeicher (RAM)|2 GB|16 GB|64 GB|
|Festplatten und verfügbarer Speicherplatz|160-GB-Festplatte mit einer 60-GB-Systempartition||Keine Begrenzung|

 * Empfohlene Hardwareanforderungen zur Unterstützung der maximalen Anzahl von Benutzer-und Geräte Limits in Windows Server Essentials.

## <a name="additional-hardware-and-software-requirements"></a>Zusätzliche Hardware- und Softwareanforderungen
 Die folgende Tabelle enthält zusätzliche Hardware- und Softwareanforderungen.

|Komponente|BESCHREIBUNG|
|---------------|-----------------|
|Netzwerkadapter|Gigabit-Ethernet-Adapter (10/100/1000baseT PHY/MAC)|
|Internet|Für einige Funktionen ist möglicherweise ein Internet Zugang (ggf. Gebühren) oder ein Windows Live ID-Konto erforderlich. &reg;|
|Unterstützte Clientbetriebssysteme|-Windows 7<br />-Windows 8<br />-Macintosh OS X 10,5 bis 10,8.<br /><br /> **Hinweis:** Für einige Features sind Editionen von Professional oder höher erforderlich.<br /><br /> 1 GB verfügbarer Festplatten-Speicherplatz (ein Teil des Datenträgers wird nach der Installation freigegeben)|
|Router|Ein Router oder eine Firewall mit Unterstützung für IPv4 NAT|
|Zusätzliche Anforderungen|DVD-ROM-Laufwerk|

 Die tatsächlichen Anforderungen sind von der Systemkonfiguration und den zu installierenden Anwendungen und Funktionen abhängig. Die Prozessorleistung ist nicht nur von der Taktfrequenz des Prozessors abhängig, sondern auch von der Anzahl der Prozessorkerne und der Größe des Prozessorcaches. Bei den Speicherplatzanforderungen für die Systempartition handelt es sich um ungefähre Angaben. Zusätzlicher verfügbarer Speicherplatz ist ggf. erforderlich, wenn die Installation über ein Netzwerk erfolgt.

 Weitere Informationen zu den Hardwareanforderungen finden Sie im [Windows Server-Katalog](https://www.windowsservercatalog.com).

 Die gesamte Server Hardware sollte die Anforderungen erfüllen, die für das Windows Server 2012-Logo-Programm für Systeme festgelegt wurden. Weitere Informationen finden Sie unter [Windows Logo-Programm](https://www.microsoft.com/whdc/winlogo/hwrequirements.mspx).

## <a name="see-also"></a>Weitere Informationen

 Informationen zu den ersten Schritten [mit dem Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)

