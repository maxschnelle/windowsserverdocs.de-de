---
title: Verbesserungen bei Cache und Arbeitsspeicher
description: Cache- und Speicher-Manager-Verbesserungen in WindowsServer 2016
ms.topic: article
ms.author: pavel; atales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: c2fdceb7ff3743890c73ee4108ffcf8e00fe437f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992053"
---
# <a name="cache-and-memory-manager-improvements"></a>Verbesserungen bei Cache und Arbeitsspeicher

In diesem Thema werden die Verbesserungen von Cache Manager und Speicher-Manager in Windows Server 2012 und 2016 beschrieben.

## <a name="cache-manager-improvements-in-windows-server-2016"></a>Cache Manager-Verbesserungen in Windows Server 2016
Cache-Manager hat auch Unterstützung für echte asynchrone zwischengespeicherte Lesevorgänge hinzugefügt.
Dies kann möglicherweise die Leistung einer Anwendung verbessern, wenn Sie stark von asynchronen zwischengespeicherten Lesevorgängen abhängig ist.Obwohl bei den meisten in-Box-Dateisystemen asynchrone zwischengespeicherte Lesevorgänge für eine Weile unterstützt wurden, gab es häufig Leistungseinschränkungen aufgrund verschiedener Entwurfs Optionen im Zusammenhang mit der Verarbeitung von internen Arbeits Warteschlangen für Thread Pools und Dateisysteme.Durch die Unterstützung von Kernel-Proper verbirgt der Cache-Manager jetzt alle Komplexitäten der Thread Pool-und Arbeits Warteschlangen Verwaltung von Dateisysteme, was die Verarbeitung von asynchronen zwischengespeicherten Lesevorgängen effizienter macht. Der Cache-Manager verfügt über eine Gruppe von Steuerungs datastructures für jede der (vom System unterstützten maximalen) VHD-Schachtelungs Ebenen zum Maximieren der Parallelität.


## <a name="cache-manager-improvements-in-windows-server-2012"></a>Cache Manager-Verbesserungen in Windows Server 2012
Zusätzlich zu den Verbesserungen des Cache-Managers für die Read-Ahead-Logik für sequenzielle Arbeits Auslastungen wurde eine neue API [ccsetreadaheadgranularityex](/windows-hardware/drivers/ifs/ccsetreadaheadgranularityex) hinzugefügt, um Dateisystemtreibern, wie z. b. SMB, die Read-Ahead-Parameter Sie ermöglicht einen besseren Durchsatz für Remote Datei Szenarien, indem mehrere kleine Lese Anforderungen gesendet werden, statt eine einzelne große Read-Ahead-Anforderung zu senden. Nur Kernel Komponenten (z. b. Dateisystem Treiber) können diese Werte Programm gesteuert auf Datei Basis konfigurieren.

## <a name="memory-manager-improvements-in-windows-server-2012"></a>Verbesserungen der Speicherverwaltung in Windows Server 2012
Durch das Aktivieren der Seiten Kombination kann die Speicherauslastung auf Servern reduziert werden, die über viele private, kostenpflichtige Seiten mit identischem Inhalt verfügen. Beispielsweise können Server, auf denen mehrere Instanzen derselben speicherintensiven app ausgeführt werden, oder eine einzelne APP, die mit stark wiederkehrenden Daten arbeitet, gute Kandidaten für die Seiten Kombination sein. Der Nachteil beim Aktivieren der Seiten Kombination ist eine größere CPU-Auslastung.

Im folgenden finden Sie einige Beispiele für Server Rollen, bei denen es unwahrscheinlich ist, dass die Seiten Kombination viele Vorteile bietet:

-   Dateiserver (der meiste Arbeitsspeicher wird von Datei Seiten genutzt, die nicht privat und daher nicht kombinierbar sind)

-   Microsoft SQL-Server, die für die Verwendung von AWE oder großen Seiten konfiguriert sind (der größte Teil des Speichers ist privat, aber nicht kostenpflichtig)

Die Seiten Kombination ist standardmäßig deaktiviert, kann jedoch mithilfe des Windows PowerShell-Cmdlets [enable-mmagent](/powershell/module/mmagent/enable-mmagent?view=win10-ps) aktiviert werden. Die Seiten Kombination wurde in Windows Server 2012 hinzugefügt.