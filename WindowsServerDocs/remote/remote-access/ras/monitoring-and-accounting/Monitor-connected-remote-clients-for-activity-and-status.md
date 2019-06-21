---
title: Überwachen der Aktivitäten und des Status von verbundenen Remoteclients
description: Dieses Thema ist Teil des Leitfadens für die Überwachung des Remotezugriffs und Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: beb94475-b21f-46a9-ac51-bf2bb28ca94e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bf7aed239eb56eae599078a6088cbb2971c45821
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282737"
---
# <a name="monitor-connected-remote-clients-for-activity-and-status"></a>Überwachen der Aktivitäten und des Status von verbundenen Remoteclients

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Windows Server 2012 werden DirectAccess "und" Remote Access Service (RAS) in einer einzigen remotezugriffsrolle zusammengefasst.  
  
Sie können die-Verwaltungskonsole auf dem RAS-Server verwenden, remoteclientaktivität und den Status zu überwachen.  
  
> [!NOTE]  
> Sie müssen als Mitglied der Gruppe "Domänen-Admins" oder ein Mitglied der Gruppe "Administratoren" auf jedem Computer angemeldet sein, die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht abschließen können, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Administratoren" ist, versuchen Sie es die Aufgabe auszuführen, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-monitor-remote-client-activity-and-status"></a>Um die remoteclientaktivität und den Status überwachen  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **REPORTING** , zu dem navigiert **Remoteberichte Zugriff** in die **Remotezugriffs-Verwaltungskonsole**.  
  
3.  Klicken Sie auf **Remoteclientstatus** navigieren, der Remoteclient Aktivitäten und des Status der Benutzeroberfläche in der **Remotezugriffs-Verwaltungskonsole**.  
  
4.  Sehen Sie die Liste der Benutzer, die mit dem RAS-Server verbunden sind, und detaillierte Statistiken zu diesen. Klicken Sie auf der ersten Zeile in der Liste, die ein Client entspricht. Wenn Sie eine Zeile auswählen, wird die Remotebenutzer-Aktivität im Vorschaufenster angezeigt.  
  
![Windows PowerShell](../../../media/Monitor-connected-remote-clients-for-activity-and-status/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
PS> Get-RemoteAccessConnectionStatistics  
```  
  
Die Benutzerstatistiken können Kriterienauswahl, mithilfe der Felder in der folgenden Tabelle gefiltert werden.  
  
|Feldname|Wert|  
|-------|-----|  
|Benutzername|Der Benutzername oder das Alias des Remotebenutzers. Platzhalterzeichen können verwendet werden, um eine Gruppe von Benutzern, z. B. Contoso auszuwählen\\* oder \*\administrator.|  
|Hostname|Der Name des Computerkontos des Remotebenutzers. Eine IPv4- oder IPv6-Adresse kann auch angegeben werden.|  
|Typ|DirectAccess oder VPN. Wenn DirectAccess ausgewählt wird, werden alle Remotebenutzer, die über DirectAccess verbunden sind, aufgeführt. Wenn VPN ausgewählt wird, werden alle Remotebenutzer, die über VPN verbunden sind, aufgeführt.|  
|ISP-Adresse|Die IPv4- oder IPv6-Adresse des Remotebenutzers.|  
|IPv4-Adresse|Die interne IPv4-Adresse des Tunnels, der den Remotebenutzer mit dem Unternehmensnetzwerk herstellen.|  
|IPv6-Adresse|Die interne IPv6-Adresse des Tunnels, über den der Remotebenutzer mit dem Unternehmensnetzwerk verbunden ist.|  
|Protokoll//Tunnel|Der Übergang Technologie, die von der remote-Client verwendet wird. Dies ist Teredo, 6to4 oder IP-HTTPS für DirectAccess-Benutzer, und es ist PPTP, L2TP, SSTP oder IKEv2 für VPN-Benutzer.|  
|Aufgerufene Ressource|Alle Benutzer, die auf eine bestimmte Unternehmensressource oder einen bestimmten Unternehmensendpunkt zugreifen. Der Wert, der dieses Feld entspricht, ist der Hostname oder IP-Adresse des Servers.|  
|Server|Der RAS-Server, mit dem Clients verbunden sind. Dies ist nur für Clusterbereitstellungen und Bereitstellungen für mehrere Standorte relevant.|  
  
  
  


