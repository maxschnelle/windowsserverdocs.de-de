---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: Festlegen der AD FS-Bereitstellungstopologie
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: dfb863cf85f9e9bffadbe10ca017491341596dad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972117"
---
# <a name="determine-your-ad-fs-deployment-topology"></a>Festlegen der AD FS-Bereitstellungstopologie

Der erste Schritt bei der Planung einer Bereitstellung von Active Directory-Verbunddienste (AD FS) \( AD FS \) ist die Ermittlung der richtigen Bereitstellungs Topologie, um die SSO-Anforderungen für einmaliges Anmelden in \- \( \) Ihrer Organisation zu erfüllen. In den Themen in diesem Abschnitt werden die verschiedenen Bereitstellungstopologien beschrieben, die Sie mit AD FS verwenden können. Zudem werden die mit jeder Bereistellungstopologie verbundenen Vorteile und Einschränkungen beschrieben, damit Sie die am besten geeignete Topologie für Ihre speziellen geschäftlichen Anforderungen auswählen können.

Bevor Sie dieses Thema zur Bereitstellungstopologie lesen, sollten Sie zunächst die in der folgenden Tabelle aufgeführt Aufgaben in der angegebenen Reihenfolge durchführen.

|Empfohlene Aufgabe|BESCHREIBUNG|Verweis|
|--------------------|---------------|-------------|
|Überprüfen Sie, wie AD FS Daten auf anderen Verbund Servern in einer Verbund Serverfarm gespeichert und repliziert werden.|Informieren Sie sich über den Zweck und die Replikationsmethoden, die für die zugrundeliegenden Daten verwendet werden können, die in der AD FS-Konfigurationsdatenbank gespeichert sind. In diesem Thema werden die Konzepte der Konfigurations Datenbank vorgestellt und die beiden Datenbanktypen beschrieben: interne Windows-Datenbank \( \) -wid und Microsoft SQL Server.|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|
|Wählen Sie den AD FS-Konfigurationsdatenbanktyp aus, den Sie in Ihrer Organisation bereitstellen werden.|Betrachten Sie die verschiedenen Vorteile und Einschränkungen bei der Verwendung von WID oder SQL Server als AD FS-Konfigurationsdatenbank und die verschiedenen Anwendungsszenarien, die sie unterstützen.|[Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md)|

> [!NOTE]
> Zum Implementieren von grundlegender Redundanz, Lastenausgleich und der Option zum Skalieren des Verbunddienst bei \( Bedarf wird \) empfohlen, dass Sie mindestens zwei Verbund Server pro Verbund Serverfarm für alle Produktionsumgebungen bereitstellen, unabhängig davon, welcher Datenbanktyp verwendet werden soll.

Wenn Sie die Inhalte der vorstehenden Tabelle durchgesehen haben, fahren Sie mit den folgenden Themen in diesem Abschnitt fort:

-   [Eigenständiger Verbundserver mit WID](Stand-Alone-Federation-Server-Using-WID.md)

-   [Verbundserverfarm mit WID](Federation-Server-Farm-Using-WID-2012.md)

-   [Verbundserverfarm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)

-   [Verbundserverfarm mit SQL Server](Federation-Server-Farm-Using-SQL-Server-2012.md)

Nachdem Sie die Auswahl Ihrer AD FS Bereitstellungs Topologie abgeschlossen haben, sollten Sie das Thema [Planen der AD FS Server Kapazität](Planning-for-AD-FS-Server-Capacity.md) lesen, um die empfohlene Anzahl von Servern zu ermitteln, die Sie zur Unterstützung dieser Topologie bereitstellen müssen.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

