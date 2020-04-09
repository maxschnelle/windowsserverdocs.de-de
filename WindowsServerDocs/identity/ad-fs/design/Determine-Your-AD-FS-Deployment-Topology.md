---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: Identifizieren der AD FS-Bereitstellungstopologie
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0336c54357745217c30e14afc0824f97d476b45d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855153"
---
# <a name="determine-your-ad-fs-deployment-topology"></a>Identifizieren der AD FS-Bereitstellungstopologie

Der erste Schritt bei der Planung einer Bereitstellung von Active Directory-Verbunddienste (AD FS) \(AD FS\) besteht darin, die geeignete Bereitstellungs Topologie zu ermitteln, um das einmalige Anmelden\-für \(SSO-\) Anforderungen Ihrer Organisation zu erfüllen. In den Themen in diesem Abschnitt werden die verschiedenen Bereitstellungstopologien beschrieben, die Sie mit AD FS verwenden können. Zudem werden die mit jeder Bereistellungstopologie verbundenen Vorteile und Einschränkungen beschrieben, damit Sie die am besten geeignete Topologie für Ihre speziellen geschäftlichen Anforderungen auswählen können.  
  
Bevor Sie dieses Thema zur Bereitstellungstopologie lesen, sollten Sie zunächst die in der folgenden Tabelle aufgeführt Aufgaben in der angegebenen Reihenfolge durchführen.  
  
|Empfohlene Aufgabe|Beschreibung|Verweis|  
|--------------------|---------------|-------------|  
|Überprüfen Sie, wie AD FS Daten auf anderen Verbund Servern in einer Verbund Serverfarm gespeichert und repliziert werden.|Informieren Sie sich über den Zweck und die Replikationsmethoden, die für die zugrundeliegenden Daten verwendet werden können, die in der AD FS-Konfigurationsdatenbank gespeichert sind. In diesem Thema werden die Konzepte der Konfigurations Datenbank vorgestellt und die beiden Datenbanktypen beschrieben: interne Windows-Datenbank-\(wid\) und Microsoft SQL Server.|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|Wählen Sie den AD FS-Konfigurationsdatenbanktyp aus, den Sie in Ihrer Organisation bereitstellen werden.|Betrachten Sie die verschiedenen Vorteile und Einschränkungen bei der Verwendung von WID oder SQL Server als AD FS-Konfigurationsdatenbank und die verschiedenen Anwendungsszenarien, die sie unterstützen.|[Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md)|  
  
> [!NOTE]  
> Zum Implementieren von grundlegender Redundanz, Lastenausgleich und der Option zum Skalieren der Verbunddienst \(falls erforderlich\)sollten Sie mindestens zwei Verbund Server pro Verbund Serverfarm für alle Produktionsumgebungen bereitstellen, unabhängig davon, welcher Datenbanktyp verwendet werden soll.  
  
Wenn Sie die Inhalte der vorstehenden Tabelle durchgesehen haben, fahren Sie mit den folgenden Themen in diesem Abschnitt fort:  
  
-   [Eigenständiger Verbundserver mit WID](Stand-Alone-Federation-Server-Using-WID.md)  
  
-   [Verbundserverfarm mit WID](Federation-Server-Farm-Using-WID-2012.md)  
  
-   [Verbundserverfarm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)  
  
-   [Verbundserverfarm mit SQL Server](Federation-Server-Farm-Using-SQL-Server-2012.md)  
  
Nachdem Sie die Auswahl Ihrer AD FS Bereitstellungs Topologie abgeschlossen haben, sollten Sie das Thema [Planen der AD FS Server Kapazität](Planning-for-AD-FS-Server-Capacity.md) lesen, um die empfohlene Anzahl von Servern zu ermitteln, die Sie zur Unterstützung dieser Topologie bereitstellen müssen.  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

