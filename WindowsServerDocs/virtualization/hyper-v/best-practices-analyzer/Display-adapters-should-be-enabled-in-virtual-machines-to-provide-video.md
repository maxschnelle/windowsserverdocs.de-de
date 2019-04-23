---
title: Grafikkarten sollte auf virtuellen Computern aktiviert werden, um video bereitzustellen
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8d61461db471a876ddf46c1e5fec6992ffa80373
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870691"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>Grafikkarten sollte auf virtuellen Computern aktiviert werden, um video bereitzustellen

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu best Practices und Überprüfungen finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Das Microsoft Virtual Machine-Bus-Video-Gerät möglicherweise auf einem virtuellen Computer deaktiviert.*  
  
Microsoft Virtual Machine-Bus Videogerät ist eine virtuelle Grafikkarte, die für die Verwendung mit Hyper-V-Computer optimiert. Wenn Sie ein virtuellen Computer nicht mit der Microsoft Virtual Machine-Bus-Video-Gerät konfiguriert wurde, wird eine ältere Grafikkarte verwendet. Microsoft Virtual Machine-Bus Videogerät bietet eine bessere Leistung als eine ältere Grafikkarte.  
  
## <a name="impact"></a>Auswirkungen  
  
*Video Leistung für die folgenden virtuellen Computer wird beeinträchtigt werden:*  
  
\<Liste von Namen virtueller Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Geräte-Manager im Gastbetriebssystem, um das Microsoft Virtual Machine-Bus-Video-Gerät zu aktivieren.*  
  
Die erforderlichen Schritte zum Geräte-Manager verwenden, variieren je nach Betriebssystem. Anweisungen hierzu finden Sie in das Gastbetriebssystem zu.  
  


