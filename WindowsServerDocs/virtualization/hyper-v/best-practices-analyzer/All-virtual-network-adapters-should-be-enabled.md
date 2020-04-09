---
title: Alle virtuellen Netzwerkadapter sollten aktiviert sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 450a3b42529be9a85991fcaf5263bae7b7827b1a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857833"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>Alle virtuellen Netzwerkadapter sollten aktiviert sein.

>Gilt für: Windows Server 2016


  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Mindestens ein virtueller Netzwerkadapter, der einem physischen Netzwerkadapter zugeordnet ist, wird im Verwaltungs Betriebssystem deaktiviert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die Konfiguration dieses Servers ist nicht optimal.*  
  
Das Verwaltungs Betriebssystem kann keine Verbindung mit einem physischen (externen) Netzwerk über einen der physischen Netzwerkadapter auf diesem Computer herstellen, da er einem deaktivierten virtuellen Netzwerkadapter zugeordnet ist.  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie die Netzwerk-& Internet Einstellungen, um den virtuellen Netzwerkadapter zu aktivieren. Alternativ können Sie mit dem Manager für virtuelle Switches den externen virtuellen Switch so konfigurieren, dass er nicht mit dem Verwaltungs Betriebssystem gemeinsam verwendet wird.*  
  


