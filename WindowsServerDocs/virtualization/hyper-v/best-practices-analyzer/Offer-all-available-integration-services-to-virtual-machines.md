---
title: Alle verfügbaren Integrationsdienste für virtuelle Maschinen anbieten
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2c4b2043-ad81-495e-aa7a-467f813bb3d2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5ec2dc73cea8b8356d832bf9fdb960985df2df6c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393604"
---
# <a name="offer-all-available-integration-services-to-virtual-machines"></a>Alle verfügbaren Integrationsdienste für virtuelle Maschinen anbieten

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Mindestens ein verfügbarer Integrations Dienst ist auf virtuellen Computern nicht aktiviert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Einige Funktionen sind für die folgenden virtuellen Computer nicht verfügbar:*  
  
\<liste der Namen der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Andernfalls sollten Sie alle Integrationsdienste in den Einstellungen dieser virtuellen Computer anbieten.*  
  
Die Verfügbarkeit einiger Integrationsdienste kann über die Einstellungen des virtuellen Computers verwaltet werden.   
  
#### <a name="to-manage-the-availability-of-integration-services-to-a-virtual-machine"></a>So verwalten Sie die Verfügbarkeit von Integrationsdiensten für eine virtuelle Maschine  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den virtuellen Computer aus, den Sie konfigurieren möchten.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie unter **Verwaltung**auf **Integration Services**.  
  
5.  Aktivieren Sie in der Liste der Integrationsdienste das Kontrollkästchen für jeden Dienst, den Sie dem virtuellen Computer anbieten möchten. Wenn ein Kontrollkästchen nicht verfügbar ist, wird dieser bestimmte Integrations Dienst nicht von dem Gast Betriebssystem unterstützt, das auf dem virtuellen Computer ausgeführt wird.  
  


