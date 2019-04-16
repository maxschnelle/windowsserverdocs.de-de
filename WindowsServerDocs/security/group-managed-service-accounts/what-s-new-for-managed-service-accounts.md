---
title: "Neues für verwaltete Dienstkonten"
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
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="what39s-new-for-managed-service-accounts"></a>Was & #39; s für verwaltete Dienstkonten

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten werden die Änderungen an der Funktionalität für verwaltete Dienstkonten mit der Einführung des Gruppenverwalteten Dienstkontos (gMSA) in Windows Server 2012 und Windows 8 beschrieben.

Das verwaltete Dienstkonto dient zum Bereitstellen der Dienste und Aufgaben wie das Windows-Dienste und IIS-Anwendungspools für die eigenen Domänenkonten zu teilen, während ein Administrator Kennwörter für diese Konten manuell verwaltet überflüssig. Es ist von verwalteten Domänenkonten, die automatische kennwortverwaltung bereitstellt.

## <a name="versions"></a>Neues für verwaltete Dienstkonten in Windows Server 2012 und Windows 8
Im folgenden wird beschrieben, welche Änderungen an der Funktionalität auf Microsoft-Konto in Windows Server 2012 und Windows 8 vorgenommen wurden.

### <a name="group-managed-service-accounts"></a>Gruppenverwaltete Dienstkonten
Wenn ein Domänenkonto für einen Server in einer Domäne konfiguriert ist, kann der Clientcomputer authentifizieren und eine Verbindung dazu herstellen. Zuvor wurden nur zwei Kontotypen Identität ohne Verwaltung bereitgestellt. Aber diese Kontotypen haben Einschränkungen:

-   Computerkonto ist auf einen Domänenserver beschränkt und die Kennwörter werden vom Computer verwaltet.

-   Das verwaltete Dienstkonto ist auf einen Domänenserver beschränkt und die Kennwörter werden vom Computer verwaltet.

Diese Konten können nicht über mehrere Systeme hinweg freigegeben werden. Aus diesem Grund müssen Sie das Konto für jeden Dienst auf jedem System, um zu verhindern, dass unerwünschte Kennwortablauf regelmäßig warten.

**Hinzufügen der Wert diese Änderung?**

Die Group-Managed Service Account löst dieses Problem, da das Kontokennwort von Windows Server 2012-Domänencontroller verwaltet wird und durch mehrere Windows Server 2012-Systeme abgerufen werden kann. Das minimiert den administrativen Mehraufwand eines Dienstkontos, indem Windows gestattet wird, die kennwortverwaltung für diese Konten zu behandeln.

**Worin bestehen die Unterschiede?**

Auf Computern kann von einem Server unter Windows Server 2012 oder Windows 8, eine Gruppe, die Microsoft-Konto erstellt und über den Dienst-Manager verwaltet, sodass mehrere Instanzen des Diensts, z. B. bereitgestellt, über eine Serverfarm verwaltet werden. Tools und Hilfsprogrammen, die Sie zur Verwaltung von verwalteten Dienstkonten, z. B. IIS Application Pool Manager können mit Gruppenverwalteten Dienstkonten verwendet werden. Domänenadministratoren können die dienstverwaltung an Dienstadministratoren delegieren, die den gesamten Lebenszyklus eines verwalteten Dienstkontos oder Gruppenverwalteten Dienstkontos verwalten können. Vorhandene Computer werden zu allen solchen Diensten authentifizieren, ohne zu wissen, welcher Dienstinstanz sie das tun.

### <a name="interoperability"></a>Entfernte oder veraltete Funktionen
Für Windows Server 2012, die Windows PowerShell-Cmdlets standardmäßig für die Verwaltung der Gruppenverwalteten Dienstkonten anstatt die serververwalteten Dienstkonten.

## <a name="see-also"></a>Siehe auch

-   [Gruppe verwaltete Dienstkonten: Übersicht](group-managed-service-accounts-overview.md)

-   [Übersicht über Active Directory-Domänendienste](active-directory-domain-services-overview.md)

-   [Verwaltete Dienstkonten: Grundlegendes, Implementierung, bewährte Methoden und Problembehandlung](http://blogs.technet.com/b/askds/archive/20../managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)


