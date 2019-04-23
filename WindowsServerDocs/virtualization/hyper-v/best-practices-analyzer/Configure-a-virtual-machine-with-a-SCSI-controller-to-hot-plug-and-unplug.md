---
title: Konfigurieren eines virtuellen Computers mit einem SCSI-Controller in der Lage zu "Hot" Plug & trennen Sie Speicher im laufenden Systembetrieb
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 511e1172-aeef-463d-b5dd-2bffae411ff1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 755e7485e54ee58e0acd7ebd75a7ee591aa655f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843281"
---
# <a name="configure-a-virtual-machine-with-a-scsi-controller-to-be-able-to-hot-plug-and-hot-unplug-storage"></a>Konfigurieren eines virtuellen Computers mit einem SCSI-Controller in der Lage zu "Hot" Plug & trennen Sie Speicher im laufenden Systembetrieb

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
  
*Ein virtuellen Computer wurde gefunden, die nicht mit einem SCSI-Controller konfiguriert ist.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Es werden nicht möglich "heiß" Plug oder Speicher für die folgenden virtuellen Computer "Hot" zu trennen:*  
  
\<Liste von Namen virtueller Computer >  
  
Die Möglichkeit, "heiß" Plug oder trennen Sie Speicher im laufenden Systembetrieb erleichtert es, um die speicheranforderungen eines virtuellen Computers zu verwalten, ohne Ausfallzeiten. Virtuelle Computer ohne SCSI-Controller muss heruntergefahren werden, hinzufügen oder Entfernen von Speicher zu können.  
  
## <a name="resolution"></a>Auflösung  
  
*Wenn Sie nicht benötigen, "heiß" Plug oder Speicher für diesen virtuellen Computer "Hot" zu trennen, ist keine Aktion erforderlich. Andernfalls fahren Sie den virtuellen Computer herunter, und der Konfiguration einen SCSI-Controller hinzufügen.*  
  
Um verwenden Sie einen SCSI-Controller an "Hot", und trennen Sie Speicher im laufenden Systembetrieb, muss das Gastbetriebssystem die aktuelle Version von Integrationsservices ausgeführt werden.  
  


