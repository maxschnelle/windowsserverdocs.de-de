---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows-Zeitdienst
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: a86c2bdde9c65878b228f153009734da8f03960d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856831"
---
# <a name="windows-time-service-w32time"></a>Windows Time Service (W32Time)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Datum und Uhrzeit für alle Computer mit in Active Directory Domain Services (AD DS), wird der Windows-Zeitdienst (W32Time) synchronisiert. Die uhrzeitsynchronisierung ist für die ordnungsgemäße Ausführung von vielen Windows-Diensten und Line-of-Business (LOB)-Anwendungen von entscheidender Bedeutung. Der Windows-Zeitdienst verwendet das Network Time Protocol (NTP), um Computertakt auf das Netzwerk zu synchronisieren. NTP wird sichergestellt, dass eine genaue Uhrzeit oder Zeitstempel zu Netzwerk-Überprüfung und Resource Access-Anforderungen zugewiesen werden kann.

Im Thema Windows-Zeitdienst (W32Time) ist Folgendes verfügbar:
- **[Windows Server 2016 – genaue Uhrzeit](accurate-time.md).** Synchronisierung uhrzeitsynchronisierungsdienst in Windows Server 2016 wurde erheblich, und gleichzeitig vollständige Abwärtskompatibilität NTP-Kompatibilität mit älteren Windows-Versionen verbessert. Unter angemessenen betriebsbedingungen 1 verwaltet werden können ms Genauigkeit in Bezug auf die UTC-Zeit oder besser für Mitglieder der Domäne Windows Server 2016 und Windows 10 Anniversary Update.
- **[Begrenzung der Unterstützung für Umgebungen mit hoher Genauigkeit](support-boundary.md).** Dieser Artikel beschreibt die Grenzen der Unterstützung für den Windows-Zeitdienst (W32Time) in Umgebungen, die äußerst präzise und stabile-System stets angefordert wird.
- **[Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md).** Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde erheblich verbessert.  Unter betriebsbedingungen sinnvoll, Systeme zum Verwalten von 1 ms (Millisekunden) konfiguriert werden können Genauigkeit oder höher (in Bezug auf UTC).
- **[Windows-Zeit für die Nachverfolgbarkeit](windows-time-for-traceability.md).** In vielen Bereichen geltender werden Systeme in UTC zurückverfolgt werden.  Dies bedeutet, dass es sich bei eines Systems Offset in Bezug auf UTC nachgewiesen werden kann.  Um die Einhaltung gesetzlicher Bestimmungen Szenarien zu ermöglichen, bietet Windows 10 und Server 2016 neuen Ereignisprotokolle auf ein Bild aus der Perspektive des Betriebssystems, um einen Überblick über die Aktionen, die auf der Systemzeit zu bilden.  Diese Ereignisprotokolle kann werden kontinuierlich für Windows-Zeitdienst generiert und überprüft oder zur späteren Analyse archiviert werden.
- **[Technische Referenz zu Windows Time Service](windows-time-service-tech-ref.md).** Der W32Time-Dienst stellt die Synchronisation des Computertakts Netzwerk für Computer ohne umfassende Konfiguration bereit. Der W32Time-Dienst ist wichtig, um den reibungslosen Betrieb Kerberos V5-Authentifizierung und somit auf AD DS-basierte Authentifizierung.
    - **[Funktionsweise der Windows-Zeitdienst](How-the-Windows-Time-Service-Works.md).** Obwohl der Windows-Zeitdienst nicht um eine genaue Implementierung des Network Time Protocol (NTP) ist, wird die komplexe Sammlung von Algorithmen, die in den NTP-Spezifikationen, um sicherzustellen, dass die Uhren auf den Computern in einem Netzwerk so exakt wie möglich definiert ist.
    - **[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md).** Die meisten Domänenmitgliedscomputer weisen den Typ Client Zeit NT5DS, was bedeutet, dass sie aus der Domänenhierarchie synchronisiert. Nur typische eine Ausnahme ist der Domänencontroller, der als primärer Domänencontroller (PDC) Emulationsbetriebsmaster des von der Stammdomäne der Gesamtstruktur, die in der Regel konfiguriert ist fungiert, um die Zeit mit einer externen Zeitquelle synchronisieren.


## <a name="related-topics"></a>Verwandte Themen
Weitere Informationen über die Domänenhierarchie und Punktesystems finden Sie unter den ["Was ist Windows-Zeitdienst?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) .

Die Anbieter-Plug-in das Modell für Windows ist [auf TechNet-Website dokumentiert](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx).

Ein Nachtrag der Windows 2016 genau Zeit-Artikel kann heruntergeladen werden [hier](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)

Für eine kurze Übersicht über Windows-Zeitdienst, sehen Sie sich diese [auf hoher Ebene übersichtsvideo](https://aka.ms/WS2016TimeVideo).

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

