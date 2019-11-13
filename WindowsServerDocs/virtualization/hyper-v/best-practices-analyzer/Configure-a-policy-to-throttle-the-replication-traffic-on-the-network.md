---
title: Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5b3afd594f56973007a2f0f4318de8a8c7a98209
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365113"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Möglicherweise gibt es keine Beschränkung für die Menge an Netzwerkbandbreite, die von der Replikation beansprucht werden darf.*  
  
## <a name="impact"></a>Auswirkungen  
*Die Netzwerkbandbreite könnte vollständig von Replikations Datenverkehr dominiert werden Dies wirkt sich auf die folgenden Ports aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Wenn Sie eine andere Methode zum Einschränken des Netzwerk Datenverkehrs verwenden, können Sie dies ignorieren. Verwenden Sie andernfalls Gruppenrichtlinie-Editor, um eine Richtlinie zu konfigurieren, die den Netzwerk Datenverkehr zum relevanten Port des Replikat Servers drosselt.*  
  
  


