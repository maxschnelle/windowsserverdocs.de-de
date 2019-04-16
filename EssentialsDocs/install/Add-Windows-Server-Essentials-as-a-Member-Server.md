---
title: "Hinzufügen von Windows Server Essentials als Mitgliedsserver"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d09dd82f-f7d2-47ce-862d-fd9869f2021c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8fb73f8186d3984c9e93f7a6e39cb72a54db1e58
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="add-windows-server-essentials-as-a-member-server"></a>Hinzufügen von Windows Server Essentials als Mitgliedsserver

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Thema bezieht sich auf einem Server mit Windows Server 2012 R2 Standard, Windows Server 2012 R2 Datacenter oder Windows Server 2016 mit installierter Windows Server Essentials Experience-Rolle. Im weiteren Verlauf dieses Dokuments wird Windows Server Essentials Experience-Rolle als Windows Server Essentials bezeichnet werden.  
  
> [!NOTE]
>   Windows Server Essentials kann nur als Domänencontroller bereitgestellt werden. In diesem Dokument umfasst Windows Server Essentials nicht Windows Server Essentials.  
  
 Windows Server Essentials muss nicht als primärer Server innerhalb einer Windows-Domäne. Sie können einer vorhandenen Active Directory-Domäne-Umgebung Windows Server Essentials als Mitgliedsserver hinzufügen und nutzen Sie die einfache Datenschutz, sicheren Remotezugriff und Cloud-Integration-Features, die es enthält. Darüber hinaus kann Windows Server Essentials in einer vorhandenen Active Directory-Umgebung bereitgestellt werden, ohne dass ein Domänencontroller sein. Dadurch können Sie den Speicher erweitern oder eine Filiale für lokalen Speicher und Verwaltung verwenden.  
  
 Sie können Windows Server Essentials in den folgenden Szenarien hinzufügen:  
  
-   Hinzufügen von Windows Server Essentials in einer Filiale, und fügen Sie ihn mit dem Domänencontroller, der in der hauptniederlassung an einem anderen Speicherort befindet, mithilfe der systemeigenen Tools hinzu. Sie können die BranchCache-Features für eine optimale bandbreitennutzung auf diesem Mitgliedsserver aktivieren.  
  
-   Hinzufügen von Windows Server Essentials als Mitgliedsserver in einem Windows Server Essentials-Netzwerk, Speicher in Ihrem Netzwerk zu erweitern, indem Sie zusätzliche Serverordner auf Ihrem Mitgliedsserver hinzufügen können.  
  
-   Hinzufügen von Windows Server Essentials als Mitgliedsserver in der Filiale, wenn Ihr primäre Server mit Windows Server Essentials in Microsoft Azure gehostet wird, oder von einem drittanbieterhoster gehostet wird. Müssen Sie Windows Server Essentials als Mitgliedsserver an Ihren lokalen Office-Website können zur Optimierung der Auslastung der Netzwerkbandbreite.  
  
## <a name="adding-windows-server-essentials-as-a-member-server"></a>Hinzufügen von Windows Server Essentials als Mitgliedsserver  
 Um Windows Server Essentials als Mitgliedsserver zu einem primären Server mit Windows Server 2012 R2 oder Windows Server Essentials in einer vorhandenen Active Directory-Umgebung hinzuzufügen, müssen Sie die folgenden Schritte ausführen:  
  
1.  Fügen Sie den Server mit Windows Server Essentials zu einer Arbeitsgruppe.  
  
2.  Fügen Sie die Server mit Windows Server Essentials der Domäne eines primären Windows Server Essentials-Servers.  
  
3.  Konfigurieren Sie die Windows Server Essentials-Umgebung über Server-Manager.  
  
#### <a name="to-join-windows-server-essentials-to-a-workgroup-or-domain"></a>Windows Server Essentials zu einer Arbeitsgruppe oder Domäne beitreten  
  
1.  Schließen Sie nach Abschluss der Installation von Windows Server Essentials auf Ihrem zweiten Server, Windows Server Essentials Assistenten zum Konfigurieren.  
  
2.  In der **Suche** geben **Systemeinstellungen**, und klicken Sie in den Suchergebnissen auf **Erweiterte Systemeinstellungen anzeigen**.  
  
3.  In **Systemeigenschaften**, klicken Sie auf die **Computername** Registerkarte.  
  
4.  In **Computername**in der **Domäne** auf **ändern**.  
  
5.  In **Computer bzw.-domänenänderungen**in der **Member** aus, wenn Sie den Server mit Windows Server Essentials zum beitreten möchten eine **Arbeitsgruppe** oder zu einer **Domäne**.  
  
    -   Um den Server zu einer Arbeitsgruppe hinzuzufügen, geben Sie **Arbeitsgruppe**, und klicken Sie dann auf **OK**.  
  
    -   Um diesen Server zu einer vorhandenen Active Directory-Domäne beizutreten, geben Sie den Namen der Domäne, und klicken Sie dann auf **OK**.  
  
6.  Starten Sie den Server aus, um die Änderungen zu übernehmen.  
  
 Nachdem Sie den Server der primäre Server s-Domäne hinzugefügt haben, können Sie weiterhin Windows Server Essentials durch Ausführen von Windows Server Essentials Assistenten zum Konfigurieren von Server-Manager konfigurieren.  
  
#### <a name="to-configure-windows-server-essentials-experience-on-a-member-server"></a>So konfigurieren Sie Windows Server Essentials Experience auf einem Mitgliedsserver  
  
1.  (Optional) Ändern Sie den Namen des Servers.  
  
    > [!IMPORTANT]
    >  Sie können nicht den Namen des Servers nicht ändern, nachdem Sie Windows Server Essentials-Umgebung konfiguriert haben.  
  
2.  Melden Sie sich an den Server mit der Domänen-Admins-Konto.  
  
3.  Öffnen Sie Server-Manager.  
  
4.  Klicken Sie im meldungsinfobereich im **Server-Manager**, klicken Sie auf das Kennzeichen, und klicken Sie dann auf **Konfigurieren von Windows Server Essentials**.  
  
5.  Aktivieren Sie zum Konfigurieren des Servers als Mitgliedsserver, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf **konfigurieren** an der Konfiguration zu beginnen. Die Konfiguration dauert ungefähr 10 Minuten.  
  
7.  Klicken Sie auf dem Desktop auf das Dashboard-Symbol, um das serverdashboard zu starten. Führen Sie auf der Startseite die **Einstieg** Aufgaben, die aufgeführt sind die **Setup** Registerkarte.  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

-   [Installieren von Windows Server Essentials](../install/Install-Windows-Server-Essentials.md)

