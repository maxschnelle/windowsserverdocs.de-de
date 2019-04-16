---
title: "Richtlinien für Softwareeinschränkung"
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c0befad-07c3-4262-b418-372d01850305
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ab44013b947d33adc12c54b527415bf16c46a4c6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="software-restriction-policies"></a>Richtlinien für Softwareeinschränkung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema für IT-Experten beschreibt (Software Restriction Policies, SRP) in Windows Server2012 und Windows8 und enthält Links zu technischen Informationen zu SRP, beginnend mit Windows Server2003.

Verfahren und Tipps zur Problembehandlung finden Sie unter [Administer Software Restriction Policies](administer-software-restriction-policies.md) und [Problembehandlung bei Richtlinien für Softwareeinschränkung](troubleshoot-software-restriction-policies.md).

## <a name="BKMK_OVER"></a>Software Restriction Policies Beschreibung
(Software Restriction Policies, SRP) ist der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt, und die Fähigkeit zur Ausführung dieser Programme steuert. Richtlinien für Softwareeinschränkung sind Teil der Microsoft Security und Verwaltungsstrategie, die Unternehmen dabei helfen soll die Zuverlässigkeit, Integrität und verwaltbarkeit ihrer Computer zu erhöhen.

Sie können Richtlinien für Softwareeinschränkung auch verwenden, eine stark eingeschränkte Konfiguration für Computer zu erstellen, in dem Sie nur explizit angegebene Anwendungen ausführen können. Richtlinien für Softwareeinschränkung sind mit Microsoft Active Directory und Gruppenrichtlinien integriert. Sie können Richtlinien für Softwareeinschränkung auch auf eigenständigen Computern erstellen. Richtlinien für Softwareeinschränkung sind Vertrauensrichtlinien, die hierbei Vorschriften durch den Administrator eingeschränkt, Skripts und anderem Code, der nicht vollständig vertrauenswürdigen ausgeführt werden.

Sie können diese Richtlinien durch die Erweiterung von Softwareeinschränkungsrichtlinien, der den Editor für lokale Gruppenrichtlinien oder der lokalen Sicherheitsrichtlinien-Snap-In auf der Microsoft Management Console (MMC) definieren.

Ausführliche Informationen zu SRP finden Sie unter der [Software Restriction Policies Technical Overview](software-restriction-policies-technical-overview.md).

## <a name="BKMK_APP"></a>In der Praxis
Administratoren können Richtlinien für Softwareeinschränkung für die folgenden Aufgaben:

-   Definieren Sie, was als vertrauenswürdiger Code gilt

-   Entwerfen einer flexiblen Gruppenrichtlinie zum Regulieren von Skripts, ausführbaren Dateien und ActiveX-Steuerelemente

Richtlinien für Softwareeinschränkung werden erzwungen, indem Sie das Betriebssystem und Anwendungen (beispielsweise skriptanwendungen), die Einhaltung der Richtlinien für Softwareeinschränkung.

Insbesondere können Administratoren Richtlinien für Softwareeinschränkung für folgende Zwecke:

-   Geben Sie an, welche Software (ausführbare Dateien) auf Clients ausgeführt werden können

-   Verhindern Sie, dass Benutzer bestimmte Programme auf gemeinsam genutzten Computern ausführen.

-   Geben Sie an, wer vertrauenswürdige Herausgeber zu Clients hinzufügen kann

-   Legen Sie den Umfang der Softwareeinschränkungsrichtlinien (angeben, ob Richtlinien alle Benutzer auswirken oder eine Teilmenge der Benutzer auf den Clients)

-   Verhindern Sie, dass ausführbare Dateien, die auf dem lokalen Computer, Organisationseinheit (OU), Standort oder Domäne ausgeführt werden. Dies wäre in adäquat, wenn Sie nicht von Softwareeinschränkungsrichtlinien zu potenziellen Problemen durch böswillige Benutzer verwenden.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Es gibt keine Änderungen an der Funktionalität für Softwareeinschränkungsrichtlinien.

## <a name="BKMK_DEP"></a>Entfernte oder veraltete Funktionen
Es ist keine entfernten oder veralteten Funktionen für Softwareeinschränkungsrichtlinien.

## <a name="BKMK_SOFT"></a>Anforderungen der Clientsoftware
Die Erweiterung von Softwareeinschränkungsrichtlinien auf den Editor für lokale Gruppenrichtlinien kann über die MMC zugegriffen werden.

Die folgenden Features sind erforderlich, zum Erstellen und Verwalten von Softwareeinschränkungsrichtlinien auf dem lokalen Computer:

-   Editor für lokale Gruppenrichtlinien

-   Windows Installer

-   Authenticode und WinVerifyTrust

Die folgenden Features sind erforderlich, wenn Ihr Design für domänenbereitstellung dieser Richtlinien, zusätzlich zu der Liste oben aufruft:

-   Active Directory-Domänendienste

-   Gruppenrichtlinie

## <a name="BKMK_INSTALL"></a>Server-Manager-Informationen
Richtlinien für Softwareeinschränkung ist eine Erweiterung von der Editor für lokale Gruppenrichtlinien und nicht über Server-Manager, Hinzufügen von Rollen und Features installiert ist.

## <a name="BKMK_LINKS"></a>Siehe auch
Die folgende Tabelle enthält Links zu relevanten Ressourcen zum verstehen und Verwenden von SRP.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Sperren von Anwendungen mit Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|
|**Planen der**|[Software Restriction Policies Technical Overview](software-restriction-policies-technical-overview.md) (Windows Server 2012)<br /><br />[technische Referenz zu Software Restriction Policies](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx) (Windows Server 2003)|
|**Bereitstellung**|Keine Ressourcen verfügbar.|
|**Vorgänge**|[Administer Software Restriction Policies](administer-software-restriction-policies.md) (Windows Server 2012)<br /><br />[Software Restriction Policies Produkthilfe](https://technet.microsoft.com/library/cc779607(v=WS.10).aspx) (Windows Server 2003)|
|**Problembehandlung**|[Problembehandlung bei Richtlinien für Softwareeinschränkung](troubleshoot-software-restriction-policies.md) (Windows Server 2012)<br /><br />[Problembehandlung bei der Softwareeinschränkungsrichtlinien](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx) (Windows Server 2003)|
|**Sicherheit**|[Bedrohungen und Gegenmaßnahmen für Software Restriction Policies](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx) (Windows Server 2008)<br /><br />[Bedrohungen und Gegenmaßnahmen für Software Restriction Policies](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx) (Windows Server2008 R2)|
|**Tools und Einstellungen**|[Richtlinien für Softwareeinschränkung Tools und Einstellungen](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx) (Windows Server 2003)|
|**Community-Ressourcen**|[Sperren von Anwendungen mit Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|



