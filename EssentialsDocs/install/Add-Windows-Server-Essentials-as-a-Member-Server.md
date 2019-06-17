---
title: Hinzufügen von Windows Server Essentials als Mitgliedsserver
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: 502e54cf719895dd11030cf163159f6cdda47164
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433730"
---
# <a name="add-windows-server-essentials-as-a-member-server"></a>Hinzufügen von Windows Server Essentials als Mitgliedsserver

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Thema bezieht sich auf einem Server unter Windows Server 2012 R2 Standard, Windows Server 2012 R2 Datacenter oder Windows Server 2016 mit installierter Windows Server Essentials Experience-Rolle. Im weiteren Verlauf dieses Dokuments wird die Windows Server Essentials Experience-Rolle als Windows Server Essentials bezeichnet.  
  
> [!NOTE]
>   Windows Server Essentials kann nur als Domänencontroller bereitgestellt werden. In diesem Dokument umfasst Windows Server Essentials nicht Windows Server Essentials.  
  
 Windows Server Essentials muss kein primärer Server innerhalb einer Windows-Domäne sein. Sie können Windows Server Essentials zu einer vorhandenen Active Directory-Domänenumgebung als Mitgliedsserver hinzufügen, um einfache Features für Datenschutz, sicheren Remotezugriff und Cloudintegration zu nutzen. Darüber hinaus kann Windows Server Essentials ohne einen Domänencontroller in einer vorhandenen Active Directory-Umgebung bereitgestellt werden. Dadurch können Sie den Speicher erweitern oder eine Filiale für lokalen Speicher und Verwaltung verwenden.  
  
 Sie können Windows Server Essentials in den folgenden Szenarien hinzufügen:  
  
-   Fügen Sie Windows Server Essentials in einer Filiale hinzu und fügen Sie diese zum Domänencontroller, der sich in der Hauptniederlassung an einem anderen Speicherort befindet, unter Verwendung der systemeigenen Tools hinzu. Sie können die BranchCache-Features für eine optimale Bandbreitennutzung auf diesem Mitgliedsserver aktivieren.  
  
-   Hinzufügen von Windows Server Essentials als Mitgliedsserver in einer Windows Server Essentials-Netzwerk, um von Speicher in Ihrem Netzwerk zu erweitern, indem Sie zusätzliche Serverordner auf Ihrem Mitgliedsserver hinzufügen.  
  
-   Fügen Sie Windows Server Essentials als Mitgliedsserver in der Filiale hinzu, wenn Ihr primäre Server mit Windows Server Essentials in Microsoft Azure gehostet wird, oder von einem drittanbieterhoster gehostet wird. Windows Server Essentials als Mitgliedsserver an Ihrem Filialstandort hilft Ihnen bei der Optimierung der Auslastung der Netzwerkbandbreite.  
  
## <a name="adding-windows-server-essentials-as-a-member-server"></a>Hinzufügen von Windows Server Essentials als Mitgliedsserver  
 Um Windows Server Essentials als Mitgliedsserver zu einem primären Server mit Windows Server 2012 R2 oder Windows Server Essentials in einer vorhandenen Active Directory-Umgebung hinzuzufügen, müssen Sie die folgenden Schritte ausführen:  
  
1.  Fügen Sie den Server, der unter Windows Server Essentials ausgeführt wird, zu einer Arbeitsgruppe hinzu.  
  
2.  Fügen Sie den Server, die mit Windows Server Essentials, mit der Domäne eines primären Windows Server Essentials-Servers ein.  
  
3.  Konfigurieren Sie Windows Server Essentials Experience in Server-Manager.  
  
#### <a name="to-join-windows-server-essentials-to-a-workgroup-or-domain"></a>So fügen Sie Windows Server Essentials zu einer Domäne oder Arbeitsgruppe hinzu  
  
1. Schließen Sie nach Abschluss der Installation von Windows Server Essentials auf Ihrem zweiten Server den Assistenten zum Konfigurieren von Windows Server Essentials.  
  
2. Geben Sie im Feld **Suche** **System Settings**ein, und klicken Sie in den Suchergebnissen auf **Erweiterte Systemeinstellungen anzeigen**.  
  
3. Klicken Sie in **Systemeigenschaften** auf die Registerkarte **Computername**.  
  
4. Klicken Sie in **Computername**im Bereich **Domäne** auf **Ändern**.  
  
5. In **Änderung des Computernamens bzw, der Domäne**in die **Member** wählen sollten Sie den Server mit Windows Server Essentials zu verbinden einer **Arbeitsgruppe** oder eine **Domäne**.  
  
   -   Um den Server zu einer Arbeitsgruppe hinzuzufügen, geben Sie **workgroup** ein, und klicken Sie dann auf **OK**.  
  
   -   Um diesen Server mit einer vorhandenen Active Directory-Domäne zu verknüpfen, geben Sie den Namen der Domäne ein, und klicken Sie dann auf **OK**.  
  
6. Starten Sie den Server erneut, um die Änderungen zu übernehmen.  
  
   Nachdem Sie den Server mit der Domäne des primären Servers s hinzugefügt haben, können Sie weiterhin Windows Server Essentials konfigurieren, indem Sie Ausführung der Konfigurieren von Windows Server Essentials-Assistenten im Server-Manager.  
  
#### <a name="to-configure-windows-server-essentials-experience-on-a-member-server"></a>So konfigurieren Sie Windows Server Essentials Experience auf einem Mitgliedsserver  
  
1.  (Optional) Ändern Sie den Namen des Servers.  
  
    > [!IMPORTANT]
    >  Sie können nicht den Namen des Servers nicht ändern, nachdem Sie Windows Server Essentials-Umgebung konfiguriert haben.  
  
2.  Melden Sie sich mit Ihrem Domänenadministratorkonto auf dem Server an.  
  
3.  Öffnen Sie den Server-Manager.  
  
4.  Klicken Sie im Meldungsinfobereich im **Server-Manager** auf Flag, und dann auf **Windows Server Essentials konfigurieren**.  
  
5.  Wählen Sie die Option zum Konfigurieren des Servers als Mitgliedsserver, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf **Konfigurieren**, um die Konfiguration zu beginnen. Die Konfiguration dauert ungefähr 10 Minuten.  
  
7.  Klicken Sie auf dem Desktop auf das Dashboardsymbol, um das Serverdashboard zu starten. Führen Sie auf der Homepage die Aufgaben für **Erste Schritte** aus, die auf der Registerkarte **Setup** aufgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

-   [Installieren von Windows Server Essentials](../install/Install-Windows-Server-Essentials.md)

