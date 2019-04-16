---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Technische Referenz zu Windows Time Service
description: ''
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 02/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 916ac654aeb1ca56e0283f9a18e011ef67734776
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="windows-time-service-technical-reference"></a>Technische Referenz zu Windows Time Service
Der W32Time-Dienst bietet Netzwerk Computertakts für Computer ohne umfassende Konfiguration. Der W32Time-Dienst ist wichtig für die erfolgreiche Ausführung des Kerberos V5-Authentifizierung und daher auf AD DS-basierte Authentifizierung. Kerberos-fähige Anwendung, die meisten Sicherheitsdienste einschließlich stützt sich auf die zeitsynchronisierung zwischen den Computern, die in die Authentifizierungsanforderung berücksichtigt werden. AD DS-Domänencontrollern müssen auch Uhren, um genau die Datenreplikation sicherstellen synchronisiert.

> [!NOTE]  
> In Windows Server 2003 und Microsoft Windows 2000 Server heißt der Verzeichnisdienst Active Directory-Dienst. In Windows Server 2008 R2 und Windows Server 2008 heißt der Verzeichnisdienst Active Directory-Domänendienste (AD DS). Im weiteren Verlauf dieses Themas bezieht sich auf AD DS, aber die Informationen gilt auch für Active Directory-Domänendienste in Windows Server 2016.

Der W32Time-Dienst in einer dynamic Link Library aufgerufen W32Time.dll, das installiert wird, wird standardmäßig in implementiert ist **%Systemroot%\System32**. W32Time.dll wurde ursprünglich für Windows 2000 Server, auf denen eine Spezifikation das Kerberos V5-Authentifizierungsprotokoll entwickelt, die Uhrzeit in einem Netzwerk zu synchronisierenden erforderlich. Ab Windows Server2003, bereitgestellt W32Time.dll höhere Genauigkeit im Netzwerk des Computertakts, über das Windows Server2000-Betriebssystem. Darüber hinaus unterstützt W32Time.dll in Windows Server2003 eine Vielzahl von Hardwaregeräten und Zeit Netzwerkprotokolle Zeitanbieter verwenden.

Obwohl ursprünglich Computertakts Kerberos-Authentifizierung bereitstellen, verwenden viele aktuelle Anwendungen Zeitstempel, um Konsistenz zu gewährleisten, notieren Sie den Zeitpunkt der wichtige Ereignisse und andere unternehmenskritische zeitabhängige Informationen.  Diese Apps profitieren von zeitsynchronisierung zwischen Computern, die von der Windows-Zeitdienst bereitgestellt werden.

## <a name="importance-of-time-protocols"></a>Bedeutung der Zeit Protokolle
Zeit Protokolle Kommunikation zwischen zwei Computern zum Austausch von Informationen, und klicken Sie dann diese Informationen verwenden, um ihre Uhren synchronisieren. Mit dem Windows-Zeitdienst Service Time-Protokoll ein Client fordert Informationen von einem Server und synchronisiert die Uhr auf Basis der Informationen, die empfangen werden.
  
Windows-Zeitdienst verwendet NTP, um die Zeit in einem Netzwerk zu synchronisieren. NTP ist ein Internet-Zeit-Protokoll, das die Disziplin Algorithmen für die Synchronisierung von Uhren erforderlichen enthält. NTP ist eine genauere NTP als SNTP Simple Network Time Protocol (), die in einigen Versionen von Windows verwendet wird. Allerdings unterstützt auch weiterhin W32Time SNTP um Abwärtskompatibilität mit Zeit SNTP-basierte Dienste wie z. B. Windows 2000-Computern zu aktivieren.
<!-- maybe this should be its own topic under the Tech Ref section -->
## <a name="BKMK_Config"></a>Windows-Zeitdienst-Dienst im Zusammenhang mit Konfiguration Informationsquellen  
Dieses Handbuch ist **nicht** Konfigurieren der Windows-Zeitdienst erläutert. Es gibt mehrere unterschiedliche Themen im Microsoft TechNet und in der Microsoft Knowledge Base, in denen Verfahren zum Konfigurieren der Windows-Zeitdienst. Wenn Sie Informationen benötigen, sollten in den folgenden Themen finden Sie die entsprechende Informationen finden.  
<!-- should this be an if/then table -->
-   Zum Konfigurieren der Windows-Zeitdienst für die Gesamtstruktur Stamm Emulators primärer Domänencontroller (PDC) finden Sie unter:  
  
    -   [Konfigurieren des Windows-Zeitdiensts auf dem PDC-Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [Konfigurieren eine Zeitquelle für die Gesamtstruktur](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft Knowledge Base-Artikel 816042, [Vorgehensweise beim Konfigurieren eines autorisierenden Zeitservers in Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402), welche beschreibt die Konfigurationseinstellungen für Computer unter Windows Server2008 R2, Windows Server2008, Windows Server2003 und Windows Server2003 R2.  
  
-   Zum Konfigurieren des Windows-Zeitdiensts auf jedem Domain Member Client oder Server, oder sogar Domänencontroller, die nicht als Gesamtstruktur Root PDC-Emulator konfiguriert sind, finden Sie unter [Konfigurieren eines Clientcomputers für automatischen Synchronisierung](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
    > [!WARNING]  
    > Einige Anwendungen erfordern ihre Computer präzise Zeit Dienste haben. Wenn dies der Fall ist, können Sie eine manuelle Zeitquelle konfigurieren, aber beachten Sie, dass der Windows-Zeitdienst nicht als eine enorm präzise Zeitquelle ausgelegt ist. Stellen Sie sicher, dass Sie die Einschränkungen für präzise Zeit Umgebungen wie im Microsoft Knowledge Base-Artikel 939322, beschrieben sind [Unterstützung Grenze so konfigurieren Sie die Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](https://go.microsoft.com/fwlink/?LinkID=179459).  
  
-   So konfigurieren Sie die Windows-Zeitdienst auf allen Windows-basierten Client oder Server-Computern, die konfiguriert sind, wie der Arbeitsgruppenmitglieder, anstelle der Mitglieder der Domäne finden Sie unter [konfigurieren Sie eine manuelle Zeitquelle für einen ausgewählten Clientcomputer](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29).  
  
-   Zum Konfigurieren von Windows-Zeitdienst auf einem Hostcomputer, der eine virtuelle Umgebung ausgeführt wird, finden Sie im Microsoft Knowledge Base-Artikel 816042, [Vorgehensweise beim Konfigurieren eines autorisierenden Zeitservers in Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402). Wenn Sie ein nicht-Microsoft-Virtualisierungs-Produkt verwenden, achten Sie darauf, dass Sie die Dokumentation des Herstellers für das Produkt.  
  
-   Um die Windows-Zeitdienst auf einem Domänencontroller zu konfigurieren, die auf einem virtuellen Computer ausgeführt wird, wird empfohlen, die zeitsynchronisierung zwischen dem Betriebssystem des Hosts und dem Gastbetriebssystem, der als Domänencontroller fungiert teilweise zu deaktivieren. Dies ermöglicht dem Gast-Domänencontroller zum Synchronisieren der Zeit für die Domänenhierarchie aber verhindert, dass Sie einen Zeitversatz, wenn sie aus einem gespeicherten Zustand wiederhergestellt wird. Weitere Informationen finden Sie im Microsoft Knowledge Base-Artikel 976924, [erhalten Sie die Windows-Zeitdienst Ereignis-IDs 24, 29 und 38 auf einem virtualisierten Domänencontroller, die auf einem Windows Server2008-basierten Hostserver mit Hyper-V ausgeführt wird](https://go.microsoft.com/fwlink/?LinkID=192236) und [Bereitstellungsüberlegungen für virtualisierte Domänencontroller](https://go.microsoft.com/fwlink/?LinkID=192235).  
  
-   Zum Konfigurieren des Windows-Zeitdiensts auf einem Domänencontroller, der als des Gesamtstruktur Root PDC-Emulators, die auch auf einem virtuellen Computer ausgeführt wird, führen Sie die gleichen Schrittefür einen physischen Computer beschriebenen [konfigurieren den Windows-Zeitdienst auf dem primären Domänencontroller Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29).  
  
-   Verwenden Sie zum Konfigurieren des Windows-Zeitdiensts auf einem Mitgliedsserver ausgeführt wird als virtueller Computer Zeit Domänenhierarchie siehe ([Konfigurieren eines Clientcomputers für automatischen Synchronisierung](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).


> [!IMPORTANT]  
> Vor Windows Server 2016 wurde der W32Time-Dienst nicht für zeitabhängige Anwendung Anforderungen entwickelt.  Updates für Windows Server 2016 jetzt können Sie jedoch zum Implementieren einer Lösung für 1ms Genauigkeit in Ihrer Domäne.  Weitere Informationen finden Sie unter [Windows 2016 genau Zeit](accurate-time.md) und [Unterstützung Grenze so konfigurieren Sie die Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](https://go.microsoft.com/fwlink/?LinkID=179459) Weitere Informationen.

## <a name="related-topics"></a>Verwandte Themen  
[Wie funktioniert der Windows-Zeitdienst](How-the-Windows-Time-Service-Works.md)  
[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)