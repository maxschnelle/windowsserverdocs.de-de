---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: Planen der Domänencontrollerkapazität
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 68406d4973dd585bf0a98562c987c1b1512c095c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883361"
---
# <a name="planning-domain-controller-placement"></a>Planen der Domänencontrollerkapazität

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie die Netzwerk-Informationen gesammelt haben, die zum Entwerfen der Standorttopologie verwendet werden, Planen Sie Domänencontroller, einschließlich Domänencontrollern im Gesamtstrukturstamm, der regionalen Domänencontroller, der Betriebsmasterrolle, einfügen möchten, und globale Katalogserver.  
  
In Windows Server 2008 können Sie auch von schreibgeschützten Domänencontrollern (RODCs) nutzen. Einen RODC handelt es sich um eine neue Art von Domänencontroller, die schreibgeschützten Partitionen der Active Directory-Datenbank hostet. Mit Ausnahme von Kontokennwörtern sind ein RODC enthalten alle Active Directory-Objekte und Attribute, die ein beschreibbarer Domänencontroller verfügt. Änderungen können nicht jedoch in der Datenbank vorgenommen werden, die auf dem RODC gespeichert ist. Änderungen müssen auf einen beschreibbaren Domänencontroller vorgenommen und dann zurück auf den RODC repliziert werden.  
  
Ein RODC dient in erster Linie für die Bereitstellung in Remotebüros oder zweigstellenumgebungen, die in der Regel relativ wenige Benutzer, die eine schlechte physische Sicherheit, die relativ schwache Netzwerkbandbreite zu einem Hubstandort vorhanden sind, und der Mitarbeiter mit eingeschränkten Kenntnissen von Informationen Informationstechnologie (IT). Bereitstellen von RODCs führt verbesserte Sicherheit und effizienter Zugriff auf Netzwerkressourcen. Weitere Informationen zu RODC-Funktionen finden Sie in AD DS: Read-Only Domain Controller ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616)). Informationen zum Bereitstellen eines RODC, finden Sie unter der schrittweisen Anleitung für Read-Only-Domänencontroller ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728)).  
  
> [!NOTE]  
> Dieses Handbuch wird nicht erläutert, wie Sie ermitteln, die richtige Anzahl von Domänencontrollern und der Hardware domänencontrolleranforderungen für jede Domäne, die an jedem Standort dargestellt wird.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [Planen der Platzierung der regionalen Domänencontroller](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [Planen der Platzierung des globalen Katalogservers](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [Planen der Platzierung der Vorgänge](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


