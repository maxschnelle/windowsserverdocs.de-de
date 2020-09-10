---
title: Richtlinien für die Softwareeinschränkung
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 5c0befad-07c3-4262-b418-372d01850305
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: f4019902622b667267562a8490b6540a6c27d1e4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640235"
---
# <a name="software-restriction-policies"></a>Richtlinien für die Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema für IT-Experten werden Richtlinien für Software Einschränkung (Software Einschränkung Policies, SRP) in Windows Server 2012 und Windows 8 beschrieben. Außerdem finden Sie hier Links zu technischen Informationen zu SRP, beginnend mit Windows Server 2003.

Verfahren und Tipps zur Problembehandlung finden Sie unter [Verwalten von Richtlinien für Software Einschränkung](administer-software-restriction-policies.md) und Problembehandlung von [Software Einschränkungs Richtlinien](troubleshoot-software-restriction-policies.md).

## <a name="software-restriction-policies-description"></a><a name="BKMK_OVER"></a>Richtlinien für Softwareeinschränkung: Beschreibung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Richtlinien für Softwareeinschränkung sind Teil der Microsoft-Sicherheits- und Verwaltungsstrategie, die Unternehmen dabei helfen soll, die Zuverlässigkeit, Integrität und Verwaltbarkeit ihrer Computer zu verbessern.

Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, mit der Sie ausschließlich die Ausführung explizit ausgewiesene Anwendungen zulassen. Richtlinien für Softwareeinschränkung sind mit Microsoft Active Directory und Gruppenrichtlinien verknüpft. Sie können Richtlinien für Softwareeinschränkung auch auf eigenständigen Computern erstellen. Richtlinien für Softwareeinschränkung sind Vertrauensrichtlinien. Hierbei handelt es sich um von einem Administrator festgelegte Vorschriften, um die Ausführung von Skripts und anderem Code zu beschränken, der als nicht als absolut vertrauenswürdig erachtet wird.

Sie können diese Richtlinien über die Erweiterung %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; des Editors für lokale Gruppenrichtlinien oder über das Snap-In %%amp;quot;Lokale Sicherheitsrichtlinie%%amp;quot; der Microsoft Management Console (MMC) definieren.

Ausführliche Informationen zu SRP finden Sie in der [technischen Übersicht zu den Richtlinien für Softwareeinschränkung](software-restriction-policies-technical-overview.md).

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
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

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Für die Richtlinien für Softwareeinschränkung gibt es keine Funktionalitätsänderungen.

## <a name="removed-or-deprecated-functionality"></a><a name="BKMK_DEP"></a>Entfernte oder veraltete Funktionen
Für die Richtlinien für Softwareeinschränkung gibt es keine entferne oder veraltete Funktionalität.

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen
Der Zugriff auf die Erweiterung %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; des Editors für lokale Gruppenrichtlinien erfolgt über die MMC.

Die folgenden Features sind erforderlich, um Richtlinien für Softwareeinschränkung auf dem lokalen Computer zu erstellen und zu pflegen:

-   Editor für lokale Gruppenrichtlinien

-   Windows Installer

-   Authenticode und WinVerifyTrust

Wenn Ihre Strategie eine Domänenbereitstellung dieser Richtlinien erfordert, sind außer den zuvor aufgeführten Features noch die folgenden Features erforderlich:

-   Active Directory Domain Services

-   Gruppenrichtlinie

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>Informationen zum Server-Manager
Die Richtlinien für Softwareeinschränkung sind eine Erweiterung des Editors für lokale Gruppenrichtlinien und werden nicht über die Option %%amp;quot;Rollen und Features hinzufügen%%amp;quot; des Server-Managers installiert.

## <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle finden Sie Links zu relevanten Ressourcen mit Grundlageninformationen und mit Informationen zur Verwendung von SRP.

|Inhaltstyp|Referenzen|
|--------|-------|
|**Produktbewertung**|[Sperren von Anwendungen mit Richtlinien für Softwareeinschränkung](/previous-versions/technet-magazine/cc510322(v=msdn.10)?pr=blog)|
|**Planung**|[Software Einschränkungs Richtlinien technische Übersicht](software-restriction-policies-technical-overview.md) (Windows Server 2012)<p>[Richtlinien zur Softwareeinschränkung – Technische Referenz](/previous-versions/windows/it-pro/windows-server-2003/cc728085(v=ws.10)) (Windows  Server 2003)|
|**Bereitstellung**|Keine Ressourcen verfügbar.|
|**Vorgänge**|[Verwalten von Richtlinien für Software Einschränkung](administer-software-restriction-policies.md) (Windows Server 2012)<p>[Richtlinien für Softwareeinschränkung – Produkthilfe](/previous-versions/windows/it-pro/windows-server-2003/cc779607(v=ws.10)) (Windows Server 2003)|
|**Problembehandlung**|Problembehandlung bei [Richtlinien für Software Einschränkung](troubleshoot-software-restriction-policies.md) (Windows Server 2012)<p>[Problembehandlung bei Richtlinien für Softwareeinschränkung](/previous-versions/windows/it-pro/windows-server-2003/cc737011(v=ws.10)) (Windows  Server 2003)|
|**Security**|[Bedrohungen und Gegenmaßnahmen für Richtlinien für Softwareeinschränkungen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd349795(v=ws.10)) (Windows  Server 2008)<p>[Bedrohungen und Gegenmaßnahmen für Richtlinien für Softwareeinschränkungen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125926(v=ws.10)) (Windows  Server 2008 R2)|
|**Tools und Einstellungen**|[Tools und Einstellungen für Richtlinien für Softwareeinschränkung](/previous-versions/windows/it-pro/windows-server-2003/cc782454(v=ws.10)) (Windows  Server 2003)|
|**Communityressourcen**|[Sperren von Anwendungen mit Richtlinien für Softwareeinschränkung](/previous-versions/technet-magazine/cc510322(v=msdn.10)?pr=blog)|
