---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: Planen der Domänencontrollerkapazität
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 784e26a1762e8950b8f658ea32968a0d170df13d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822183"
---
# <a name="planning-domain-controller-placement"></a>Planen der Domänencontrollerkapazität

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie alle Netzwerkinformationen gesammelt haben, die zum Entwerfen der Standort Topologie verwendet werden, planen Sie, wo Sie Domänen Controller platzieren möchten, einschließlich der Gesamtstruktur-Stamm Domänen Controller, regionaler Domänen Controller, Betriebs Master-Rollen Inhaber und globaler Katalogserver.  
  
In Windows Server 2008 können Sie auch schreibgeschützte Domänen Controller (Read-Only Domain Controllers, RODCs) nutzen. Ein RODC ist eine neue Art von Domänen Controller, der schreibgeschützte Partitionen der Active Directory Datenbank hostet. Mit Ausnahme von Konto Kennwörtern enthält ein RODC alle Active Directory Objekte und Attribute, die ein Beschreib barer Domänen Controller enthält. Es können jedoch keine Änderungen an der Datenbank vorgenommen werden, die auf dem RODC gespeichert ist. Änderungen müssen an einem beschreibbaren Domänen Controller vorgenommen und dann zurück auf den RODC repliziert werden.  
  
Ein RODC wurde hauptsächlich für die Bereitstellung in Remote Umgebungen oder in Zweigstellen Umgebungen entwickelt, die in der Regel nur relativ wenige Benutzer, schlechte physische Sicherheit, eine relativ schlechte Netzwerkbandbreite für eine Hub-Site und Mitarbeiter mit eingeschränkten Kenntnissen der Informationstechnologie (IT) haben. Das Bereitstellen von RODCs führt zu einer verbesserten Sicherheit und einem effizienteren Zugriff auf Netzwerkressourcen. Weitere Informationen zu RODC-Funktionen finden Sie unter AD DS: schreibgeschützte Domänen Controller ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616)). Informationen zum Bereitstellen eines RODC finden Sie in der Schritt-für-Schritt-Anleitung für schreibgeschützte Domänen Controller ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728)).  
  
> [!NOTE]  
> In diesem Handbuch wird nicht erläutert, wie Sie die richtige Anzahl von Domänen Controllern und die Hardwareanforderungen des Domänen Controllers für jede Domäne ermitteln, die an jedem Standort repräsentiert wird.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [Planen der Platzierung regionaler Domänen Controller](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [Planen der Platzierung des globalen Katalogservers](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [Planen der Platzierung der Rolle „Betriebsmaster“](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


