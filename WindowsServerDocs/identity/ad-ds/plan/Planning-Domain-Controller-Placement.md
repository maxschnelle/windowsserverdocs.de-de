---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: "Planen der Domänencontrollerkapazität"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c6d9ca064699f95390e5b95863a6871ea2dc9d6e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="planning-domain-controller-placement"></a>Planen der Domänencontrollerkapazität

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie die Netzwerk-Informationen gesammelt haben, die zum Entwerfen der Standorttopologie, Planen Sie die Domänencontroller, einschließlich Domänencontrollern im Gesamtstrukturstamm, regionalen Domänencontroller platziert werden soll verwendet werden master Operations Rolleninhaber und globalen Katalogservern.  
  
In Windows Server2008 können Sie auch von schreibgeschützten Domänencontrollern (RODCs) nutzen. Ein RODC ist eine neue Art von Domänencontroller, die nur-Lese-Partitionen der Active Directory-Datenbank hostet. Mit Ausnahme von Kontokennwörtern enthält ein RODC alle Active Directory-Objekte und Attribute, die ein beschreibbaren Domänencontroller enthält. Allerdings kann nicht in die Datenbank geändert werden, die auf dem RODC gespeichert ist. Änderungen müssen auf einem beschreibbaren Domänencontroller vorgenommen und dann wieder auf den RODC repliziert werden.  
  
Ein RODC soll in erster Linie in Remotebüros bereitgestellt werden oder Zweigniederlassungen, die in der Regel relativ wenige Benutzer, eine schlechte physische Sicherheit, relativ schlechte Netzwerkbandbreite an einem Hubstandort und Mitarbeiter mit eingeschränkte Kenntnisse der Informationstechnologie (IT). Bereitstellen von RODCs Ergebnisse in verbesserte Sicherheit und effizienter Zugriff auf Netzwerkressourcen. Weitere Informationen zu RODC-Features finden Sie unter AD DS: Read-Only Domänencontroller ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616)). Weitere Informationen zum Bereitstellen eines RODC finden Sie unter der Step-by-Step Handbuch für Read-Only Domänencontroller ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728)).  
  
> [!NOTE]  
> Dieses Handbuch wird nicht erläutert, wie Sie ermitteln, die richtige Anzahl von Domänencontrollern und die Hardware Anforderungen an den Domänencontroller für jede Domäne, die an jedem Standort dargestellt wird.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [Planen der Platzierung der regionalen Domänencontroller](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [Planen der Platzierung des globalen Katalogs](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [Planen der Platzierung der Rolle "Betriebsmaster"](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


