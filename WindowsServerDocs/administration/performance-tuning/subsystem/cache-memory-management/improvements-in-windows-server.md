---
title: Cache und Speicher-Manager-Verbesserungen
description: Cache "und" Speicher-Manager-Verbesserungen in WindowsServer 2016
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bd15cfc0714d1992e6b15d716b6b96ce259786da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868581"
---
# <a name="cache-and-memory-manager-improvements"></a>Cache und Speicher-Manager-Verbesserungen

Dieses Thema beschreibt die Verbesserungen bei Cache-Manager und Speicher-Manager in Windows Server 2012 und 2016.

## <a name="cache-manager-improvements-in-windows-server-2016"></a>Cache-Manager-Verbesserungen in Windows Server 2016
Cache-Manager-Unterstützung auch für "true" asynchrone liest zwischengespeichert.
Dies kann potenziell die Leistung einer Anwendung verbessern, wenn asynchrone Lesevorgänge aus zwischengespeicherten stark verwendet.  Während die meisten integrierten Dateisysteme zwischengespeicherten asynchrone Lesevorgänge für eine Weile unterstützt haben, wurden häufig leistungseinschränkungen aufgrund von verschiedenen Entwurfsoptionen, die im Zusammenhang mit der Behandlung von Thread-Pools und Dateisysteme interner Warteschlangen.  Dank der Unterstützung von Kernel ordnungsgemäßem Cache-Manager jetzt ausgeblendet, alle Thread-Pool, und Arbeit Warteschlange Verwaltungskomplexität in Dateisystemen, die somit besser verarbeiten asynchroner Zwischenspeicherung Lesevorgänge. Cache-Manager hat einen Satz von Steuerelement-Datastructures für die einzelnen (System unterstützten Maximum) VHD-Schachtelungsebenen um Parallelität zu erhöhen.


## <a name="cache-manager-improvements-in-windows-server-2012"></a>Cache-Manager-Verbesserungen in Windows Server 2012
Zusätzlich zu den Erweiterungen Cache-Manager zum Lesen von ahead Logik bei sequenziellen Arbeitslasten, eine neue API [CcSetReadAheadGranularityEx](https://msdn.microsoft.com/library/windows/hardware/hh406341.aspx) können file Systemtreiber, z.B. SMB, ändern Sie ihre read-ahead-Parameter hinzugefügt wurde. Sie können einen besseren Durchsatz für Szenarien mit remote-Datei durch Senden von mehreren kleinen Read-ahead-Anforderungen gesendet, dass eine einzelne große ahead Anforderung gelesen werden, anstatt an. Nur Kernelkomponenten, z. B. Dateisystemtreiber, können diese Werte programmgesteuert auf einer Basis pro Datei konfigurieren.

## <a name="memory-manager-improvements-in-windows-server-2012"></a>Speicher-Manager-Verbesserungen in Windows Server 2012
Aktivieren die Seite aus kann speicherauslastung auf dem Server reduziert werden, die viele private, navigierbaren Seiten mit identischem Inhalt haben. Z. B. möglicherweise Server mehrere Instanzen der gleichen speicherintensive-app oder eine einzelne app, die mit hoher Daten, funktioniert mit guten Kandidaten zum Kombinieren von Seite zu testen. Der Nachteil der Aktivierung aus der Seite ist die CPU-Nutzung.

Hier sind einige Beispiele für die Server-Rollen, in denen Seite kombiniert es unwahrscheinlich, dass viele Vorteile bieten:

-   Dateiserver (den meisten Arbeitsspeicher wird belegt, durch Datei-Seiten, die nicht privat und daher nicht mit den flexibel kombinierbaren sind)

-   Microsoft SQL Server, die zur Verwendung von AWE oder große Seiten (die meisten der Arbeitsspeicher ist privat, aber nicht auslagerbaren) konfiguriert sind

Seite kombiniert ist standardmäßig deaktiviert, kann aber aktiviert werden mithilfe der [aktivieren-MMAgent](https://technet.microsoft.com/library/jj658954.aspx) Windows PowerShell-Cmdlet. Kombinieren von Seite wurde in Windows Server 2012 hinzugefügt.
