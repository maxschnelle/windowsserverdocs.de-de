---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Technische Referenz zum Windows-Zeitdienst
description: Der W32Time-Dienst bietet Uhrsynchronisierung im Netzwerk für Computer, ohne dass eine größere Konfiguration erforderlich ist. Der W32Time-Dienst ist für den erfolgreichen Betrieb der Kerberos V5-Authentifizierung und somit für die AD DS basierte Authentifizierung von wesentlicher Bedeutung.
author: dcuomo
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: ec141fe8a5e2b1acf0a9f6627dd2d394382424bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859823"
---
# <a name="windows-time-service-technical-reference"></a>Technische Referenz zum Windows-Zeitdienst
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Der W32Time-Dienst bietet Uhrsynchronisierung im Netzwerk für Computer, ohne dass eine größere Konfiguration erforderlich ist. Der W32Time-Dienst ist für den erfolgreichen Betrieb der Kerberos V5-Authentifizierung und somit für die AD DS basierte Authentifizierung von wesentlicher Bedeutung. Jede Kerberos-fähige Anwendung, einschließlich der meisten Sicherheitsdienste, basiert auf der Zeitsynchronisierung zwischen den Computern, die an der Authentifizierungsanforderung teilnehmen. AD DS-Domänencontroller müssen auch synchronisierte Uhren besitzen, um die exakte Datenreplikation zu gewährleisten.

> [!NOTE]  
> In Windows Server 2003 und Microsoft Windows 2000 Server heißt der Verzeichnisdienst Active Directory-Verzeichnisdienst. In Windows Server 2008 R2 und Windows Server 2008 heißt der Verzeichnisdienst Active Directory Domain Services (AD DS). Im weiteren Verlauf dieses Themas wird Bezug auf AD DS genommen, aber die Informationen gelten auch für Active Directory Domain Services in Windows Server 2016.

Der W32Time-Zeitdienst ist in einer DLL (Dynamic Link Library) namens „W32Time.dll“ implementiert, die standardmäßig in **%Systemroot%\System32** installiert wird. „W32Time.dll“ wurde ursprünglich für Windows 2000 Server entwickelt, um eine Spezifikation des Kerberos V5-Authentifizierungsprotokolls zu unterstützen, die erfordert, dass Uhren in einem Netzwerk synchronisiert sind. Seit Windows Server 2003 stellt „W32Time.dll“ eine höhere Genauigkeit bei der Netzwerkuhrsynchronisierung über das Betriebssystem Windows Server 2000 bereit. Darüber hinaus unterstützte „W32Time.dll“ in Windows Server 2003 eine Vielzahl von Hardwaregeräten und Netzwerkzeitprotokollen mithilfe von Zeitanbietern.

Obwohl es ursprünglich konzipiert wurde, um Uhrsynchronisierung für die Kerberos-Authentifizierung bereitzustellen, verwenden viele aktuelle Anwendungen Zeitstempel, um die Transaktionskonsistenz sicherzustellen, um die Zeit wichtiger Ereignisse sowie anderer geschäftskritischer, zeitabhängiger Informationen aufzuzeichnen.  Diese Anwendungen profitieren von der Zeitsynchronisierung zwischen Computern, die vom Windows-Zeitdienst bereitgestellt wird.

## <a name="importance-of-time-protocols"></a>Wichtigkeit von Zeitprotokollen
Zeitprotokolle kommunizieren zwischen zwei Computern, um Zeitinformationen auszutauschen, und verwenden diese Informationen dann, um ihre Uhren zu synchronisieren. Mit dem Zeitprotokoll des Windows-Zeitdiensts fordert ein Client Zeitinformationen von einem Server an und synchronisiert seine Uhr basierend auf den empfangenen Informationen.
  
Der Windows-Zeitdienst verwendet NTP, um die Synchronisierung der Zeit über ein Netzwerk zu unterstützen. NTP ist ein Internetzeitprotokoll, das die für die Synchronisierung von Uhren erforderlichen Disziplinalgorithmen umfasst. NTP ist ein genaueres Zeitprotokoll als das Simple Network Time Protocol (SNTP), das in einigen Versionen von Windows verwendet wird. W32Time unterstützt jedoch weiterhin SNTP, um Abwärtskompatibilität mit Computern zu ermöglichen, auf denen SNTP-basierte Zeitdienste, wie beispielsweise Windows 2000, ausgeführt werden.
## <a name="where-to-find-windows-time-service-configuration-related-information"></a>Wo finde ich konfigurationsbezogene Informationen zum Windows-Zeitdienst?  
In diesem Leitfaden wird **nicht** erläutert, wie der Windows-Zeitdienst konfiguriert wird. In Microsoft TechNet und in der Microsoft Knowledge Base findest du zahlreiche Themen, in denen erläutert wird, wie der Windows-Zeitdienst konfiguriert wird. Wenn du Konfigurationsinformationen benötigst, sollten dir die folgenden Themen beim Auffinden der entsprechenden Informationen helfen.  
-   Informationen zum Konfigurieren des Windows-Zeitdiensts für den PDC-Emulator in der Stammdomäne der Gesamtstruktur findest du hier:
  
    -   [Konfigurieren des Windows-Zeitdiensts im PDC-Emulator in der Stammdomäne der Gesamtstruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [Konfigurieren des Zeitdiensts für die Gesamtstruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft Knowledge Base-Artikel 816042, [Konfigurieren eines autoritativen Zeitservers in Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402), in dem die Konfigurationseinstellungen für Computer mit Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 und Windows Server 2003 R2 beschrieben werden.  
  
-   Informationen zum Konfigurieren des Windows-Zeitdiensts auf einem beliebigen Domänenmitgliedsclient oder -server oder sogar auf Domänencontrollern, die nicht als PDC-Emulator des Gesamtstrukturstamms konfiguriert sind, findest du unter [Konfigurieren eines Clientcomputers für die automatische Domänenzeitsynchronisierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
    > [!WARNING]  
    > Für einige Anwendungen ist es möglicherweise erforderlich, dass ihre Computer über hochgenaue Zeitdienste verfügen. Wenn dies der Fall ist, kannst du eine manuelle Zeitquelle konfigurieren, doch beachte dabei, dass der Windows-Zeitdienst nicht konzipiert wurde, um als hochgenaue Zeitquelle zu fungieren. Stelle sicher, dass du die Einschränkungen der Unterstützung für Umgebungen mit hochgenauer Zeit kennst, wie im Microsoft Knowledge Base-Artikel 939322, [Support-Grenze zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md), beschrieben.  
  
-   Informationen zum Konfigurieren des Windows-Zeitdiensts auf einem Windows-basierten Client- oder Servercomputer, der nicht als Domänenmitglied, sondern als Arbeitsgruppenmitglied konfiguriert ist, findest du unter [Konfigurieren einer manuellen Zeitquelle für einen ausgewählten Clientcomputer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29).  
  
-   Informationen zum Konfigurieren des Windows-Zeitdiensts auf einem Hostcomputer, auf dem eine virtuelle Umgebung ausgeführt wird, findest du im Microsoft Knowledge Base-Artikel 816042 [Konfigurieren eines autoritativen Zeitservers in Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402). Wenn du mit einem Virtualisierungsprodukt arbeitest, das nicht von Microsoft stammt, lies die Herstellerdokumentation für dieses Produkt.  
  
-   Um den Windows-Zeitdienst auf einem Domänencontroller zu konfigurieren, der in einem virtuellen Computer ausgeführt wird, empfiehlt es sich, die Zeitsynchronisierung zwischen dem Hostsystem und dem Gastbetriebssystem, das als Domänencontroller dient, teilweise zu deaktivieren. Auf diese Weise vermeidest du eine Zeitabweichung, wenn der Gastdomänencontroller aus einem Zustand „Gespeichert“ wiederhergestellt wird, behältst jedoch die Zeitsynchronisierung für die Domänenhierarchie bei. Weitere Informationen findest du im Microsoft Knowledge Base-Artikel 976924, [Du erhältst die Windows-Zeitdienstereignis-IDs 24, 29 und 38 auf einem virtualisierten Domänencontroller, der auf einem Windows Server 2008-basierten Hostserver mit Hyper-V ausgeführt wird](https://go.microsoft.com/fwlink/?LinkID=192236), und [Überlegungen zur Bereitstellung virtualisierter Domänencontroller](https://go.microsoft.com/fwlink/?LinkID=192235).  
  
-   Um den Windows-Zeitdienst auf einem Domänencontroller zu konfigurieren, der als PDC-Emulator des Gesamtstrukturstamms fungiert, der ebenfalls auf einem virtuellen Computer ausgeführt wird, befolge dieselben Anweisungen wie für einen physischen Computer, wie in [Konfigurieren des Windows-Zeitdiensts im PDC-Emulator in der Stammdomäne der Gesamtstruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) beschrieben.  
  
-   Um den Windows-Zeitdienst auf einem Mitgliedsserver zu konfigurieren, der als virtueller Computer ausgeführt wird, verwende die Domänenzeithierarchie, wie unter [Konfigurieren eines Clientcomputers für die automatische Domänenzeitsynchronisierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29) beschrieben.


> [!IMPORTANT]  
> Vor Windows Server 2016 war der W32Time-Dienst nicht so konzipiert, dass er die Anforderungen zeitabhängiger Anwendungen erfüllte.  Updates für Windows Server 2016 ermöglichen es jetzt jedoch, eine Lösung für eine Genauigkeit von 1 ms in deiner Domäne zu implementieren.  Weitere Informationen findest du unter [Windows 2016: Genaue Zeit](accurate-time.md) und [Supportgrenze zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md).

## <a name="related-topics"></a>Zugehörige Themen
- [Windows 2016 – Genaue Uhrzeit](accurate-time.md)
- [Verbesserungen bei der Zeitgenauigkeit für Windows Server 2016](windows-server-2016-improvements.md)  
- [Funktionsweise des Windows-Zeitdiensts](How-the-Windows-Time-Service-Works.md)  
- [Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md)  
- [Supportgrenze zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md)
- [Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)
