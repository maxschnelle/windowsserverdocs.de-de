---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: Bestimmen der AD FS-Bereitstellungstopologie
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3300c16be6d516d7ec0bf4d0c3a025e59e6126b6
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="determine-your-ad-fs-deployment-topology"></a>Bestimmen der AD FS-Bereitstellungstopologie

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Der erste Schrittbei der Planung einer Bereitstellung von Active Directory Federation Services \(AD FS\) wird benötigt, um die geeignete Bereitstellungstopologie zum Erfüllen der einzelnen Standardparameter auf \(SSO\) Ihrer Organisation. Die Themen in diesem Abschnittbeschreiben die verschiedenen Bereitstellungstopologien, die Sie mit AD FS verwenden können. Außerdem werden die vor- und Nachteile, die mit jeder bereistellungstopologie verknüpft ist, sodass Sie die am besten geeignete Topologie für Ihre speziellen geschäftlichen Anforderungen auswählen können beschrieben.  
  
Bevor Sie dieses Thema zur Bereitstellungstopologie lesen, sollten Sie zunächst die in der Reihenfolge, in der folgenden Tabelle aufgeführten Aufgaben.  
  
|Empfohlene Aufgabe|Beschreibung|Referenz zu|  
|--------------------|---------------|-------------|  
|Überprüfen Sie, wie AD FS-Daten gespeichert und an andere Verbundserver in einer Verbundserverfarm repliziert.|Verstehen der Zweck und die Replikationsmethoden, die für die zugrunde liegenden Daten verwendet werden können, die in der AD FS-Konfigurationsdatenbank gespeichert ist. In diesem Thema werden Konzepte der Konfigurationsdatenbank eingeführt und die zwei Datenbanktypen beschrieben: Windows Internal Database \(WID\) und Microsoft SQL Server.|[Die Rolle des AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|Wählen Sie den Typ der AD FS-Konfigurationsdatenbank, die Sie in Ihrer Organisation bereitstellen.|Überprüfen Sie die verschiedenen Vorteile und Einschränkungen bei der Verwendung von WID oder SQL Server als der AD FS-Konfigurationsdatenbank und die verschiedenen Anwendungsszenarien, die sie unterstützen.|[Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md)|  
  
> [!NOTE]  
> Um grundlegende Redundanz, Lastenausgleich und die Möglichkeit, den Verbunddienst \(if required\) skalieren zu implementieren, empfehlen wir, dass Sie über mindestens zwei Verbundserver pro Verbundserverfarm für alle Produktionsumgebungen, unabhängig von der Art der Datenbank bereitstellen, die Sie verwenden möchten.  
  
Wenn Sie die Inhalte in der vorherigen Tabelle durchgesehen haben, fahren Sie mit den folgenden Themen in diesem Abschnittfort:  
  
-   [Eigenständiger Verbundserver mit WID](Stand-Alone-Federation-Server-Using-WID.md)  
  
-   [Verbundserverfarm mit WID](Federation-Server-Farm-Using-WID-2012.md)  
  
-   [Verbundserverfarm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)  
  
-   [Verbundserverfarm mit SQLServer](Federation-Server-Farm-Using-SQL-Server-2012.md)  
  
Die AD FS-Bereitstellungstopologie ausgewählt haben, wird empfohlen, dass Sie das Thema zu lesen [Planen der AD FS-Serverkapazität](Planning-for-AD-FS-Server-Capacity.md) die empfohlene Anzahl von Servern zu ermitteln, die Sie zur Unterstützung dieser Topologie bereitstellen müssen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

