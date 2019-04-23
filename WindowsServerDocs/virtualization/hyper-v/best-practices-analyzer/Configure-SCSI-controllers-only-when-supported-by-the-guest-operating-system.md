---
title: Konfigurieren von SCSI-Controller nur dann, wenn vom Gastbetriebssystem unterstützt
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3dc48602ab6c71c60fdb734ca98cf1359f58d87c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830391"
---
# <a name="configure-scsi-controllers-only-when-supported-by-the-guest-operating-system"></a>Konfigurieren von SCSI-Controller nur dann, wenn vom Gastbetriebssystem unterstützt

>Gilt für: Windows Server 2016


  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer ist mit einem SCSI-Controller konfiguriert, die verwendet werden kann, weil das Gastbetriebssystem SCSI-Controller nicht unterstützt.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Virtuelle Computer kann nicht an den SCSI-Controller angeschlossen Speicher verwenden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Fahren Sie den virtuellen Computer herunter, und Hyper-V-Manager verwenden, um den SCSI-Controller vom virtuellen Computer zu entfernen. Starten Sie den virtuellen Computer anschließend neu.*  
  


