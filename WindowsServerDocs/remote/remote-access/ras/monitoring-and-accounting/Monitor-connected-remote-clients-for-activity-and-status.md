---
title: Überwachen der Aktivitäten und des Status von verbundenen Remoteclients
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: beb94475-b21f-46a9-ac51-bf2bb28ca94e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4b2377816255189efbaa6d5c39cd4e91b923a039
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314219"
---
# <a name="monitor-connected-remote-clients-for-activity-and-status"></a>Überwachen der Aktivitäten und des Status von verbundenen Remoteclients

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

**Hinweis:** Windows Server 2012 kombiniert DirectAccess und RAS-Dienst (RAS) zu einer einzigen Remote Zugriffs Rolle.  
  
Sie können die-Verwaltungskonsole auf dem Remote Zugriffs Server verwenden, um die Remote Client Aktivität und den Status zu überwachen.  
  
> [!NOTE]  
> Sie müssen auf jedem Computer als Mitglied der Gruppe "Domänen-Admins" oder "Administratoren" angemeldet sein, um die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht ausführen können, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Administratoren" ist, versuchen Sie, die Aufgabe auszuführen, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-monitor-remote-client-activity-and-status"></a>So überwachen Sie die Remote Client Aktivität und den Status  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **Berichterstattung** , um in der **Remote Zugriffs-Verwaltungskonsole**zur **Remote Zugriffs Berichterstattung** zu navigieren.  
  
3.  Klicken Sie auf **Remote Client Status** , um in der **Remote Zugriffs-Verwaltungskonsole**in der Remote Zugriffs-Verwaltungskonsole zur Remote Client Aktivität und zur Benutzeroberfläche  
  
4.  Es wird eine Liste der Benutzer angezeigt, die mit dem RAS-Server verbunden sind, sowie ausführliche Statistiken zu diesen. Klicken Sie auf die erste Zeile in der Liste, die einem Client entspricht. Wenn Sie eine Zeile auswählen, wird die Remote Benutzeraktivität im Vorschaubereich angezeigt.  
  
![der entsprechenden Windows PowerShell-](../../../media/Monitor-connected-remote-clients-for-activity-and-status/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
PS> Get-RemoteAccessConnectionStatistics  
```  
  
Die Benutzerstatistiken können mithilfe der Felder in der folgenden Tabelle gefiltert werden, basierend auf der Kriterienauswahl.  
  
|Feldname|Wert|  
|-------|-----|  
|Benutzername|Der Benutzername oder das Alias des Remotebenutzers. Platzhalter Zeichen können verwendet werden, um eine Gruppe von Benutzern auszuwählen,\\wie z. b. "\*" von "\administrator" ".|  
|Hostname|Der Name des Computerkontos des Remotebenutzers. Außerdem kann eine IPv4-oder IPv6-Adresse angegeben werden.|  
|Typ|DirectAccess oder VPN. Wenn DirectAccess ausgewählt ist, werden alle Remote Benutzer, die über DirectAccess verbunden sind, aufgeführt. Wenn VPN ausgewählt wird, werden alle Remote Benutzer aufgelistet, die über VPN verbunden sind.|  
|ISP-Adresse|Die IPv4- oder IPv6-Adresse des Remotebenutzers.|  
|IPv4-Adresse|Die innere IPv4-Adresse des Tunnels, der den Remote Benutzer mit dem Unternehmensnetzwerk verbindet.|  
|IPv6-Adresse|Die interne IPv6-Adresse des Tunnels, über den der Remotebenutzer mit dem Unternehmensnetzwerk verbunden ist.|  
|Protokoll//Tunnel|Die Übergangstechnologie, die vom Remote Client verwendet wird. Dies ist Teredo, 6de4 oder IP-HTTPS für DirectAccess-Benutzer, und es ist PPTP, L2TP, SSTP oder IKEv2 für VPN-Benutzer.|  
|Aufgerufene Ressource|Alle Benutzer, die auf eine bestimmte Unternehmensressource oder einen bestimmten Unternehmensendpunkt zugreifen. Der Wert, der diesem Feld entspricht, ist der Hostname/die IP-Adresse des Servers.|  
|Server|Der RAS-Server, mit dem Clients verbunden sind. Dies ist nur für Clusterbereitstellungen und Bereitstellungen für mehrere Standorte relevant.|  
  
  
  


