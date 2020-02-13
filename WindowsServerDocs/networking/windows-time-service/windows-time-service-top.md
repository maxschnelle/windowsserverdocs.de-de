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
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405182"
---
# <a name="windows-time-service-w32time"></a>Windows-Zeitdienst (W32Time)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Der Windows-Zeitdienst (W32Time) synchronisiert das Datum und die Uhrzeit für alle Computer, die in Active Directory Domain Services (AD DS) ausgeführt werden. Die Zeitsynchronisierung ist kritisch für den ordnungsgemäßen Betrieb vieler Windows-Dienste und Branchen Anwendungen. Der Windows-Zeitdienst verwendet das Netzwerkzeitprotokoll (NTP), um Computeruhren im Netzwerk zu synchronisieren. NTP stellt sicher, dass Netzwerkvalidierungs- und Ressourcenzugriffsanforderungen ein genauer Uhrzeitwert oder Zeitstempel zugewiesen werden kann.

Im Thema „Windows-Zeitdienst (W32Time)“ findest du folgenden Inhalt:
- **[Genaue Uhrzeit für Windows Server 2016](accurate-time.md).** Die Genauigkeit der Zeitsynchronisierung in Windows Server 2016 wurde erheblich verbessert, während gleichzeitig die vollständige NTP-Abwärtskompatibilität mit älteren Windows-Versionen erhalten blieb. Unter angemessenen Betriebsbedingungen kannst du eine Genauigkeit von 1 ms in Bezug auf die UTC oder besser für Domänenmitglieder von Windows Server 2016 und Windows 10 Anniversary Update erhalten.
- **[Unterstützte Grenze für hochpräzise Umgebungen](support-boundary.md).** In diesem Artikel werden die unterstützten Grenzen für den Windows-Zeitdienst (W32Time) in Umgebungen beschrieben, in denen eine äußerst genaue und stabile Systemzeit erforderlich ist.
- **[Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md).** Die Zeitsynchronisierung in Windows 10 und Windows Server 2016 wurde erheblich verbessert.  Unter angemessenen Betriebsbedingungen können Systeme so konfiguriert werden, dass sie eine Genauigkeit von 1 ms (Millisekunden) oder besser (in Bezug auf die UTC) aufrechterhalten.
- **[Windows-Zeitdienst für Nachverfolgbarkeit](windows-time-for-traceability.md).** Bestimmungen in vielen Sektoren erfordern, dass Systeme bezogen auf UTC ablaufverfolgbar sind.  Dies bedeutet, dass die Abweichung eines Systems in Bezug auf die UTC nachgewiesen werden kann.  Zum Aktivieren regulatorischer Complianceszenarien bieten Windows 10 und Server 2016 neue Ereignisprotokolle, um ein Bild aus der Perspektive des Betriebssystems bereitzustellen und so ein Verständnis der an der Systemuhr vorgenommenen Aktionen zu erstellen.  Diese Ereignisprotokolle werden fortlaufend für den Windows-Zeitdienst generiert und können untersucht sowie zur späteren Analyse archiviert werden.
- **[Technische Referenz zum Windows-Zeitdienst](windows-time-service-tech-ref.md).** Der W32Time-Dienst bietet Uhrsynchronisierung im Netzwerk für Computer, ohne dass eine größere Konfiguration erforderlich ist. Der W32Time-Dienst ist für den erfolgreichen Betrieb der Kerberos V5-Authentifizierung und somit für die AD DS basierte Authentifizierung von wesentlicher Bedeutung.
    - **[Funktionsweise des Windows-Zeitdiensts](How-the-Windows-Time-Service-Works.md).** Obwohl es sich beim Windows-Zeitdienst nicht um eine exakte Implementierung des Netzwerkzeitprotokolls (Network Time Protocol, NTP) handelt, verwendet er die komplexe Suite von Algorithmen, die in den NTP-Spezifikationen definiert sind, um sicherzustellen, dass Uhren auf Computern innerhalb eines Netzwerks so genau wie möglich sind.
    - **[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md).** Die meisten Domänenmitgliedscomputer verfügen über einen Zeitclient vom Typ NT5DS, was bedeutet, dass sie die Zeit aus der Domänenhierarchie synchronisieren. Die einzige typische Ausnahme hierbei ist der Domänencontroller, der als Betriebsmaster der Stammdomäne der Gesamtstruktur des PDC-Emulators (Primärer Domänencontroller) fungiert, der in der Regel so konfiguriert ist, dass er die Zeit mit einer externen Zeitquelle synchronisiert.


## <a name="related-topics"></a>Verwandte Themen
Weitere Informationen zur Domänenhierarchie und zum Bewertungssystem findest du im Blogbeitrag [Was ist der Windows-Zeitdienst?](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) .

Das Windows-Zeitanbieter-Plug-In-Modell ist [auf TechNet dokumentiert](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx).

Ein Nachtrag, auf den im Artikel „Windows 2016 – Genaue Uhrzeit“ verwiesen wird, kann [hier](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf) heruntergeladen werden.

Eine kurze Übersicht über den Windows-Zeitdienst findest du in diesem [Übersichtsvideo](https://aka.ms/WS2016TimeVideo).
