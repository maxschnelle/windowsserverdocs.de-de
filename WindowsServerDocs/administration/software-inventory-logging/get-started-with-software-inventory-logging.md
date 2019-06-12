---
title: Erste Schritte mit der Software Softwareinventurprotokollierung
description: Beschreibt, wie zum Installieren und starten die Protokollierung des Softwarebestands verwenden
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6944eac179c605db6c7b6f3e08f87c2329fb777f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435374"
---
# <a name="get-started-with-software-inventory-logging"></a>Erste Schritte mit der Software Softwareinventurprotokollierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

 Protokollierung des Softwarebestands sammelt Microsoft Inventardaten zu Software auf einer pro Server aggregiert. Bevor Sie die Protokollierung des Softwarebestands in Windows Server 2012 R2 verwenden, stellen Sie sicher, dass Windows Update [KB 3000850](https://support.microsoft.com/kb/3000850) und [KB 3060681](https://support.microsoft.com/kb/3060681) werden auf jedem System, die inventarisiert werden, wird installiert. Keine Windows-Update ist erforderlich für Windows Server 2016. Auch wenn SILs-Funktion zu verwenden, um Daten an einen aggregationsserver weitergeleitet werden sollen, achten Sie darauf, dass Sie eine gültige SSL-Zertifikate für Ihr Netzwerk haben.

## <a name="BKMK_OVER"></a>Featurebeschreibung
Die Protokollierung des Softwarebestands in Windows Server ist ein Feature mit einer Reihe einfacher PowerShell-Cmdlets, über die Serveradministratoren eine Liste der auf Servern installierten Microsoft-Software abrufen können. Darüber hinaus bietet sie die Möglichkeit, diese Daten für die Aggregation in regelmäßigen Abständen mithilfe des HTTPS-Protokolls über das Netzwerk zu sammeln und an einen Zielwebserver weiterzuleiten. Zum Verwalten des Features – in erster Linie zum stündlichen Sammeln und Weiterleiten – werden ebenfalls PowerShell-Befehle verwendet.

> [!NOTE]
> Ein Aggregationsserver, auf dem ein Webdienst ausgeführt wird, kann separat konfiguriert werden. Weitere Informationen zum [Aggregator der Protokollierung des Softwarebestands](software-inventory-logging-aggregator.md).

> [!IMPORTANT]
> Im Rahmen der Funktionalität des Features werden keine bei der Softwareinventurprotokollierung gesammelten Daten an Microsoft gesendet.

## <a name="BKMK_APP"></a>Praktische Anwendungen
Durch die Protokollierung des Softwarebestands sollen die Betriebskosten für das Abrufen genauer Informationen zu der lokal auf einem Server bereitgestellten Microsoft-Software reduziert werden, vor allem aber für das Abrufen dieser Informationen von mehreren Servern in einer IT-Umgebung (sofern sie in der gesamten IT-Umgebung bereitgestellt und aktiviert wird). Da die Daten an einen Aggregationsserver weitergeleitet werden können (wenn dieser separat von einem IT-Administrator eingerichtet wurde), können sie zentral, einheitlich und automatisch gesammelt werden. Die Schnittstellen können hierzu zwar direkt abgefragt werden, jedoch können mit der Protokollierung des Softwarebestands durch die Nutzung einer auf jedem Server initiierten Weiterleitungsarchitektur (über das Netzwerk) die in vielen Softwareinventur- und Ressourcenverwaltungsszenarios typischen Herausforderungen bei der Computererkennung bewältigt werden. Die über HTTPS an den Aggregationsserver eines Administrators weitergeleiteten Daten werden mit SSL gesichert. Da sich die Daten an einer zentralen Stelle (auf einem einzigen Server) befinden, können sie leichter analysiert und bearbeitet werden sowie Berichte erstellt werden. Beachten Sie, dass im Rahmen der Funktionalität des Features keine Daten an Microsoft gesendet werden. Die Daten und die Funktionalität der Softwareinventurprotokollierung sind ausschließlich zur Verwendung durch den lizenzierten Besitzer der Serversoftware und durch Administratoren gedacht.

Die Softwareinventurprotokollierung kann Serveradministratoren beim Ausführen folgender Aufgaben unterstützen:

-   Abrufen von Inventurinformationen für Software und Server von Windows-Servern (remote und bedarfsgesteuert)

-   Aggregieren von Inventurinformationen für Software und Server für eine Vielzahl von Software Asset Management-Szenarios durch Aktivieren der Protokollierung des Softwarebestands für jeden Server und Auswählen eines Ziel-URI für einen Webserver und eines Fingerabdrucks des Zertifikats für die Authentifizierung.

## <a name="see-also"></a>Siehe auch
[Aggregator der Protokollierung des Softwarebestands](https://technet.microsoft.com/library/mt572043.aspx)<br>
[Verwaltung der Protokollierung des Softwarebestands](manage-software-inventory-logging.md)<br>
[Cmdlets für die Protokollierung von Software Inventory in Windows PowerShell](https://technet.microsoft.com/library/dn283390.aspx)<br>
[Microsoft Assessment and Planning Toolkit](https://www.microsoft.com/download/en/details.aspx?id=7826)
[Volume Activation Management Tool](http://blogs.technet.com/b/volume-licensing/)

