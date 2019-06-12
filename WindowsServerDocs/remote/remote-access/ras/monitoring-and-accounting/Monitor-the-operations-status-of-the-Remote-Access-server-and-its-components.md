---
title: Überwachen des Betriebsstatus des Remotezugriffsservers und dessen Komponenten
description: Dieses Thema ist Teil des Leitfadens für die Überwachung des Remotezugriffs und Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 077a3a64-2fa3-4994-9711-ec1fbdc081ba
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7f4c7e1418e541e1f913c8a20cbda3456c1c3802
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446598"
---
# <a name="monitor-the-operations-status-of-the-remote-access-server-and-its-components"></a>Überwachen des Betriebsstatus des Remotezugriffsservers und dessen Komponenten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Durch Windows Server 2013 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Die-Verwaltungskonsole auf dem RAS-Server kann verwendet werden, um den Status der Vorgänge zu überwachen.  
  
> [!NOTE]  
> Sie müssen als Mitglied der Gruppe "Domänen-Admins" oder ein Mitglied der Gruppe "Administratoren" auf jedem Computer angemeldet sein, zum Abschließen der Aufgabe, die in diesem Thema beschrieben. Wenn Sie eine Aufgabe nicht abschließen können, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Administratoren" ist, versuchen Sie es die Aufgabe auszuführen, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-monitor-the-remote-access-server-operations-status"></a>Überwachen des Betriebsstatus des RAS-server  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **DASHBOARD** , zu dem navigiert **Remoteberichte Zugriff** in die **Remotezugriffs-Verwaltungskonsole**.  
  
3.  Beachten Sie, dass das Dashboard für die **Vorgangsstatus** Kachel innerhalb der **Serverstatus** Kachel. Auf dieser Kachel werden die Vorgänge des Status und den Status der Komponenten für alle Server aufgelistet.  
  
4.  Klicken Sie auf **aktualisieren** unter **Aufgaben** im rechten Bereich, den Status der Vorgänge neu zu laden. Der Vorgangsstatus wird automatisch alle fünf Minuten aktualisiert werden, dies ist das Standardaktualisierungsintervall. Um das standardmäßige Aktualisierungsintervall ändern möchten, klicken Sie auf **Aktualisierungsintervall konfigurieren**.  
  
![Windows PowerShell](../../../media/Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
> [!NOTE]  
> Der Befehl für den Betriebsstatus eines Clusters ist sind zu Referenzzwecken.  
  
```  
PS> Get-RemoteAccessHealth  
PS> Get-RemoteAccessHealth -Cluster  
```  
  


