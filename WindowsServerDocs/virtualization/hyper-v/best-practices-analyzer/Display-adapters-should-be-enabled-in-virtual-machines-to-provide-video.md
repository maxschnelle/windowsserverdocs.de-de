---
title: Anzeige Adapter sollten auf virtuellen Computern aktiviert werden, um Videofunktionen bereitzustellen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0c515c7fb1ed160dfee1e1b7303022082e936157
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364908"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>Anzeige Adapter sollten auf virtuellen Computern aktiviert werden, um Videofunktionen bereitzustellen.

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Das Video Gerät für den Microsoft Virtual Machine Bus ist möglicherweise auf einem virtuellen Computer deaktiviert.*  
  
Das Videogerät für den Microsoft Virtual Machine Bus ist ein virtueller Grafikadapter, der für die Verwendung mit virtuellen Hyper-V-Computern optimiert ist. Wenn ein virtueller Computer nicht für die Verwendung des Microsoft Virtual Machine Bus-Videogeräts konfiguriert ist, wird eine Legacy Grafikkarte verwendet. Das Videogerät des Microsoft Virtual Machine Bus-Videos ist besser als eine ältere Grafikkarte.  
  
## <a name="impact"></a>Auswirkungen  
  
*Die Video Leistung für die folgenden virtuellen Computer wird beeinträchtigt:*  
  
\<liste der Namen der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Geräte-Manager im Gast Betriebssystem, um das Video Gerät für den Microsoft Virtual Machine Bus zu aktivieren.*  
  
Die Schritte, die für die Geräte-Manager Verwendung von erforderlich sind, sind je nach Betriebssystem unterschiedlich. Anweisungen hierzu finden Sie in der Hilfe zum Gast Betriebssystem.  
  


