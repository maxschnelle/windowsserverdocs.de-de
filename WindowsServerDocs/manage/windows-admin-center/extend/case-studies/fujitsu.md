---
title: 'Windows Admin Center-SDK-Fallstudie: Fujitsu'
description: 'Windows Admin Center-SDK-Fallstudie: Fujitsu'
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6d916920b187dd3c637644a0f40ae9f9cca72b66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814991"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>Fujitsu ServerView Integrität und RAID-Erweiterungen

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>Einbinden von End-to-End-Sichtbarkeit von Hardware, des Betriebssystems in Windows Admin Center

Fujitsu ist eine führende japanische IT- und IT-Unternehmen und Hersteller von [PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/) und [PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/) Serverprodukte. Die [Fujitsu ServerView Management Suite](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/) umfasst ein umfangreiches Toolset für Server einschließlich einen serverseitigen-Agent, der eine CIM- und PowerShell-Schnittstelle für die hardwareverwaltung bietet Anwendungslebenszyklus-Verwaltung.

Fujitsu haben die Möglichkeit, mühelos in Windows Admin Center integrieren lassen, wie sie CIM und PowerShell-Schnittstellen, die kommunizieren konnte mit den serverseitigen-Agents bereitgestellt. Das Entwicklungsteam auf Fujitsu konnte auf einfache Weise implementieren die CIM-Aufrufe, die, denen Sie für den Agent mit vertraut waren, und Visualisieren Sie die Informationen in die verfügbaren Komponenten der Benutzeroberfläche mithilfe von Windows Admin Center zur Verfügung.

![Fujitsu Erweiterung - Health-Strukturansicht](../../media/extend-case-study-fujitsu/health-tree.png)

Nachdem das Team vertraut sind, mit dem Windows Admin Center-SDK wurde, Hinzufügen von Benutzeroberfläche, um zusätzliche Hardware-Informationen verfügbar machen häufig einfach ein paar weitere Textzeilen HTML-Code war, und sie konnten schnell erweitern Sie in einem einzelnen Tool für die Anzeige einer zusammenfassenden Darstellung der Hardware-Komponente Integrität und die ausführliche Ansichten für die Systemereignisprotokolle, Treiber überwachen, trennen Sie Ansichten für Prozessor, Arbeitsspeicher, Lüfter, Netzteile, Temperaturen und Spannung und sogar ein zusätzliches Tool zur Verwaltung von RAID. Verwenden die UI-Steuerelemente, die im SDK wie z. B. der Struktur verfügbar, aktiviert Raster und Details-Steuerelemente das Team schnell Benutzeroberfläche erstellen, und erreichen auch einen Entwurf Visual und Interaktion sehr ähnlich, mit der restlichen Windows Admin Center.

![Fujitsu Erweiterung - RAID-Strukturansicht](../../media/extend-case-study-fujitsu/raid-tree.png)

![Fujitsu-Erweiterung – Anzeigen von RAID-volumes](../../media/extend-case-study-fujitsu/raid-volumes.png)

Die Partnerschaft zwischen Fujitsu und dem Windows Admin Center-Team zeigt eindeutig den Wert der Integration in Windows Admin Center, damit Kunden, damit End-to-End-Einblick in die Serverrollen und Dienste, um das Betriebssystem und hardwareverwaltung .