---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Technische Referenz für den Windows-Zeit Dienst
description: Der W32Time-Dienst ermöglicht die Synchronisierung von Netzwerk Uhren für Computer, ohne dass eine umfassende Konfiguration erforderlich ist. Der W32Time-Dienst ist für den erfolgreichen Betrieb der Kerberos V5-Authentifizierung und somit für die AD DS basierte Authentifizierung unverzichtbar.
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 04d39f222fbbc7943cc2074a857a76f38832935d
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919877"
---
# <a name="windows-time-service-technical-reference"></a>Technische Referenz für den Windows-Zeit Dienst
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Der W32Time-Dienst ermöglicht die Synchronisierung von Netzwerk Uhren für Computer, ohne dass eine umfassende Konfiguration erforderlich ist. Der W32Time-Dienst ist für den erfolgreichen Betrieb der Kerberos V5-Authentifizierung und somit für die AD DS basierte Authentifizierung unverzichtbar. Jede Kerberos-fähige Anwendung (einschließlich der meisten Sicherheitsdienste) basiert auf der Zeitsynchronisierung zwischen den Computern, die an der Authentifizierungsanforderung teilnehmen. AD DS Domänen Controllern müssen auch synchronisierte Uhren aufweisen, damit eine genaue Datenreplikation gewährleistet ist.

> [!NOTE]  
> In Windows Server 2003 und Microsoft Windows 2000 Server wird der Verzeichnisdienst Active Directory Verzeichnisdienst benannt. In Windows Server 2008 R2 und Windows Server 2008 heißt der Verzeichnisdienst Active Directory Domain Services (AD DS). Der Rest dieses Themas bezieht sich auf AD DS, die Informationen gelten jedoch auch für Active Directory Domain Services in Windows Server 2016.

Der W32Time-Dienst wird in einer Dynamic Link Library mit dem Namen "w32time. dll" implementiert, die standardmäßig in " **%SystemRoot%\System32**" installiert wird. W32time. dll wurde ursprünglich für Windows 2000 Server entwickelt, um eine Spezifikation durch das Kerberos V5-Authentifizierungsprotokoll zu unterstützen, das die Synchronisierung der Uhren in einem Netzwerk erforderte. Ab Windows Server 2003 hat w32time. dll eine größere Genauigkeit bei der Netzwerkzeit Synchronisierung über das Betriebssystem Windows Server 2000 bereitgestellt. Außerdem unterstützte w32time. dll in Windows Server 2003 eine Vielzahl von Hardware Geräten und Netzwerk Zeit Protokollen unter Verwendung von Zeit Anbietern.

Obwohl es ursprünglich für die Zeitsynchronisierung der Kerberos-Authentifizierung konzipiert wurde, verwenden viele aktuelle Anwendungen Zeitstempel, um die Transaktions Konsistenz sicherzustellen, die Zeit wichtiger Ereignisse aufzuzeichnen und andere geschäftskritische, Zeit empfindliche Informationen.  Diese Anwendungen profitieren von der Zeitsynchronisierung zwischen Computern, die vom Windows-Zeit Dienst bereitgestellt werden.

## <a name="importance-of-time-protocols"></a>Wichtigkeit von Zeit Protokollen
Zeitprotokolle kommunizieren zwischen zwei Computern, um Zeit Informationen auszutauschen, und verwenden diese Informationen dann, um die Uhren zu synchronisieren. Mit dem Zeitprotokoll für den Windows-Zeit Dienst fordert ein Client Zeit Informationen von einem Server an und synchronisiert seine Uhr basierend auf den empfangenen Informationen.
  
Der Windows-Zeit Dienst verwendet NTP, um die Zeit über ein Netzwerk zu synchronisieren. NTP ist ein Internet Zeitprotokoll, das die für die Synchronisierung von Uhren erforderlichen Disziplin Algorithmen umfasst. NTP ist ein genaueres Zeitprotokoll als das Simple Network Time Protocol (SNTP), das in einigen Versionen von Windows verwendet wird. Allerdings unterstützt W32Time weiterhin SNTP, um die Abwärtskompatibilität mit Computern zu ermöglichen, auf denen SNTP-basierte Zeit Dienste wie z. b. Windows 2000 ausgeführt werden.
## <a name="where-to-find-windows-time-service-configuration-related-information"></a>Wo finden Sie Informationen zur Windows-Zeit Dienst Konfiguration  
In diesem Handbuch wird die Konfiguration des Windows-Zeit Dienstanbieter **nicht** erläutert. In Microsoft TechNet und in der Microsoft Knowledge Base finden Sie verschiedene Themen, in denen erläutert wird, wie Sie den Windows-Zeit Dienst konfigurieren. Wenn Sie Konfigurationsinformationen benötigen, sollten Sie die folgenden Themen beim Auffinden der entsprechenden Informationen unterstützen.  
-   Informationen zum Konfigurieren des Windows-Zeit Diensts für den Gesamtstruktur Stamm-PDC-Emulator (Primary Domain Controller) finden Sie unter:
  
    -   [Konfigurieren des Windows-Zeit Diensts für den PDC-Emulator in der Stamm Domäne der Gesamtstruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [Konfigurieren einer Zeit Quelle für die Gesamtstruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft Knowledge Base-Artikel 816042, [Konfigurieren eines autorisierenden Zeit Servers in Windows Server, in](https://go.microsoft.com/fwlink/?LinkID=60402)dem die Konfigurationseinstellungen für Computer mit Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 und Windows Server 2003 R2 beschrieben werden.  
  
-   Informationen zum Konfigurieren des Windows-Zeit Diensts auf einem beliebigen Domänen Mitglieds Client oder-Server oder sogar auf Domänen Controllern, die nicht als PDC-Emulator für die Gesamtstruktur Stamm konfiguriert sind, finden Sie unter [Konfigurieren eines Client Computers für die automatische Synchronisierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)  
  
    > [!WARNING]  
    > Für einige Anwendungen ist es möglicherweise erforderlich, dass Ihre Computer über hohe Genauigkeit für Zeit Dienste verfügen. Wenn dies der Fall ist, können Sie eine manuelle Zeit Quelle konfigurieren, aber beachten Sie, dass der Windows-Zeit Dienst nicht als äußerst genaue Zeit Quelle konzipiert wurde. Stellen Sie sicher, dass Sie die Einschränkungen der Unterstützung für Umgebungen mit hoher Genauigkeit beachten, wie im Microsoft Knowledge Base-Artikel 939322, [Support Grenze zum Konfigurieren des Windows-Zeit Dienstanbieter für hochwertige Umgebungen](support-boundary.md)beschrieben.  
  
-   Informationen zum Konfigurieren des Windows-Zeit diensdienstanbieter auf Windows-basierten Client-oder Server Computern, die als Arbeitsgruppenmitglieder konfiguriert sind, anstelle von Domänen Mitgliedern finden Sie unter [Konfigurieren einer manuellen Zeit Quelle für einen ausgewählten Client Computer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29).  
  
-   Informationen zum Konfigurieren des Windows-Zeit Diensts auf einem Host Computer, auf dem eine virtuelle Umgebung ausgeführt wird, finden Sie im Microsoft Knowledge Base-Artikel 816042, [Konfigurieren eines autorisierenden Zeit Servers in Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402). Wenn Sie mit einem anderen Virtualisierungsprodukt als Microsoft arbeiten, lesen Sie die Dokumentation des Herstellers für dieses Produkt.  
  
-   Zum Konfigurieren des Windows-Zeit Diensts auf einem Domänen Controller, der auf einem virtuellen Computer ausgeführt wird, wird empfohlen, die Zeitsynchronisierung zwischen dem Host System und dem Gast Betriebssystem, das als Domänen Controller fungiert, teilweise zu deaktivieren. Auf diese Weise vermeiden Sie einen Zeitversatz, wenn der Gastdomänencontroller aus einem Zustand Gespeichert wiederhergestellt wird, behalten jedoch die Zeitsynchronisierung für die Domänenhierarchie bei. Weitere Informationen finden Sie im Microsoft Knowledge Base-Artikel 976924, [Sie erhalten die Windows-Zeit Dienst Ereignis-IDs 24, 29 und 38 auf einem virtualisierten Domänen Controller, der auf einem Windows Server 2008-basierten Host Server mit Hyper-V](https://go.microsoft.com/fwlink/?LinkID=192236) und [Bereitstellungs Überlegungen für virtualisierte Domänen Controller](https://go.microsoft.com/fwlink/?LinkID=192235)ausgeführt wird.  
  
-   Um den Windows-Zeit Dienst auf einem Domänen Controller zu konfigurieren, der als VM-Stamm-PDC-Emulator fungiert, der ebenfalls auf einem virtuellen Computer ausgeführt wird, befolgen Sie die gleichen Anweisungen für einen physischen Computer, wie in [Konfigurieren des Windows-Zeit Diensts auf dem PDC-Emulator in der Stamm Domäne](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)der Gesamtstruktur beschrieben.  
  
-   Um den Windows-Zeit Dienst auf einem Mitglieds Server zu konfigurieren, der als virtueller Computer ausgeführt wird, verwenden Sie die Domänen Zeit Hierarchie, wie unter [Konfigurieren eines Client Computers für die automatische Domänen Zeitsynchronisierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)beschrieben.


> [!IMPORTANT]  
> Vor Windows Server 2016 wurde der W32Time-Dienst nicht so konzipiert, dass er Zeit empfindliche Anwendungsanforderungen erfüllt.  Updates für Windows Server 2016 ermöglichen es Ihnen jetzt jedoch, eine Lösung für eine Genauigkeit von 1 MS in Ihrer Domäne zu implementieren.  Weitere Informationen zu finden Sie unter [Windows 2016 (genaue Zeit](accurate-time.md) -und [Support Grenze) zum Konfigurieren des Windows-Zeit Dienstanbieter für hochwertige Umgebungen](support-boundary.md) .

## <a name="related-topics"></a>Zugehörige Themen
- [Windows 2016, genaue Zeit](accurate-time.md)
- [Verbesserungen bei der Zeit Genauigkeit für Windows Server 2016](windows-server-2016-improvements.md)  
- [Funktionsweise des Windows-Zeit Dienstanbieter](How-the-Windows-Time-Service-Works.md)  
- [Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md)  
- [Unterstützungsgrenzen zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md)
- [Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)
