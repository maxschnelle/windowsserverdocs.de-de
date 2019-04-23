---
title: Bieten Sie alle verfügbaren integrationskonten Dienste für virtuelle Computer
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2c4b2043-ad81-495e-aa7a-467f813bb3d2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c2b5137594f78980f87f6520ae4b4af8203aef32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883781"
---
# <a name="offer-all-available-integration-services-to-virtual-machines"></a>Bieten Sie alle verfügbaren integrationskonten Dienste für virtuelle Computer

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Eine oder mehrere verfügbare Integrationsdienste sind nicht auf virtuellen Computern aktiviert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Einige Funktionen werden nicht für die folgenden virtuellen Computer verfügbar:*  
  
\<Liste von Namen virtueller Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Erwägen Sie andernfalls, bietet alle Integration Services in den Einstellungen dieser virtuellen Computer aus.*  
  
Die Verfügbarkeit einiger Integration Dienste kann über die Einstellungen des virtuellen Computers verwaltet werden.   
  
#### <a name="to-manage-the-availability-of-integration-services-to-a-virtual-machine"></a>Um die Verfügbarkeit von Integrationsservices an einen virtuellen Computer zu verwalten.  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Ergebnisbereich unter **VMs**, wählen Sie den virtuellen Computer, die Sie konfigurieren möchten.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie unter **Management**, klicken Sie auf **Integrationsdienste**.  
  
5.  Wählen Sie das Kontrollkästchen für die einzelnen Dienste, die Sie für die virtuelle Maschine anbieten möchten, in der Liste von Integrationsservices. Wenn das Kontrollkästchen nicht verfügbar ist, ist, dass bestimmte Integration-Dienst von Gast-Betriebssystems, die auf dem virtuellen Computer ausgeführt wird, nicht unterstützt wird.  
  


