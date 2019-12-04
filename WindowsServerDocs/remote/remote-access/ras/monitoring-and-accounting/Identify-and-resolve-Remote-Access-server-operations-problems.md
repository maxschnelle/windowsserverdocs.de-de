---
title: Identifizieren und Beheben von Betriebsproblemen auf dem Remotezugriffsserver
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ce84c9f-fd1f-4463-8fc7-d2f33344a2c9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 831f484db8325bf9a27e9065ac5cf74913d0805c
ms.sourcegitcommit: 4a03f263952c993dfdf339dd3491c73719854aba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2019
ms.locfileid: "74791160"
---
# <a name="identify-and-resolve-remote-access-server-operations-problems"></a>Identifizieren und Beheben von Betriebsproblemen auf dem Remotezugriffsserver

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

**Hinweis:** Durch Windows Server 2012 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Mithilfe der folgenden Verfahren können Sie Probleme bei RAS-Server Vorgängen, ihre Hauptursachen und die Lösung ermitteln, die zum Beheben der Probleme erforderlich ist.  
  
> [!NOTE]  
> Sie müssen auf jedem Computer als Mitglied der Gruppe "Domänen-Admins" oder "Administratoren" angemeldet sein, um die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht ausführen können, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Administratoren" ist, versuchen Sie, die Aufgabe auszuführen, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Domänen-Admins" ist.  
  
Dieses Thema enthält Informationen zum Ausführen der folgenden Aufgaben:  
  
- Simulieren eines Vorgangs Problems  
  
- Identifizieren des Vorgangs Problems und ergreifen von Korrekturmaßnahmen  
  
- Wiederherstellen des IP Helper-Dienes  
  
### <a name="BKMK_Simulate"></a>Simulieren eines Vorgangs Problems  
  
> [!CAUTION]  
> Da der RAS-Server wahrscheinlich ordnungsgemäß konfiguriert ist und keine Probleme aufgetreten sind, können Sie das folgende Verfahren verwenden, um ein Vorgangs Problem zu simulieren. Wenn Ihr Server momentan Clients in einer Produktionsumgebung verarbeitet, möchten Sie diese Aktionen möglicherweise zu diesem Zeitpunkt nicht durchführen. Stattdessen können Sie die Schritte lesen, um zu verstehen, wie Sie Probleme beheben können, die in Zukunft auf dem RAS-Server auftreten können.  
  
Der IP-Hilfsdienst (iphlpsvc) hostet IPv6-Übergangs Technologien (z. b. IP-HTTPS, IPv6-zu-IPv4 oder Teredo) und ist erforderlich, damit der DirectAccess-Server ordnungsgemäß funktioniert. Zum veranschaulichen eines simulierten Vorgangs Problems auf dem RAS-Server müssen Sie den Netzwerkdienst (iphlpsvc) unterbinden.  
  
##### <a name="to-stop-the-ip-helper-service"></a>So verhindern Sie den IP-Hilfsdienst  
  
1.  Klicken Sie auf dem **Start** Bildschirm des Remote Zugriffs Servers auf **Verwaltung**, und doppelklicken Sie dann auf **Dienste**.  
  
2.  Scrollen Sie in der Liste der **Dienste**nach unten, **und klicken Sie**mit der rechten Maustaste auf **IP**-Hilfsobjekt.  
  
### <a name="BKMK_Identify"></a>Identifizieren des Vorgangs Problems und ergreifen von Korrekturmaßnahmen  
Das Ausschalten des IP-Hilfsobjekts führt zu einem schwerwiegenden Fehler auf dem RAS-Server. Das Dashboard für die Überwachung zeigt den Betriebsstatus des Servers und die Details des Problems an.  
  
##### <a name="to-identify-the-details-and-take-corrective-action"></a>So identifizieren Sie die Details und ergreifen Korrekturmaßnahmen  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **DASHBOARD**, um in der **Remotezugriffs-Verwaltungskonsole** zum **Remotezugriffdashboard** zu navigieren.  
  
3.  Stellen Sie sicher, dass der Remote Zugriffs Server im linken Bereich ausgewählt ist, und klicken Sie dann im mittleren Bereich auf **Vorgangs Status**.  
  
4.  Die Liste der Komponenten mit grünen oder roten Symbolen wird angezeigt, die den Betriebsstatus angeben. Klicken Sie in der Liste auf die Zeile **IP-HTTPS** . Wenn Sie eine Zeile ausgewählt haben, werden die Details für den Vorgang wie folgt im **Detail** Bereich angezeigt:  
  
    **Fehler**  
  
    Der IP-Hilfsdienst (iphlpsvc) wurde beendet. DirectAccess funktioniert möglicherweise nicht wie erwartet. Der IP-Hilfsdienst bietet Tunnel Konnektivität mithilfe der Konnektivitätsplattform, IPv6-Übergangs Technologien und IP-HTTPS.  
  
    **Gründe**  
  
    1.  Der IP-Hilfsdienst wurde beendet.  
  
    2.  Der IP-Hilfsdienst antwortet nicht.  
  
    **Lösung**  
  
    1.  Um sicherzustellen, dass der Dienst ausgeführt wird, geben Sie an einer Windows PowerShell-Eingabeaufforderung **Get-Service iphlpsvc** ein.  
  
    2.  Um den Dienst zu aktivieren, geben Sie an einer Windows PowerShell-Eingabeaufforderung mit erhöhten **rechten Start-Service iphlpsvc** ein.  
  
    3.  Um den Dienst neu zu starten, geben Sie an einer Windows PowerShell-Eingabeaufforderung mit erhöhten **rechten Restart-Service iphlpsvc** ein.  
  
### <a name="BKMK_Restart"></a>Wiederherstellen des IP Helper-Dienes  
Um den IP-Hilfsdienst auf Ihrem RAS-Server wiederherzustellen, können Sie die oben beschriebenen Lösungsschritte ausführen, um den Dienst zu starten oder neu zu starten, oder Sie können das folgende Verfahren verwenden, um das Verfahren umzukehren, das Sie zum Simulieren des Fehlers bei IP-Hilfsobjekten verwendet haben.  
  
##### <a name="to-restart-the-ip-helper-service-on-the-remote-access-server"></a>So starten Sie den IP Helper-Dienst auf dem Remote Zugriffs Server neu  
  
1.  Klicken Sie auf dem Bildschirm **Start** auf **Verwaltung**, und doppelklicken Sie dann auf **Dienste**.  
  
2.  Scrollen Sie in der Liste der **Dienste**nach unten, **und klicken Sie**mit der rechten Maustaste auf **IP**-Hilfsobjekt.  
  
![der entsprechenden Windows PowerShell-](../../../media/Identify-and-resolve-Remote-Access-server-operations-problems/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```PowerShell
PS> Get-RemoteAccessHealth | Where-Object {$_.Component -eq "IP-HTTPS"} | Format-List -Property *  
```
