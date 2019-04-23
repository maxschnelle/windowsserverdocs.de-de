---
title: What's New for Managed Service Accounts
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f2a8b6b-c152-4c40-b712-bfabff0e408b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: cac55d04a40c84ce160eb3883d6095a7db0ef3be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872181"
---
# <a name="what39s-new-for-managed-service-accounts"></a>Was&#39;Neues in verwalteten Dienstkonten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema für IT-Experten beschreibt die Änderungen an der Funktionalität für Gruppenverwaltete Dienstkonten: Übersicht mit der Einführung der gruppenverwalteten Dienstkontos (gMSA) in Windows Server 2012 und Windows 8.

Das verwaltete Dienstkonto wurde entwickelt, damit Dienste und Aufgaben wie Windows-Dienste und ISS-Anwendungspools eigene Domänenkonten zur Verfügung stellen und dabei die Anforderung an Administratoren wegfällt, diesen Konten manuell Kennwörter zuweisen zu müssen. Die automatische Kennwortverwaltung wird von verwalteten Domänenkonten bereitgestellt.

## <a name="versions"></a>Neues bei verwalteten Dienstkonten in Windows Server 2012 und Windows 8
Im folgenden wird beschrieben, welche Änderungen an der Funktionalität funktionsänderungen in Windows Server 2012 und Windows 8 vorgenommen wurden.

### <a name="group-managed-service-accounts"></a>Gruppenverwaltete Dienstkonten
Wenn ein Domänenkonto für einen Server in einer Domäne konfiguriert wird, kann sich der Clientcomputer bei diesem Gerät authentifizieren und eine Verbindung dazu herstellen. Zuvor stellen nur zwei Kontotypen eine Identität zur Verfügung, ohne dass die Kennwortverwaltung erforderlich war. Diese Kontotypen haben jedoch Einschränkungen:

-   Das Computerkonto ist auf einen Domänenserver beschränkt und die Kennwörter werden vom Computer verwaltet.

-   Das verwaltete Dienstkonto ist auf einen Domänenserver beschränkt und die Kennwörter werden vom Computer verwaltet.

Diese Konten können nicht über mehrere Systeme hinweg freigegeben werden. Aus diesem Grund muss das Konto im Hinblick auf alle Dienste auf allen Systemen regelmäßig gewartet werden, um zu verhindern, dass das Kennwort unbeabsichtigterweise abläuft.

**Welchen Nutzen bietet diese Änderung?**

Das gruppenverwaltete Dienstkonto löst dieses Problem, da das Kennwort für das von Windows Server 2012-Domänencontrollern verwaltet wird und von mehreren Windows Server 2012--Systemen abgerufen werden kann. Das minimiert den administrativen Mehraufwand eines Dienstkontos, indem Windows gestattet wird, die Kennwortverwaltung für diese Konten zu übernehmen.

**Worin bestehen die Unterschiede?**

Auf Computern kann von einem Server unter Windows Server 2012 oder Windows 8, einer Gruppe MSA erstellt und über den Dienststeuerungs-Manager verwaltet werden, damit mehrere Instanzen des Diensts wird z. B. über eine Serverfarm bereitgestellt werden kann, verwaltet werden. Tools und Hilfsprogramme zur Verwaltung von verwalteten Dienstkonten, etwa der ISS-Anwendungspoolmanager, können mit gruppenverwalteten Dienstkonten verwendet werden. Domänenadministratoren können die Dienstverwaltung an Dienstadministratoren delegieren, die den gesamten Lebenszyklus eines verwalteten oder gruppenverwalteten Dienstkontos verwalten können. Bestehende Clientcomputer können sich bei allen solchen Diensten authentifizieren, ohne zu wissen, bei welcher Dienstinstanz sie das tun.

### <a name="interoperability"></a>Entfernten oder veralteten Funktionen
Für Windows Server 2012, die Windows PowerShell-Cmdlets standardmäßig für die Verwaltung der gruppenverwalteten Dienstkonten anstatt für die Server verwalteten Dienstkonten.

## <a name="see-also"></a>Siehe auch

-   [Gruppe verwaltete Dienstkonten: Übersicht](group-managed-service-accounts-overview.md)

-   [Übersicht über Active Directory-Domänendienste](active-directory-domain-services-overview.md)

-   [Verwaltete Dienstkonten: Grundlegendes, Implementierung, bewährte Methoden und Problembehandlung](http://blogs.technet.com/b/askds/archive/20../managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)


