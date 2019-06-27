---
title: 'Windows Admin Center-SDK-Fallstudie: Thomas-Krenn'
description: 'Windows Admin Center-SDK-Fallstudie: Thomas-Krenn'
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93b8a450aa86a454ec6febd349fcaa35df590266
ms.sourcegitcommit: 3be280c8638214857dc355b201eb56a04499a5e5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2019
ms.locfileid: "67396760"
---
# <a name="thomas-krennag-extension"></a>Thomas-Krenn.AG Extension

## <a name="intuitive-server-and-storage-health-management"></a>Intuitive integritätsverwaltung für Server und Speicher

Die Erweiterung Thomas Krenn.AG Windows Admin Center wurde speziell für die hoch verfügbare 2 Knoten [S2D Micro-Cluster](https://www.thomas-krenn.com/en/products/application/software-defined-storage/s2d-micro-cluster.html) Appliance. Die benutzerfreundliche, grafische Weboberfläche eine Micro-Cluster-Integritätsstatus über ein einfaches Dashboard visualisiert und ermöglicht Ihnen, um einen Drilldown auf Speichergeräte, Netzwerkschnittstellen oder den gesamten Cluster, um weitere Details anzuzeigen.

Diese Erweiterung bietet intuitiven Zugriff auf Informationen, die in der Regel auf oberster Ebene Service- und Aufrufe wie z. B. Seriennummern, die Softwareversionen, die speicherauslastung und vieles mehr benötigt. Es soll an Administratoren nützlich sein, die keine Erfahrung mit Windows Server hyper-konvergiert Infrastruktur haben.

Einige der Erkenntnisse verfügbar sind:
- Allgemeine Informationen über die Micro-Knoten und die Micro-Cluster
- Betriebssystem und dem Gerätestatus
- Kapazität HDD- und SSD-Status Zwischenspeichern
- Clusterereignisse
- Netzwerkstatus und Informationen

Verwenden Sie das Dashboard, um zu bestimmen, Integritätsstatus und wichtigen Systeminformationen, wie z. B. Seriennummern, Modell, Version des Betriebssystems und die Auslastung des Clusters. Darüber hinaus werden-Lüfter, die NIC und die allgemeine Integrität der Knoten-Hardware auf dem Dashboard wird ebenfalls angezeigt.

![Thomas Krenn Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-1.png)

Sie können Storage Geräten anzeigen, Seriennummern, die SMARTCARD-Status und die Ausnutzung der Speicherkapazität aufgliedern. Startgeräte werden auch Wear, Indikatoren, die neu reserviert Sektoren und Power pünktlich, sind die besten Indikatoren SSD-Integrität.

![Thomas Krenn Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-2.png)

Das Symbol für den Cluster wird erweitert, um eine Zusammenfassung der Funktionsdetails des Clusters.

![Thomas Krenn Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-3.png)

Nachdem diese Micro-Cluster Azure-Cloud-Zeuge für eine ganze Nacht nicht verfügbar war, ist ein Blick genug, um das Problem zu identifizieren. Klicken auf "Benachrichtigungen" sofort sind relevante Ereignisse für die schnelle Behebung aufgeführt. Clusterereignisse sind lokalisiert und durch die Basissprache des Betriebssystems bestimmt. Die Erweiterung selbst unterstützt Englisch und Deutsch.

![Thomas Krenn Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-4.png)

Informationen zum Netzwerk ist ebenfalls verfügbar.

![Thomas Krenn Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-5.png)

Basierend auf Kundenfeedback, haben wir auch "dunkel" Verfügbare Modus in Windows Admin Center v1904 implementiert. Dies ist die wohltuend in dunkel Rechenzentren und schlecht hervorgehobenen CAB-Dateien und Kleiderschrank aufbewahrt werden sollte. Es ist auch Windows Admin Center Zugriff auf durch Verringern der Beschichtung für Administratoren mit bestimmten sehfähigkeit.

![Thomas Krenn Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-6.png)

Thomas-Krenn realisiert sofort, dass benutzerfreundlichkeit und Barrierefreiheit für untrainiertes Administratoren Taste, um eine große benutzerfreundlichkeit für die hyperkonvergenten Infrastruktur auf dem Markt für kleine und mittelständische Unternehmen wäre. Thomas-Krenn Micro-Cluster-Erweiterung ergänzt perfekt Verwaltungsfunktionen von Windows Admin Center native HCI durch einschließlich proprietären Hardware-Informationen auf dem Dashboard und erneut gruppieren wichtig Integrität Clusterinformationen in einem neuen, Benutzerfreundlicher-Schnittstelle.

Während des Entwicklungsprozesses wurde beschlossen, Windows Admin Center 1904 in einer Konfiguration mit hoher Verfügbarkeit für den Cluster selbst sicherstellen Verwaltbarkeit auch nach dem Ausfall von Serverknoten bereitstellen. Die Erweiterung ist vorinstalliert, wie das gesamte Betriebssystem.

Die Erweiterung erstellt wurde gleichzeitig mit Windows Admin Center 1904 bei Microsoft entwickelt. Enge Zusammenarbeit und kontinuierliches Feedback verfügbar gemacht werden Probleme auf beiden Seiten, die vor dem Produkt wurde erfolgreich gestartet wird, im April 2019 gemeinsam aufgelöst wurden. Thomas-Krenn ist sehr stolz auf den ersten vollständig unterstützen, und implementieren die neuen Features von Windows Admin Center 1904.
