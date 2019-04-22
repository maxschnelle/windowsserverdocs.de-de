---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Technische Referenz für Windows Time Service
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 0b424e118980792d4b4db8ba365ad60cc5edc75c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815941"
---
# <a name="windows-time-service"></a>Windows-Zeitdienst

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher


**In diesem Handbuch**  
  
* Wo Windows Time Service-Konfigurationsinformationen zu finden.  
* Was ist der Windows-Zeitdienst?  
* Wichtigkeit der Time-Protokolle  
* Funktionsweise des Windows-Zeitdiensts   
* Windows-Zeitdienst: Tools und Einstellungen  
  
> [!NOTE]  
> In Windows Server 2003 und Microsoft Windows 2000 Server heißt der Verzeichnisdienst Active Directory-Dienst. In Windows Server 2008 R2 und Windows Server 2008 heißt der Verzeichnisdienst Active Directory Domain Services (AD DS). Im weiteren Verlauf dieses Themas bezieht sich auf AD DS, aber die Informationen gelten jedoch auch für Active Directory Domain Services in Windows Server 2016.  
  
Der Windows-Zeitdienst, auch bekannt als W32Time, wird das Datum und die Uhrzeit für alle Computer einer AD DS-Domäne synchronisiert. Die uhrzeitsynchronisierung ist für die ordnungsgemäße Ausführung vieler Windows-Dienste und Line-of-Business-Anwendungen von entscheidender Bedeutung. Der Windows-Zeitdienst verwendet das Network Time Protocol (NTP), um Computertakt auf das Netzwerk zu synchronisieren, sodass eine genaue Uhrzeit oder Zeitstempel, um Netzwerk-Überprüfung und Resource Access-Anforderungen zugewiesen werden kann. Der Dienst integriert NTP und Zeitanbieter, eine zuverlässige und skalierbare Zeitdienst für Administratoren in Unternehmen erleichtert.
  
> [!IMPORTANT]  
> Vor Windows Server 2016 wurde der W32Time-Dienst nicht für zeitempfindliche Anwendung Bedürfnissen entwickelt.  Updates für Windows Server 2016 nun ermöglichen jedoch zum Implementieren einer Lösung für 1 ms Genauigkeit in Ihrer Domäne.  Finden Sie unter [Windows 2016 genau Zeit](accurate-time.md) und [Unterstützung Grenze so konfigurieren Sie den Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](support-boundary.md) für Weitere Informationen.  
  
## <a name="BKMK_Config"></a>Wo Windows Time Service-Konfigurationsinformationen zu finden.  
Dieses Handbuch ist **nicht** erläutert die Konfiguration des Windows-Zeitdienstes. Es gibt mehrere verschiedene Themen im Microsoft TechNet und in der Microsoft Knowledge Base, in denen Verfahren zum Konfigurieren des Windows-Zeitdienstes erläutert. Wenn Sie Informationen zur Konfiguration benötigen, sollten Sie finden die entsprechende Informationen von den folgenden Themen finden.  
  
-   Zum Konfigurieren des Windows-Zeitdienstes für die Gesamtstruktur Stamm Emulator primärer Domänencontroller (PDC) finden Sie unter:  
  
    -   [Konfigurieren des Windows-Zeitdienstes auf dem PDC-Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [Konfigurieren eine Zeitquelle für die Gesamtstruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft Knowledge Base-Artikel 816042, [Vorgehensweise: konfigurieren ein autorisierenden Zeitservers in Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402), beschreibt die Konfigurationseinstellungen für Computer unter Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 und Windows Server 2003 R2.  
  
-   Zum Konfigurieren des Windows-Zeitdienstes auf Member der Domänenclient oder Server oder sogar Domänencontroller, die nicht als der Gesamtstruktur-Stamm-PDC-Emulator konfiguriert sind, finden Sie unter [Konfigurieren eines Clientcomputers für die zeitsynchronisierung für die automatische Domäne](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
    > [!WARNING]  
    > Einige Anwendungen erfordern möglicherweise ihre Computer damit hohe Genauigkeit Laufzeitdienste. Wenn dies der Fall ist, können Sie eine manuelle Zeitquelle konfigurieren, aber beachten Sie, dass der Windows-Zeitdienst nicht entworfen wurde, als eine äußerst präzise Zeitquelle fungieren. Stellen Sie sicher, dass Sie über die für unterstützungseinschränkungen sind für hohe Genauigkeit Time-Umgebungen wie im Microsoft Knowledge Base beschriebene 939322, Artikel [Unterstützung Grenze so konfigurieren Sie den Windows-Zeitdienst für High-Genauigkeit Umgebungen](support-boundary.md).  
  
-   So konfigurieren Sie den Windows-Zeitdienst auf allen Windows-basierten Client oder Server-Computern, die konfiguriert werden, wie die Mitglieder der Arbeitsgruppe Mitglieder der Domäne finden Sie unter [konfigurieren Sie eine manuelle Zeitquelle für einen ausgewählten Clientcomputer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29).  
  
-   Zum Konfigurieren des Windows-Zeitdienstes auf einem Hostcomputer, der eine virtuelle Umgebung ausgeführt wird finden Sie im Microsoft Knowledge Base-Artikel 816042, [Vorgehensweise: konfigurieren ein autorisierenden Zeitservers in Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402). Wenn Sie mit einem nicht-Microsoft Virtualisierungsprodukt arbeiten, achten Sie darauf, dass Sie in der Dokumentation des Herstellers für dieses Produkt zu informieren.  
  
-   Um den Windows-Zeitdienst auf einem Domänencontroller zu konfigurieren, die auf einem virtuellen Computer ausgeführt wird, empfiehlt es sich, dass Sie teilweise Deaktivieren der zeitsynchronisierung zwischen dem Betriebssystem des Hosts und dem Gastbetriebssystem, die als Domänencontroller fungieren. Dies ermöglicht es dem Gast-Domänencontroller für die zeitsynchronisierung für die Domänenhierarchie, behalten jedoch müssen Sie einen Zeitversatz, wenn sie aus einem gespeicherten Zustand wiederhergestellt wurde. Weitere Informationen finden Sie im Microsoft Knowledge Base-Artikel 976924, [erhalten Sie die Windows-Zeitdienst Ereignis-IDs 24 29 und 38 auf einem virtualisierten Domänencontroller, die auf einem Windows Server 2008-basierten Host-Server mit Hyper-V ausgeführt wird](https://go.microsoft.com/fwlink/?LinkID=192236) und [Bereitstellungsüberlegungen für virtualisierte Domänencontroller](https://go.microsoft.com/fwlink/?LinkID=192235).  
  
-   Zum Konfigurieren des Windows-Zeitdienstes auf einem Domänencontroller fungiert, als des Gesamtstruktur-Stamm-PDC-Emulators, die auch in einem virtuellen Computer ausgeführt wird, führen Sie die gleichen Anweisungen für einen physischen Computer beschriebenen [konfigurieren Sie auf den Windows-Zeitdienst der PDC-Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29).  
  
-   Verwenden Sie zum Konfigurieren des Windows-Zeitdienstes auf einem Mitgliedsserver ausgeführt als virtueller Computer die Domäne-Time-Hierarchie, wie in beschrieben ([Konfigurieren eines Clientcomputers für die zeitsynchronisierung für die automatische Domäne](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
## <a name="BKMK_WTS"></a>Was ist der Windows-Zeitdienst?  
Der Windows-Zeitdienst (W32Time) stellt die Synchronisation des Computertakts Netzwerk für Computer ohne umfassende Konfiguration bereit.  
  
Der Windows-Zeitdienst ist wichtig, um die erfolgreiche Ausführung der Kerberos V5-Authentifizierung und somit auf AD DS-basierte Authentifizierung. Kerberos-fähige Anwendung, die meisten Sicherheitsdienste, einschließlich basiert auf der zeitsynchronisierung zwischen den Computern, die in der Authentifizierungsanforderung beteiligt sind. AD DS-Domänencontrollern müssen auch Uhren, um damit genau die Datenreplikation sorgen Sie dafür synchronisiert haben.  
  
Der Windows-Zeitdienst wird in einer dynamic Link Library namens W32Time.dll implementiert. W32Time.dll wird standardmäßig installiert, in der **%Systemroot%\System32** Ordner während der Installation des Betriebssystems und Installation.  
  
W32Time.dll wurde ursprünglich für Windows 2000 Server, um eine Spezifikation unterstützen das Kerberos V5-Authentifizierungsprotokoll entwickelt, die Uhren in einem Netzwerk zu synchronisierenden erforderlich. Ab Windows Server 2003, W32Time.dll bereitgestellten erhöhte Genauigkeit der Synchronisation des Computertakts Netzwerk über das Betriebssystem Windows 2000 Server und darüber hinaus unterstützt eine Vielzahl von Hardwaregeräten und der Uhrzeit von Netzwerkprotokollen über Zeit Anbieter. Obwohl der ursprünglich entworfen, um die Synchronisation des Computertakts für Kerberos-Authentifizierung bereitzustellen, viele aktuelle Anwendungen Zeitstempel verwenden, um sicherzustellen, dass die Transaktionskonsistenz, zum Zeitpunkt der wichtige Ereignisse und andere unternehmenskritische, aufzeichnen zeitempfindliches Informationen. Diese Anwendungen profitieren von der zeitsynchronisierung zwischen Computern, die von der Windows-Zeitdienst bereitgestellt wird.  
  
## <a name="BKMK_TimeProtocols"></a>Wichtigkeit der Time-Protokolle  
Zeit Protokolle kommunizieren zwischen zwei Computern zum Austauschen von Informationen aus, und klicken Sie dann anhand dieser Informationen ihre Uhren synchronisieren. Mit dem Windows Time Service Time-Protokoll ein Client fordert Informationen von einem Server und synchronisiert die Uhr basierend auf den Informationen, der empfangen werden.  
  
Der Windows-Zeitdienst verwendet NTP um zeitsynchronisierung in einem Netzwerk. NTP ist ein Internetprotokoll für die Zeit, die die Disziplin Algorithmen erforderlich für die Synchronisierung von Uhren enthält. NTP ist eine genauere Time-Protokoll als SNTP Simple Network Time Protocol (), die in einigen Versionen von Windows verwendet wird. allerdings weiterhin W32Time SNTP zum Aktivieren der Abwärtskompatibilität mit der Zeit SNTP-basierte Dienste, z. B. Windows 2000-Computern unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
[Wie funktioniert die Windows-Zeitdienst](How-the-Windows-Time-Service-Works.md)  
[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)