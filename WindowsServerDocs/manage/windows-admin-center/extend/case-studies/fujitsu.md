---
title: Windows Admin Center SDK-Fallstudie-Fujitsu
description: Windows Admin Center SDK-Fallstudie-Fujitsu
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 9acfa873e4ce7d3e91a23abff726836f0e11ce59
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357219"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>Server View-Integritäts-und RAID-Erweiterungen für Fujitsu

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>Einführung von End-to-End-Sichtbarkeit von Betriebssystem zu Hardware in Windows Admin Center

Fujitsu ist ein führendes japanisches Informations-und Kommunikationstechnologie Unternehmen und ein Hersteller von [PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/) -und [PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/) -Server Produkten. Die [Fujitsu Server View Management Suite](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/) bietet ein umfassendes Toolset für die Server Lebenszyklus Verwaltung einschließlich eines serverseitigen Agents, der eine CIM-und PowerShell-Schnittstelle für die Hardware Verwaltung bereitstellt.

Fujitsu sah eine Gelegenheit, um problemlos in Windows Admin Center integriert zu werden, als CIM-und PowerShell-Schnittstellen bereitgestellt wurden, die mit den serverseitigen Agents kommunizieren konnten. Das Entwicklungsteam von Fujitsu war in der Lage, die CIM-Aufrufe, mit denen Sie vertraut waren, auf einfache Weise zu implementieren und die Informationen im Windows Admin Center mithilfe der verfügbaren UI-Komponenten visuell darzustellen.

![Fujitsu-Erweiterung-Integritäts Strukturansicht](../../media/extend-case-study-fujitsu/health-tree.png)

Nachdem das Team mit dem Windows Admin Center SDK vertraut ist, war das Hinzufügen von Benutzeroberflächen zur Offenlegung zusätzlicher Hardwareinformationen oft einfach nur noch ein paar mehr HTML-Codezeilen, und Sie waren schnell in der Lage, von einem einzigen Tool zu erweitern, um eine Zusammenfassungs Ansicht der Hardwarekomponente anzuzeigen. Integrität, ausführliche Ansichten für System Ereignisprotokolle, Treiber Monitor, separate Ansichten für Prozessor, Arbeitsspeicher, Lüfter, Stromversorgung, Temperatur und Spannungen und sogar ein zusätzliches Tool für die RAID-Verwaltung. Durch die Verwendung von UI-Steuerelementen, die im SDK verfügbar sind, z. b. die Struktur-, Raster-und Detailbereich-Steuerelemente, konnte das Team schnell eine Benutzeroberfläche erstellen

![Fujitsu-Erweiterung-RAID-Strukturansicht](../../media/extend-case-study-fujitsu/raid-tree.png)

![Fujitsu-Erweiterung-RAID-Volumes (Ansicht)](../../media/extend-case-study-fujitsu/raid-volumes.png)

Die Partnerschaft zwischen Fujitsu und dem Windows Admin Center-Team zeigt eindeutig den Wert der Integration innerhalb des Windows Admin Centers, sodass Kunden End-to-End-Einblicke in Server Rollen und-Dienste, das Betriebssystem und die Hardware Verwaltung haben. .