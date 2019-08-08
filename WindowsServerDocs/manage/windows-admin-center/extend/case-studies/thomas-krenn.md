---
title: 'Fallstudie zum Windows Admin Center SDK: Thomas-Krenn'
description: 'Fallstudie zum Windows Admin Center SDK: Thomas-Krenn'
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93b8a450aa86a454ec6febd349fcaa35df590266
ms.sourcegitcommit: 3be280c8638214857dc355b201eb56a04499a5e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2019
ms.locfileid: "67396760"
---
# <a name="thomas-krennag-extension"></a>Thomas-Krenn.AG-Erweiterung

## <a name="intuitive-server-and-storage-health-management"></a>Intuitive Server- und Speicherintegritätsverwaltung

Die Thomas Krenn.AG-Erweiterung für das Windows Admin Center wurde speziell für die [S2D Micro-Cluster](https://www.thomas-krenn.com/en/products/application/software-defined-storage/s2d-micro-cluster.html)-Appliance mit Hochverfügbarkeit und zwei Knoten entwickelt. Die benutzerfreundliche grafische Weboberfläche visualisiert den Integritätsstatus eines Mikroclusters über ein einfaches Dashboard und ermöglicht einen Drilldown auf Speichergeräte, Netzwerkschnittstellen oder den gesamten Cluster, um weitere Details anzuzeigen.

Die Erweiterung bietet intuitiven Zugriff auf Informationen, die häufig für Dienste auf oberster Ebene und Supportanfragen benötigt werden (z. B. Seriennummern, Softwareversionen, Speicherauslastung usw.). Sie ist für Administratoren vorgesehen, die keine Erfahrung mit der hyperkonvergenten Windows Server-Infrastruktur haben.

Folgenden Erkenntnisse sind u. a. verfügbar:
- Allgemeine Informationen zu den Mikroknoten und dem Mikrocluster
- Betriebssystem-/Startgerätestatus
- Kapazität der HDD und Cachestatus der SSD
- Clusterereignisse
- Netzwerkstatus und -informationen

Verwenden Sie das Dashboard, um den Integritätsstatus des Clusters und wichtige Systeminformationen wie Seriennummern, Modell, Betriebssystemversion und Auslastung zu ermitteln. Darüber hinaus werden auch Informationen zur Hardwareintegrität z. B. von Lüfter, NIC und gesamtem Knoten auf dem Dashboard angezeigt.

![Thomas-Krenn-Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-1.png)

Sie können einen Drilldown in Speichergeräte durchführen, um Seriennummern, den SMART-Status und die Kapazitätsauslastung anzuzeigen. Startgeräte zeigen auch Abnutzungsindikatoren, neu zugewiesene Sektoren und die aktive Zeit an – also die wichtigsten Daten zur SSD-Integrität.

![Thomas-Krenn-Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-2.png)

Das Clusterstatussymbol kann erweitert werden, um eine Zusammenfassung der Betriebsdetails des Clusters anzuzeigen.

![Thomas-Krenn-Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-3.png)

Nachdem der Azure-Cloudzeuge dieses Mikroclusters für eine ganze Nacht nicht verfügbar war, genügt ein Blick, um das Problem zu identifizieren. Wenn Sie auf „Notifications“ (Benachrichtigungen) klicken, werden sofort relevante Ereignisse für eine schnelle Wiederherstellung aufgelistet. Clusterereignisse werden in die Basissprache des Betriebssystems lokalisiert und durch diese festgelegt. Die Erweiterung selbst unterstützt Englisch und Deutsch.

![Thomas-Krenn-Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-4.png)

Netzwerkinformationen sind ebenfalls verfügbar.

![Thomas-Krenn-Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-5.png)

Basierend auf Kundenfeedback haben wir auch den „Dark Mode“ aus Windows Admin Center v1904 implementiert. Dieser eignet sich für dunkle Rechenzentren und schlecht beleuchtete Schaltschränke. Außerdem vereinfacht die Erweiterung die Nutzung des Windows Admin Centers, da der Bildschirm weniger stark leuchtet und so Administratoren mit bestimmten visuellen Beeinträchtigungen entgegenkommt.

![Thomas-Krenn-Erweiterung](../../media/extend-case-study-thomas-krenn/thomas-krenn-6.png)

Thomas-Krenn hat sofort erkannt, dass die Benutzerfreundlichkeit und Barrierefreiheit für untrainierte Administratoren ein wichtiger Aspekt hoher Kundenfreundlichkeit bei der hyperkonvergenten Infrastruktur sind und auf dem Markt für kleine und mittlere Unternehmen entscheidend sind. Die Mikrocluster-Erweiterung von Thomas-Krenn ergänzt die nativen HCI-Verwaltungsfunktionen von Windows Admin Center perfekt. Sie können proprietäre Hardwareinformationen auf dem Dashboard hinzufügen und wichtige Informationen zur Clusterintegrität auf einer neuen, benutzerfreundlichen Oberfläche zusammenfassen.

Schon während der Entwicklung wurde beschlossen, Windows Admin Center 1904 in einer Konfiguration mit Hochverfügbarkeit im Cluster selbst bereitzustellen, um die Verwaltbarkeit auch nach Knotenausfällen sicherzustellen. Die Erweiterung ist – wie das gesamte Betriebssystem – bereits vorinstalliert.

Die Erweiterung wurde parallel zur Entwicklung von Windows Admin Center 1904 bei Microsoft erstellt. Durch eine enge Zusammenarbeit und kontinuierliches Feedback konnten Probleme auf beiden Seiten schon vor dem erfolgreichen Start des Produkts im April 2019 behoben werden. Thomas-Krenn ist ausgesprochen stolz darauf, als eines der ersten Unternehmen die neuen Features von Windows Admin Center 1904 vollständig zu unterstützen und zu implementieren.
