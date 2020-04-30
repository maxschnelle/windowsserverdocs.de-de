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
ms.openlocfilehash: bb68a3551b362f0beb5d42a92a7c18d0913e47bc
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624088"
---
# <a name="planning-domain-controller-placement"></a>Planen der Domänencontrollerkapazität

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie alle Netzwerkinformationen gesammelt haben, die zum Entwerfen der Standort Topologie verwendet werden, planen Sie, wo Sie Domänen Controller platzieren möchten, einschließlich der Gesamtstruktur-Stamm Domänen Controller, regionaler Domänen Controller, Betriebs Master-Rollen Inhaber und globaler Katalogserver.

In Windows Server 2008 können Sie auch schreibgeschützte Domänen Controller (Read-Only Domain Controllers, RODCs) nutzen. Ein RODC ist eine neue Art von Domänen Controller, der schreibgeschützte Partitionen der Active Directory Datenbank hostet. Mit Ausnahme von Konto Kennwörtern enthält ein RODC alle Active Directory Objekte und Attribute, die ein Beschreib barer Domänen Controller enthält. Es können jedoch keine Änderungen an der Datenbank vorgenommen werden, die auf dem RODC gespeichert ist. Änderungen müssen an einem beschreibbaren Domänen Controller vorgenommen und dann zurück auf den RODC repliziert werden.

Ein RODC wurde hauptsächlich für die Bereitstellung in Remote Umgebungen oder in Zweigstellen Umgebungen entwickelt, die in der Regel nur relativ wenige Benutzer, schlechte physische Sicherheit, eine relativ schlechte Netzwerkbandbreite für eine Hub-Site und Mitarbeiter mit eingeschränkten Kenntnissen der Informationstechnologie (IT) haben. Das Bereitstellen von RODCs führt zu einer verbesserten Sicherheit und einem effizienteren Zugriff auf Netzwerkressourcen. Weitere Informationen zu RODC-Funktionen finden [Sie unter AD DS: schreibgeschützte Domänen Controller](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732801(v=ws.10)). Informationen zum Bereitstellen eines RODC finden Sie unterschritt Weise Anleitung für die schreibgeschützten [Domänen Controller](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772234(v=ws.10)) .

> [!NOTE]
> In diesem Handbuch wird nicht erläutert, wie Sie die richtige Anzahl von Domänen Controllern und die Hardwareanforderungen des Domänen Controllers für jede Domäne ermitteln, die an jedem Standort repräsentiert wird.

## <a name="in-this-section"></a>In diesem Abschnitt

- [Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)

- [Planen der Platzierung regionaler Domänen Controller](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)

- [Planen der Platzierung des globalen Katalogservers](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)

- [Planen der Platzierung der Rolle „Betriebsmaster“](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)

