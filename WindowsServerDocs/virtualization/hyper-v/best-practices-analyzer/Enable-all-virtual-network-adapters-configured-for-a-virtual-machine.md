---
title: Aktivieren Sie alle virtuellen Netzwerkadapter konfiguriert, die für einen virtuellen Computer
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: fbb1ef5283f6ccf8dfa355a09a86040be80f53e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844231"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>Aktivieren Sie alle virtuellen Netzwerkadapter konfiguriert, die für einen virtuellen Computer

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
  
*Ist möglicherweise eine oder mehrere Netzwerkadapter auf einem virtuellen Computer deaktiviert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die folgenden virtuellen Computer möglicherweise nicht über eine Netzwerkverbindung verfügen:*  
  
\<Liste von Namen virtueller Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Geräte-Manager im Gastbetriebssystem, um alle virtuellen Netzwerkadapter zu aktivieren. Wenn der Adapter nicht erforderlich ist, verwenden Sie Hyper-V-Manager, um es aus dem virtuellen Computer zu entfernen.*  
  


