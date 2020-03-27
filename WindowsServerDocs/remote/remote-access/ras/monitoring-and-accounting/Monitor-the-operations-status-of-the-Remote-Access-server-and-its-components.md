---
title: Überwachen des Betriebsstatus des Remotezugriffsservers und dessen Komponenten
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 077a3a64-2fa3-4994-9711-ec1fbdc081ba
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 64471ba81842fb91a7f6ef765e171949294102fa
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314180"
---
# <a name="monitor-the-operations-status-of-the-remote-access-server-and-its-components"></a>Überwachen des Betriebsstatus des Remotezugriffsservers und dessen Komponenten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

**Hinweis:** Durch Windows Server 2012 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Die Verwaltungskonsole auf dem RAS-Server kann zum Überwachen des Vorgangs Status verwendet werden.  
  
> [!NOTE]  
> Sie müssen auf jedem Computer als Mitglied der Gruppe "Domänen-Admins" oder "Administratoren" angemeldet sein, um die in diesem Thema beschriebene Aufgabe abzuschließen. Wenn Sie eine Aufgabe nicht ausführen können, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Administratoren" ist, versuchen Sie, die Aufgabe auszuführen, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-monitor-the-remote-access-server-operations-status"></a>So überwachen Sie den Betriebsstatus des RAS-Servers  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **Dashboard** , um in der **Remote Zugriffs-Verwaltungskonsole**zur **Remote Zugriffs Berichterstattung** zu navigieren.  
  
3.  Beachten Sie auf dem Dashboard Überwachung die Kachel **Betriebsstatus** innerhalb der Kachel **Server Status** . Diese Kachel listet den Serverbetriebs Status und den Status aller Serverkomponenten auf.  
  
4.  Klicken Sie im rechten Bereich unter **Tasks** auf **Aktualisieren** , um den Vorgangs Status neu zu laden. Der Vorgangs Status wird automatisch alle fünf Minuten aktualisiert. Dies ist das Standard Aktualisierungs Intervall. Um das Standard Aktualisierungs Intervall zu ändern, klicken Sie auf **Aktualisierungs Intervall konfigurieren**.  
  
![der entsprechenden Windows PowerShell-](../../../media/Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
> [!NOTE]  
> Der Befehl für den Vorgangs Status eines Clusters ist als Verweis enthalten.  
  
```  
PS> Get-RemoteAccessHealth  
PS> Get-RemoteAccessHealth -Cluster  
```  
  


