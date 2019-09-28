---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows-Zeitdienst
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: e3dbaa188426ac81073e706db3adc6ab0a655c01
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405182"
---
# <a name="windows-time-service-w32time"></a>Windows-Zeit Dienst (W32Time)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Der Windows-Zeit Dienst (W32Time) synchronisiert das Datum und die Uhrzeit für alle Computer, die in Active Directory Domain Services (AD DS) ausgeführt werden. Die Zeitsynchronisierung ist entscheidend für den ordnungsgemäßen Betrieb vieler Windows-Dienste und Branchen Anwendungen (LOB-Anwendungen). Der Windows-Zeit Dienst verwendet das Netzwerk Zeitprotokoll (NTP), um Computeruhren im Netzwerk zu synchronisieren. NTP stellt sicher, dass einer Netzwerk Validierung und Ressourcen Zugriffs Anforderungen ein genauerer Uhrzeitwert oder Zeitstempel zugewiesen werden kann.

Im Thema Windows-Zeit Dienst (W32Time) ist der folgende Inhalt verfügbar:
- **[Windows Server 2016 genaue Zeit](accurate-time.md).** Die Genauigkeit der Zeitsynchronisierung in Windows Server 2016 wurde erheblich verbessert, während die NTP-Kompatibilität mit älteren Windows-Versionen vollständig abwärts bleibt. Unter angemessenen Betriebsbedingungen können Sie eine Genauigkeit von 1 MS in Bezug auf die UTC oder besser für Domänen Mitglieder von Windows Server 2016 und Windows 10 Anniversary Update erhalten.
- **[Unterstützung von Grenzen für Umgebungen mit hoher Genauigkeit](support-boundary.md).** In diesem Artikel werden die unterstützten Grenzen für den Windows-Zeit Dienst (W32Time) in Umgebungen beschrieben, in denen eine sehr genaue und stabile Systemzeit erforderlich ist.
- **[Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md).** Die Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde wesentlich verbessert.  Unter angemessenen Betriebsbedingungen können Systeme so konfiguriert werden, dass Sie eine Genauigkeit von 1 ms (Millisekunden) oder eine bessere Genauigkeit (in Bezug auf die UTC) erhalten.
- **[Windows-Zeit für die Rückverfolgbarkeit](windows-time-for-traceability.md).** Für Vorschriften in vielen Sektoren ist es erforderlich, dass Systeme für die UTC in der UTC-  Dies bedeutet, dass der Offset eines Systems in Bezug auf die UTC bestätigt werden kann.  Zum Aktivieren von compliancekompatibilitäts Szenarien werden von Windows 10 und Server 2016 neue Ereignisprotokolle bereitgestellt, um ein Bild aus der Perspektive des Betriebssystems bereitzustellen und ein Verständnis der auf der Systemuhr ausgeführten Aktionen zu bilden.  Diese Ereignisprotokolle werden fortlaufend für den Windows-Zeit Dienst generiert und können zur späteren Analyse überprüft oder archiviert werden.
- **[Technische Referenz für den Windows-Zeit Dienst](windows-time-service-tech-ref.md).** Der W32Time-Dienst ermöglicht die Synchronisierung von Netzwerk Uhren für Computer, ohne dass eine umfassende Konfiguration erforderlich ist. Der W32Time-Dienst ist für den erfolgreichen Betrieb der Kerberos V5-Authentifizierung und somit für die AD DS basierte Authentifizierung unverzichtbar.
    - **[Wie der Windows-Zeit Dienst funktioniert](How-the-Windows-Time-Service-Works.md).** Obwohl es sich bei dem Windows-Zeit Dienst nicht um eine exakte Implementierung des Netzwerk Zeit Protokolls (Network Time Protocol, NTP) handelt, verwendet er die komplexe Suite von Algorithmen, die in den NTP-Spezifikationen definiert sind, um sicherzustellen, dass Uhren auf Computern innerhalb eines Netzwerks so genau wie möglich sind.
    - **[Windows-Zeit Dienst Tools und-Einstellungen](Windows-Time-Service-Tools-and-Settings.md).** Die meisten Domänen Mitglieds Computer verfügen über den Zeit Clienttyp eine NT5DS, was bedeutet, dass Sie die Zeit von der Domänen Hierarchie synchronisieren. Die einzige typische Ausnahme ist der Domänen Controller, der als Emulator-Betriebs Master des primären Domänen Controllers (PDC) der Stamm Domäne der Gesamtstruktur fungiert, der in der Regel so konfiguriert ist, dass die Zeit mit einer externen Zeit Quelle synchronisiert wird.


## <a name="related-topics"></a>Verwandte Themen
Weitere Informationen zur Domänen Hierarchie und zum Bewertungssystem finden Sie unter ["Was ist der Windows-Zeit Dienst?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) . .

Das Windows-Zeit Anbieter-Plug-in-Modell ist [auf TechNet dokumentiert](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx).

Ein Nachtrag, auf den der Artikel Windows 2016-Zeit genaue Zeit verweist, kann [hier](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf) heruntergeladen werden.

Eine kurze Übersicht über den Windows-Zeit Dienst finden Sie in diesem [Übersichts Video](https://aka.ms/WS2016TimeVideo).
