---
title: Überprüfen von Client Computer Einstellungen
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 31ea58b0-d407-4f62-8ec6-6a1b19174042
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 14fcc91fc1fcf419a81dd5d774486dc5e0800f4e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937549"
---
# <a name="verify-client-computer-settings"></a>Überprüfen von Client Computer Einstellungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie überprüfen, ob der Client Computer für BranchCache ordnungsgemäß konfiguriert ist.

> [!NOTE]
> Dieses Verfahren umfasst die Schritte zum manuellen Aktualisieren von Gruppenrichtlinie und zum Neustarten des BranchCache-Dienstanbieter. Sie müssen diese Aktionen nicht ausführen, wenn Sie den Computer neu starten, da Sie in diesem Fall automatisch auftreten werden.

Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

### <a name="to-verify-branchcache-client-computer-settings"></a>So überprüfen Sie die BranchCache-Client Computereinstellungen

1.  Um Gruppenrichtlinie auf dem Client Computer zu aktualisieren, dessen BranchCache-Konfiguration Sie überprüfen möchten, führen Sie Windows PowerShell als Administrator aus, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

    `gpupdate /force`

2.  Führen Sie für Client Computer, die im Modus "gehosteter Cache" konfiguriert sind und für die automatische Ermittlung von gehosteten Cache Servern nach Dienst Verbindungspunkt konfiguriert sind, die folgenden Befehle aus, um den BranchCache-Dienst zu starten

    `net stop peerdistsvc`

    `net start peerdistsvc`

3.  Überprüfen Sie den aktuellen BranchCache-Betriebsmodus, indem Sie den folgenden Befehl ausführen.

    `Get-BCStatus`

4.  Überprüfen Sie die Ausgabe des Befehls **Get-bcstatus** in Windows PowerShell.

    Der Wert für **branchcacheisenabled** sollte " **true**" lauten.

    In **Client Settings**sollte der Wert für **currentclientmode** in Abhängigkeit vom Modus, den Sie in diesem Handbuch konfiguriert haben, " **distributedclient** " oder " **hustedcacheclient**" lauten.

    Wenn Sie in **Client Settings**den gehosteten Cache Modus konfiguriert und die Namen der gehosteten Cache Server während der Konfiguration bereitgestellt haben, oder wenn der Client mithilfe von Dienst Verbindungs Punkten automatisch gehostete Cache Server gefunden hat, sollte **hostedcacheserverlist** einen Wert aufweisen, der mit dem Namen oder den Namen der gehosteten Cache Server identisch ist. Wenn der gehostete Cache Server z. b. den Namen HCS1 hat und Ihre Domäne corp.contoso.com ist, lautet der Wert für **hostedcacheserverlist** **HCS1.Corp.contoso.com**.

5.  Wenn eine der oben aufgeführten BranchCache-Einstellungen nicht über die korrekten Werte verfügt, verwenden Sie die Schritte in diesem Handbuch, um die Richtlinien Einstellungen für Gruppenrichtlinie oder lokale Computer sowie die von Ihnen konfigurierten Firewallausnahmen zu überprüfen und sicherzustellen, dass Sie richtig sind. Starten Sie außerdem den Computer neu, oder führen Sie die Schritte in diesem Verfahren aus, um Gruppenrichtlinie zu aktualisieren und den BranchCache-Dienst neu zu starten.



