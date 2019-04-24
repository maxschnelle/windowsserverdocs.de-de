---
title: Leistungsoptimierung für Webserver
description: Empfehlungen zur Leistungsoptimierung für Webserver unter Windows Server 16
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: DavSo; Ericam; YaShi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 72a7a8c2bc7e90a24e8c47c9296aa6670010cd0a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891821"
---
# <a name="performance-tuning-web-servers"></a>Leistungsoptimierung für Webserver


In diesem Thema werden Methoden für die Leistungsoptimierung und Empfehlungen für Windows Server 2016-Webserver beschrieben.


## <a name="selecting-the-proper-hardware-for-performance"></a>Auswählen der richtigen Hardware für die Leistung


Es ist wichtig, die richtige Hardware für die zu erwartende Weblast auswählen, indem Sie die durchschnittliche Last, Spitzenlast, Kapazität, geplanten Erweiterungen und Antwortzeiten berücksichtigen. Aufgrund von Hardwareengpässen wird die Effektivität der Softwareoptimierung eingeschränkt.

[Leistungsoptimierung für Serverhardware](../../hardware/index.md) enthält Empfehlungen für Hardware, um die folgenden Leistungseinschränkungen zu vermeiden:

-   Langsame CPUs bieten begrenzte Rechenleistung für CPU-intensive Workloads wie ASP, ASP.NET und TLS-Szenarien.

-   Ein kleiner L2- oder L3/LLC-Prozessorcache kann die Leistung beeinträchtigen.

-   Eine begrenzte Menge an Arbeitsspeicher wirkt sich auf die Anzahl der zu hostenden Websites, die Anzahl der speicherbaren dynamischen Inhaltsskripte (z.B. ASP.NET) und die Anzahl der Anwendungspools oder Arbeitsprozesse aus.

-   Das Netzwerk wird durch einen ineffizienten Netzwerkadapter zu einem Engpass.

-   Das Dateisystem wird durch ein ineffizientes Datenträgersubsystem oder einen Speicheradapter zu einem Engpass.

## <a name="operating-system-best-practices"></a>Bewährte Methoden für das Betriebssystem


Beginnen Sie nach Möglichkeit mit einer Neuinstallation des Betriebssystems. Ein Upgrade der Software kann veraltete, unerwünschte oder suboptimale Registrierungseinstellungen und zuvor installierte Dienste und Anwendungen, die Ressourcen verbrauchen, außer Kraft setzen, wenn sie automatisch gestartet werden. Wenn ein anderes Betriebssystem installiert ist und Sie es behalten müssen, sollten Sie das neue Betriebssystem auf einer anderen Partition installieren. Andernfalls überschreibt die neue Installation die Einstellungen unter %Program Files%\\Common Files.

Um Störungen beim Datenträgerzugriff zu reduzieren, platzieren Sie die Systemauslagerungsdatei, das Betriebssystem, Webdaten, den ASP-Vorlagen-Cache und das Protokoll der Internet Information Services (IIS) auf separaten physischen Datenträgern, wenn möglich.

Installieren Sie, wenn möglich, Microsoft SQL Server und IIS auf verschiedenen Servern, um die Konflikte um die Systemressourcen zu verringern.

Vermeiden Sie die Installation nicht notwendiger Dienste und Anwendungen. In einigen Fällen kann es sinnvoll sein, Dienste zu deaktivieren, die auf einem System nicht benötigt werden.

## <a name="ntfs-file-system-settings"></a>Einstellungen für das NTFS-Dateisystem

Der system-global Switch **NtfsDisableLastAccessUpdate** (REG\_DWORD) 1 befindet sich unter **HKLM\\System\\CurrentControlSet\\Control\\FileSystem** und ist standardmäßig auf 1 gesetzt. Dieser Switch reduziert die E/A-Last und Latenzen des Datenträgers, indem er die Aktualisierung von Zeitstempel und Uhrzeit für den letzten Datei- oder Verzeichniszugriff deaktiviert. Neuinstallationen von Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 aktivieren diese Einstellung standardmäßig, und Sie müssen sie nicht anpassen. Bei früheren Versionen von Windows wurde dieser Schlüssel nicht festgelegt. Wenn auf Ihrem Server eine frühere Version von Windows ausgeführt wird oder er auf Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 aktualisiert wurde, sollten Sie diese Einstellung aktivieren.

Das Deaktivieren der Updates ist wirkungsvoll, wenn Sie große Datensätze (oder viele Hosts) verwenden, die Tausende von Verzeichnissen enthalten. Wir empfehlen, stattdessen die IIS-Protokollierung zu verwenden, wenn Sie diese Informationen nur für die Webverwaltung beibehalten.

>[!Warning]
> Einige Anwendungen, wie z.B. die Hilfsprogramme für inkrementelle Sicherungen, sind auf diese Aktualisierungsinformationen angewiesen und funktionieren ohne sie nicht ordnungsgemäß.

## <a name="see-also"></a>Siehe auch
- [IIS 10.0-Leistungsfeineinstellung](tuning-iis-10.md)
- [HTTP 1.1/2-Optimierung](http-performance.md)


