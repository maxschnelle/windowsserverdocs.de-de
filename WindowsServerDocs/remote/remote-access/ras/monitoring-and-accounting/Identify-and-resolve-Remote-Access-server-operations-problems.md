---
title: Identifizieren und Beheben von Betriebsproblemen auf dem Remotezugriffsserver
description: Dieses Thema ist Teil des Leitfadens für die Überwachung des Remotezugriffs und Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ce84c9f-fd1f-4463-8fc7-d2f33344a2c9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b682685883a2200caf8f4286674bb3e2cbe6651b
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282781"
---
# <a name="identify-and-resolve-remote-access-server-operations-problems"></a>Identifizieren und Beheben von Betriebsproblemen auf dem Remotezugriffsserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Durch Windows Server 2013 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Sie können mithilfe der folgenden Verfahren zum Identifizieren von Betriebsproblemen auf dem Remote-Zugriff, die Ursachen und die Auflösung erforderlich, um die Probleme zu beheben.  
  
> [!NOTE]  
> Sie müssen als Mitglied der Gruppe "Domänen-Admins" oder ein Mitglied der Gruppe "Administratoren" auf jedem Computer angemeldet sein, die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht abschließen können, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Administratoren" ist, versuchen Sie es die Aufgabe auszuführen, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Domänen-Admins" ist.  
  
Dieses Thema enthält Informationen über die folgenden Aufgaben ausführen:  
  
- Simulieren Sie ein Problem Vorgänge  
  
- Das Operations-Problem identifizieren und korrekturmaßnahmen  
  
- Wiederherstellen des IP-Hilfsdienstes  
  
### <a name="BKMK_Simulate"></a>Simulieren Sie ein Problem Vorgänge  
  
> [!CAUTION]  
> Da Ihre RAS-Server wahrscheinlich ist so konfiguriert, ordnungsgemäß ist und nicht auf Probleme, können Sie das folgende Verfahren, um ein Problem Vorgänge zu simulieren. Wenn Clients in einer produktionsumgebung von Ihrem Server aktuell verwendet wird, sollten Sie nicht diese Aktionen zu diesem Zeitpunkt ausführen. Stattdessen erhalten Sie durch die Schritte zum verstehen, wie Sie Probleme beheben, die auf dem RAS-Server in der Zukunft auftreten können.  
  
Die IP Helper-Dienst (IPHlpSvc) Hosts IPv6-Übergang-Technologien (z. B. IP-HTTPS, 6to4 oder Teredo), und es ist erforderlich, damit der DirectAccess-Server ordnungsgemäß funktioniert. Um ein Problem simulierten Vorgänge auf dem RAS-Server zu demonstrieren, müssen Sie den Netzwerkdienst (IPHlpSvc) beenden.  
  
##### <a name="to-stop-the-ip-helper-service"></a>So beenden Sie die IP-Hilfsdienst  
  
1.  Auf der **starten** Bildschirm der RAS-Servers, klicken Sie auf **Verwaltung**, und doppelklicken Sie dann auf **Services**.  
  
2.  In der Liste der **Services**, scrollen Sie nach unten, und mit der rechten Maustaste **IP Helper**, und klicken Sie dann auf **beenden**.  
  
### <a name="BKMK_Identify"></a>Das Operations-Problem identifizieren und korrekturmaßnahmen  
Durch das Deaktivieren des IP-Hilfsdienstes führt eines schwerwiegenden Fehlers auf dem RAS-Server. Das überwachungsdashboard zeigt den Status der Vorgänge des Servers und die Details des Problems.  
  
##### <a name="to-identify-the-details-and-take-corrective-action"></a>Um die Details zu identifizieren und korrekturmaßnahmen  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **DASHBOARD**, um in der **Remotezugriffs-Verwaltungskonsole** zum **Remotezugriffdashboard** zu navigieren.  
  
3.  Stellen Sie sicher, dass Ihre RAS-Server im linken Bereich ausgewählt ist, und klicken Sie dann im mittleren Bereich auf **Vorgangsstatus**.  
  
4.  Sie sehen die Liste der Komponenten mit der grüne oder rote-Symbole, die deren Betriebsstatus angeben. Klicken Sie auf die **IP-HTTPS** Zeile in der Liste. Wenn Sie eine Zeile ausgewählt haben, werden die Details für den Vorgang angezeigt, der **Details** Bereich wie folgt:  
  
    **Fehler**  
  
    Der IP-Hilfsdienst (IPHlpSvc) wurde beendet. DirectAccess unter Umständen nicht erwartungsgemäß. Der IP-Hilfsdienst stellt tunnelkonnektivität mithilfe des Konnektivität-Plattform, die IPv6-übergangstechnologien und die IP-HTTPS.  
  
    **Bewirkt, dass**  
  
    1.  Der IP Helper-Dienst wurde beendet.  
  
    2.  Der IP-Hilfsdienst reagiert nicht.  
  
    **Lösung**  
  
    1.  Um sicherzustellen, dass der Dienst ausgeführt wird, geben Sie **Get-Service-Iphlpsc** an Windows PowerShell-Eingabeaufforderung.  
  
    2.  Um den Dienst zu aktivieren, geben **Start-Service-Iphlpsvc** ein Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten.  
  
    3.  Geben Sie zum Neustarten des Diensts **Restart-Service-Iphlpsvc** ein Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten.  
  
### <a name="BKMK_Restart"></a>Wiederherstellen des IP-Hilfsdienstes  
Um die IP-Hilfsdienst auf dem RAS-Server wiederherzustellen, können Sie die Schritte oben zum Starten oder Neustarten des Diensts folgen, oder können wie folgt vor, die Prozedur umzukehren, die Sie verwendet, um den IP-Hilfs-Dienstfehler zu simulieren.  
  
##### <a name="to-restart-the-ip-helper-service-on-the-remote-access-server"></a>Den IP Helper-Dienst auf dem RAS-Server neu gestartet  
  
1.  Auf der **starten** auf **Verwaltung**, und doppelklicken Sie dann auf **Services**.  
  
2.  In der Liste der **Services**, scrollen Sie nach unten, und mit der rechten Maustaste **IP Helper**, und klicken Sie dann auf **starten**.  
  
![Windows PowerShell](../../../media/Identify-and-resolve-Remote-Access-server-operations-problems/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
PS> Get-RemoteAccessHealth | Where-Object {$_.Component -eq "IP-HTTPS"} | Format-List -Property *  
```  
  


