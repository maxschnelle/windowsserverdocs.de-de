---
title: Fallstudie für Windows Admin Center SDK - Fujitsu
description: Fallstudie für Windows Admin Center SDK - Fujitsu
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6d916920b187dd3c637644a0f40ae9f9cca72b66
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2052374"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>Fujitsu ServerView Integritäts- und RAID-Erweiterungen

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>Importieren von End-to-End-Sichtbarkeit von Hardware, Betriebssystem in Windows-Verwaltungskonsole

Fujitsu ist eine führende japanische Informationen und Kommunikation Technologieunternehmen und der Hersteller [PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/) und [PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/) Server-Produkte. Die [Fujitsu ServerView Management Suite](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/) bietet eine umfassende Toolset für Server einschließlich einen serverseitiges-Agent, der eine CIM und PowerShell-Schnittstelle für die Verwaltung der Hardware bietet Anwendungslebenszyklus-Verwaltung.

Fujitsu gesehen Gelegenheit auf einfache Weise mit Windows-Verwaltungskonsole integriert, wie die serverseitige Agents CIM und PowerShell Schnittstellen, die kommunizieren konnte enthaltene haben. Das Entwicklungsteam zur Fujitsu konnte einfache Implementierung der CIM-Anrufe, die, denen Sie mit dem Agent vertraut waren, und Visualisieren der Informationen aus der Windows-Verwaltungskonsole mit den verfügbaren Komponenten zur Benutzeroberfläche.

![Fujitsu Erweiterung - Integrität Strukturansicht](../../media/extend-case-study-fujitsu/health-tree.png)

Nachdem das Team mit dem Windows Admin Center SDK vertraut änderte, konnten schnell mit aus einem einzelnen Tool erweitern, bis eine Zusammenfassungsansicht der Hardwarekomponente anzeigen und Hinzufügen von UI, um zusätzliche Hardwareinformationen verfügbar zu machen wurde häufig einfach ein paar zusätzliche Zeilen der HTML-code Integrität, Detailansichten für System-Ereignisprotokolle Treiber Monitor, trennen Sie Ansichten für Prozessor, Arbeitsspeicher, Lüfter, Netzteile, Temperaturen und Spannungswerte und sogar ein zusätzliches Tool für RAID-Management. Verwenden die UI-Steuerelemente im SDK wie etwa die Struktur, aktiviert Raster und Detail-Steuerelemente das Team Benutzeroberfläche schnell zu erstellen und zu erzielen auch einen Entwurf Visual und Interaktion mit dem Rest der Windows-Verwaltungskonsole sehr ähnlich.

![Fujitsu Erweiterung - RAID-Strukturansicht](../../media/extend-case-study-fujitsu/raid-tree.png)

![Fujitsu Erweiterung - RAID-Volumes anzeigen](../../media/extend-case-study-fujitsu/raid-volumes.png)

Die Partnerschaft zwischen Fujitsu und das Windows-Verwaltungskonsole Team zeigt deutlich den Wert der Integration in Windows-Verwaltungskonsole End-to-End-Einblick in die Serverrollen und Dienste, die für das Betriebssystem und zu Verwaltung der Hardware haben Kunden aktivieren .