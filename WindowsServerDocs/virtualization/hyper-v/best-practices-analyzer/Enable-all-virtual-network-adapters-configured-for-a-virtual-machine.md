---
title: Alle für einen virtuellen Computer konfigurierten virtuellen Netzwerkadapter aktivieren
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 79971ff503afcc1a087aced579e30989233c2b4a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861963"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>Alle für einen virtuellen Computer konfigurierten virtuellen Netzwerkadapter aktivieren

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
  
*Ein oder mehrere Netzwerkadapter sind möglicherweise auf einem virtuellen Computer deaktiviert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die folgenden virtuellen Computer verfügen möglicherweise nicht über eine Netzwerk Konnektivität:*  
  
\<Liste der Namen der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Geräte-Manager im Gast Betriebssystem, um alle virtuellen Netzwerkadapter zu aktivieren. Wenn der Adapter nicht erforderlich ist, verwenden Sie den Hyper-V-Manager, um ihn vom virtuellen Computer zu entfernen.*  
  


