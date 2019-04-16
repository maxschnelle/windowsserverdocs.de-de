---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows-Zeitdienst
description: ''
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 02/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b997d1f26e8da82e0d595b1ce13763e0a87d6d03
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="windows-time-service-w32time"></a>Windows-Zeitdienst (W32Time)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Windows-Zeitdienst (W32Time) synchronisiert, Datum und Uhrzeit für alle Computer in Active Directory-Domänendiensten (AD DS) ausgeführt wird. Die zeitsynchronisierung ist für den ordnungsgemäßen Betrieb des viele Windows-Dienste und Anwendungen Line-of-Business (LOB). Windows-Zeitdienst verwendet das Netzwerkzeitprotokoll (NTP), um Computeruhren im Netzwerk zu synchronisieren. NTP wird sichergestellt, dass eine genaue Uhrzeitwert oder Zeitstempel, Überprüfung und Ressource Zugriffsanforderungen Netzwerk zugewiesen werden kann.

Im Thema zum Windows-Zeitdienst (W32Time) ist der folgende Inhalt zur Verfügung:
- **[Windows2016 – genaue Uhrzeit](accurate-time.md).** Synchronisierung zeitgenauigkeit in Windows Server2016 wurde deutlich, Beibehaltung uneingeschränkter NTP-Kompatibilität mit älteren Windows-Versionen verbessert.  Unter angemessenen Betriebsbedingungen können Sie verwalten, eine 1 ms Genauigkeit in Bezug auf UTC oder besser für Windows Server2016 und Windows10 Anniversary Update Mitglieder der Domäne.
- **[technische Referenz zu Windows Time Service](windows-time-service-tech-ref.md).** Der W32Time-Dienst bietet Netzwerk Computertakts für Computer ohne umfassende Konfiguration. Der W32Time-Dienst ist wichtig für die erfolgreiche Ausführung des Kerberos V5-Authentifizierung und daher auf AD DS-basierte Authentifizierung.
    - **[Funktionsweise von Windows-Zeitdienst](How-the-Windows-Time-Service-Works.md).** Windows-Zeitdienst ist, zwar keine genaue Implementierung von der Netzwerkzeitprotokoll (NTP) verwendet er die komplexe Suite von Algorithmen, die in den NTP-Spezifikationen, um sicherzustellen, dass die Uhren auf mehreren Computern in einem Netzwerk so genau wie möglich definiert ist.
    - **[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md).** Die meisten Domänenmitgliedscomputer ist eine Zeit Client NT5DS, was bedeutet, dass sie Zeit aus der Domäne zu synchronisieren. Nur normalerweise eine Ausnahme ist der Domänencontroller, der als primärer Domänencontroller (PDC) Emulationsbetriebsmaster des der Stammdomäne der Gesamtstruktur, der in der Regel konfiguriert ist fungiert, Zeit mit einer externen Zeitquelle synchronisieren.

## <a name="related-topics"></a>Verwandte Themen
Weitere Informationen über die Domänenhierarchie und Karten finden Sie unter der ["Was ist Windows-Zeitdienst?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) Blogbeitrag.

Das Windows Zeit Anbieter-Plug-In-Modell ist [in TechNet dokumentiert](https://msdn.microsoft.com/en-us/library/windows/desktop/ms725475%28v=vs.85%29.aspx).

Ein Zusatz verwiesen wird, durch den Windows-Zeitdienst ab 2016 genau Artikel heruntergeladen werden [hier](http://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)

Für eine kurze Übersicht über Windows-Zeitdienst, sehen Sie sich diese [grobe Übersicht über Video](https://aka.ms/WS2016TimeVideo).

<!-- In this guide
In this guide:
Windows Accurate Time
High Accuracy
Support Boundary
Configuration for High Accuracy
Traceability for Compliance
Best Practices
Technical Reference
How the Windows Time Service Works
Windows Time Service Tools and Settings
-->

