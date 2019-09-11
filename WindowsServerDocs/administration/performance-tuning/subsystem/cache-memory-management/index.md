---
title: Leistungsoptimierung für Cache- und Speicher-Manager-Subsysteme
description: Leistungsoptimierung für Cache- und Speicher-Manager-Subsysteme
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 628a73f66e15940f184a076ad72fc24ad75b0e6c
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866420"
---
# <a name="performance-tuning-cache-and-memory-manager"></a>Leistungsoptimierung für Cache- und Speicher-Manager

Standardmäßig speichert Windows Dateidaten zwischen, die von Datenträgern gelesen und auf Datenträger geschrieben werden. Dies bedeutet, dass Lesevorgänge Dateidaten aus einem als Systemdateicache bezeichneten Bereich im Systemspeicher statt von dem physischen Datenträger lesen. Entsprechend schreiben Schreibvorgänge Dateidaten in den Systemdateicache statt auf den Datenträger, und diese Art von Cache wird als Zurückschreibcache bezeichnet. Zwischenspeichern wird auf Dateiobjektbasis verwaltet. Das Zwischenspeichern wird vom Cache-Manager gesteuert, der kontinuierlich aktiv ist, während Windows ausgeführt wird.

Dateidaten im Systemdateicache werden in vom Betriebssystem bestimmten Intervallen auf den Datenträger geschrieben. Geleerte Seiten bleiben entweder im Systemcache-Arbeitssatz (wenn FILE\_FLAG\_RANDOM\_ACCESS festgelegt ist und das Dateihandle nicht geschlossen wurde) oder auf der Standbyliste, wo sie Teil des verfügbaren Arbeitsspeichers werden.

Die Richtlinie zur Verzögerung beim Schreiben von Daten in die Datei und ihrer Beibehaltung im Cache, bis der Cache geleert wird, wird als „Lazy Writing“ bezeichnet und in einem bestimmten Zeitintervall vom Cache-Manager ausgelöst. Die Zeit, zu der ein Dateidatenblock geleert wird, basiert teilweise auf dem Zeitraum, für den er im Cache gespeichert wurde, und auf der Zeit, die seit dem letzten Zugriff auf die Daten in einem Lesevorgang verstrichen ist. Dadurch wird sichergestellt, dass die Möglichkeit des Zugriffs auf häufig gelesene Dateidaten im Systemdateicache für eine maximale Zeitspanne erhalten bleibt.

Dieses Zwischenspeichern von Dateidaten wird in der folgenden Abbildung dargestellt:

![Zwischenspeichern von Dateidaten](../../media/perftune-guide-file-data-caching.png)

Wie mit den durchgezogenen Pfeilen in der obigen Abbildung dargestellt, wird ein 256-KB-Datenbereich bei der ersten Anforderung durch den Cache-Manager während eines Dateilesevorgangs in einen 256-KB-Cacheslot im Systemadressraum eingelesen. Ein Benutzermodusprozess kopiert die Daten in diesem Slot dann in seinen eigenen Adressraum. Wenn der Prozess den Datenzugriff abgeschlossen hat, schreibt er die geänderten Daten wieder in denselben Slot im Systemcache, wie mit dem gestrichelten Pfeil zwischen den Adressraum des Prozesses und dem Systemcache dargestellt. Wenn der Cache-Manager ermittelt hat, dass die Daten für einen bestimmten Zeitraum nicht mehr benötigt werden, schreibt er die geänderten Daten zurück in die Datei auf dem Datenträger, wie mit dem gestrichelten Pfeil zwischen dem Systemcache und dem Datenträger dargestellt.

**In diesem Abschnitt:**

-   [Problembehandlung bei Cache- und Speicher-Manager-Leistungsproblemen](troubleshoot.md)

-   [Cache- und Speicher-Manager-Verbesserungen in WindowsServer 2016](improvements-in-2016.md)
