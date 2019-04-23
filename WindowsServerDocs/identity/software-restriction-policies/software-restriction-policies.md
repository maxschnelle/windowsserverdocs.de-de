---
title: Richtlinien für die Softwareeinschränkung
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875821"
---
# <a name="software-restriction-policies"></a>Richtlinien für die Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema für IT-Experten wird beschrieben, (Software Restriction Policies, SRP) in Windows Server 2012 und Windows 8 und enthält Links zu technischen Informationen zu SRP, beginnend mit Windows Server 2003.

Verfahren und Tipps zur Problembehandlung finden Sie [Administer Software Restriction Policies](administer-software-restriction-policies.md) und [Problembehandlung bei Richtlinien für Softwareeinschränkung](troubleshoot-software-restriction-policies.md).

## <a name="BKMK_OVER"></a>Richtlinien für Softwareeinschränkung softwarebeschreibung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Richtlinien für Softwareeinschränkung sind Teil der Microsoft-Sicherheits- und Verwaltungsstrategie, die Unternehmen dabei helfen soll, die Zuverlässigkeit, Integrität und Verwaltbarkeit ihrer Computer zu verbessern.

Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, mit der Sie ausschließlich die Ausführung explizit ausgewiesene Anwendungen zulassen. Richtlinien für Softwareeinschränkung sind mit Microsoft Active Directory und Gruppenrichtlinien verknüpft. Sie können Richtlinien für Softwareeinschränkung auch auf eigenständigen Computern erstellen. Richtlinien für Softwareeinschränkung sind Vertrauensrichtlinien. Hierbei handelt es sich um von einem Administrator festgelegte Vorschriften, um die Ausführung von Skripts und anderem Code zu beschränken, der als nicht als absolut vertrauenswürdig erachtet wird.

Sie können diese Richtlinien über die Erweiterung %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; des Editors für lokale Gruppenrichtlinien oder über das Snap-In %%amp;quot;Lokale Sicherheitsrichtlinie%%amp;quot; der Microsoft Management Console (MMC) definieren.

Ausführliche Informationen zu SRP finden Sie unter [Software Restriction Policies Technical Overview](software-restriction-policies-technical-overview.md).

## <a name="BKMK_APP"></a>Praktische Anwendungen
Administratoren können Richtlinien für Softwareeinschränkung für die folgenden Aufgaben verwenden:

-   Definieren, was als vertrauenswürdiger Code gilt.

-   Entwerfen einer flexiblen Gruppenrichtlinie zum Regulieren von Skripts, ausführbaren Dateien und ActiveX-Steuerelementen.

Richtlinien für Softwareeinschränkung werden durch das Betriebssystem und von Anwendungen (beispielsweise Skriptanwendungen) durchgesetzt, die Richtlinien für Softwareeinschränkungen erfüllen.

Administratoren können Richtlinien für Softwareeinschränkung insbesondere für die folgenden Zwecke verwenden:

-   Angeben, welche Software (ausführbare Dateien) auf Clients ausgeführt werden darf.

-   Verhindern, dass Benutzer bestimmte Programme auf gemeinsam genutzten Computern ausführen.

-   Angeben, wer vertrauenswürdige Herausgeber zu Clients hinzufügen kann.

-   Festlegen der Reichweite der Richtlinien für Softwareeinschränkung (Angeben, ob Richtlinien alle Benutzer oder nur eine Teilmenge der Benutzer von Clients betreffen).

-   Verhindern, dass ausführbare Dateien auf dem lokalen Computer, in einer Organisationseinheit, am Standort oder in der Domäne ausgeführt werden. Dies wäre in adäquat, wenn Sie Richtlinien für Softwareeinschränkung nicht verwenden, um potenziellen Problemen durch böswillige Benutzer zu begegnen.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Für die Richtlinien für Softwareeinschränkung gibt es keine Funktionalitätsänderungen.

## <a name="BKMK_DEP"></a>Entfernten oder veralteten Funktionen
Für die Richtlinien für Softwareeinschränkung gibt es keine entferne oder veraltete Funktionalität.

## <a name="BKMK_SOFT"></a>Softwareanforderungen
Der Zugriff auf die Erweiterung %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; des Editors für lokale Gruppenrichtlinien erfolgt über die MMC.

Die folgenden Features sind erforderlich, um Richtlinien für Softwareeinschränkung auf dem lokalen Computer zu erstellen und zu pflegen:

-   Editor für lokale Gruppenrichtlinien

-   Windows Installer

-   Authenticode und WinVerifyTrust

Wenn Ihre Strategie eine Domänenbereitstellung dieser Richtlinien erfordert, sind außer den zuvor aufgeführten Features noch die folgenden Features erforderlich:

-   Active Directory Domain Services

-   Gruppenrichtlinie

## <a name="BKMK_INSTALL"></a>Informationen zur Server-Manager
Die Richtlinien für Softwareeinschränkung sind eine Erweiterung des Editors für lokale Gruppenrichtlinien und werden nicht über die Option %%amp;quot;Rollen und Features hinzufügen%%amp;quot; des Server-Managers installiert.

## <a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle finden Sie Links zu relevanten Ressourcen mit Grundlageninformationen und mit Informationen zur Verwendung von SRP.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Die Sperrung von Anwendungen mit Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|
|**Planung**|[Software Restriction Policies Technical Overview](software-restriction-policies-technical-overview.md) (WindowsServer 2012)<br /><br />[Richtlinien zur Softwareeinschränkung – Technische Referenz](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx) (Windows  Server 2003)|
|**Bereitstellung**|Keine Ressourcen verfügbar.|
|**Betrieb**|[Verwalten von Richtlinien für Softwareeinschränkung](administer-software-restriction-policies.md) (WindowsServer 2012)<br /><br />[Richtlinien für Softwareeinschränkung – Produkthilfe](https://technet.microsoft.com/library/cc779607(v=WS.10).aspx) (Windows Server 2003)|
|**Problembehandlung**|[Problembehandlung bei Richtlinien für Softwareeinschränkung](troubleshoot-software-restriction-policies.md) (WindowsServer 2012)<br /><br />[Problembehandlung bei Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx) (Windows  Server 2003)|
|**Sicherheit**|[Bedrohungen und Gegenmaßnahmen für Richtlinien für Softwareeinschränkungen](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx) (Windows  Server 2008)<br /><br />[Bedrohungen und Gegenmaßnahmen für Richtlinien für Softwareeinschränkungen](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx) (Windows  Server 2008 R2)|
|**Tools und Einstellungen**|[Tools und Einstellungen für Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx) (Windows  Server 2003)|
|**Communityressourcen**|[Die Sperrung von Anwendungen mit Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|



