---
title: Beginnen Sie mit der Protokollierung des Software Bestands
description: Beschreibt, wie die Protokollierung des Software Bestands installiert und gestartet wird.
ms.custom: na
ms.prod: windows-server
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed51c13c-7cbf-4144-a675-011fd29379d4
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a38c984b2d81fc4db980a969ef0312109950b867
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382997"
---
# <a name="get-started-with-software-inventory-logging"></a>Beginnen Sie mit der Protokollierung des Software Bestands

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Bei der Protokollierung des Software Bestands werden Microsoft-Software Inventur Daten pro Server erfasst. Bevor Sie die Protokollierung des Software Bestands mit Windows Server 2012 R2 verwenden, stellen Sie sicher, dass Windows Update [KB 3000850](https://support.microsoft.com/kb/3000850) und [KB 3060681](https://support.microsoft.com/kb/3060681) auf jedem System installiert sind, das inventarisiert wird. Für Windows Server 2016 ist keine Windows Update erforderlich. Wenn Sie die Funktion von SIL zum Weiterleiten von Daten an einen Aggregations Server verwenden möchten, stellen Sie sicher, dass Sie über SSL-Zertifikate für Ihr Netzwerk verfügen.

## <a name="BKMK_OVER"></a>Funktionsbeschreibung
Die Protokollierung des Softwarebestands in Windows Server ist ein Feature mit einer Reihe einfacher PowerShell-Cmdlets, über die Serveradministratoren eine Liste der auf Servern installierten Microsoft-Software abrufen können. Darüber hinaus bietet sie die Möglichkeit, diese Daten für die Aggregation in regelmäßigen Abständen mithilfe des HTTPS-Protokolls über das Netzwerk zu sammeln und an einen Zielwebserver weiterzuleiten. Zum Verwalten des Features – in erster Linie zum stündlichen Sammeln und Weiterleiten – werden ebenfalls PowerShell-Befehle verwendet.

> [!NOTE]
> Ein Aggregationsserver, auf dem ein Webdienst ausgeführt wird, kann separat konfiguriert werden. Weitere Informationen zum [Aggregator der Protokollierung des Softwarebestands](software-inventory-logging-aggregator.md).

> [!IMPORTANT]
> Keine der von der Software Inventur Protokollierung gesammelten Daten werden im Rahmen der Funktionalität des Features an Microsoft gesendet.

## <a name="BKMK_APP"></a>Praktische Anwendungen
Durch die Protokollierung des Softwarebestands sollen die Betriebskosten für das Abrufen genauer Informationen zu der lokal auf einem Server bereitgestellten Microsoft-Software reduziert werden, vor allem aber für das Abrufen dieser Informationen von mehreren Servern in einer IT-Umgebung (sofern sie in der gesamten IT-Umgebung bereitgestellt und aktiviert wird). Da die Daten an einen Aggregationsserver weitergeleitet werden können (wenn dieser separat von einem IT-Administrator eingerichtet wurde), können sie zentral, einheitlich und automatisch gesammelt werden. Die Schnittstellen können hierzu zwar direkt abgefragt werden, jedoch können mit der Protokollierung des Softwarebestands durch die Nutzung einer auf jedem Server initiierten Weiterleitungsarchitektur (über das Netzwerk) die in vielen Softwareinventur- und Ressourcenverwaltungsszenarios typischen Herausforderungen bei der Computererkennung bewältigt werden. SSL dient zum Sichern von Daten, die über HTTPS an den Aggregations Server eines Administrators weitergeleitet werden. Da sich die Daten an einer zentralen Stelle (auf einem einzigen Server) befinden, können sie leichter analysiert und bearbeitet werden sowie Berichte erstellt werden. Beachten Sie, dass im Rahmen der Funktionalität des Features keine Daten an Microsoft gesendet werden. Daten und Funktionen der Protokollierung des Software Bestands sind nur für die Verwendung durch den lizenzierten Besitzer und die Administratoren der Server Software vorgesehen.

Die Softwareinventurprotokollierung kann Serveradministratoren beim Ausführen folgender Aufgaben unterstützen:

-   Abrufen von Inventurinformationen für Software und Server von Windows-Servern (remote und bedarfsgesteuert)

-   Aggregierte Software-und Server Inventur Informationen für eine Vielzahl von Software Asset Management-Szenarien durch Aktivieren der Protokollierungsfunktion des Software Bestands für jedes Server und Auswählen eines Ziel-URIs für den Webserver und des Zertifikat Fingerabdrucks für die Authentifizierung.

## <a name="see-also"></a>Weitere Informationen
[Aggregator der Protokollierung des Softwarebestands](https://technet.microsoft.com/library/mt572043.aspx)<br>
[Verwaltung der Protokollierung des Softwarebestands](manage-software-inventory-logging.md)<br>
[Cmdlets für die Protokollierung des Software Bestands in Windows PowerShell](https://technet.microsoft.com/library/dn283390.aspx)<br>
[Microsoft Assessment and Planning Toolkit](https://www.microsoft.com/download/en/details.aspx?id=7826)
[Tool für die Volumen Aktivierungs Verwaltung](http://blogs.technet.com/b/volume-licensing/)

