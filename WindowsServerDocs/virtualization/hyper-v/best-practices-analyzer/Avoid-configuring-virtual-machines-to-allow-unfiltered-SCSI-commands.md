---
title: Vermeiden Sie die Konfiguration von virtuellen Computern um ungefilterten SCSI-Befehle zuzulassen
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f401ce4d72f88d72529a95acea2a999df93679b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888271"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>Vermeiden Sie die Konfiguration von virtuellen Computern um ungefilterten SCSI-Befehle zuzulassen

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu best Practices und Überprüfungen finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer wird konfiguriert, um ungefilterten SCSI-Befehle zuzulassen.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Umgehen SCSI-Befehl Filtern stellt ein Sicherheitsrisiko dar. Diese Konfiguration sollte aktiviert werden, nur dann, wenn es für die Kompatibilität mit Storage-Anwendungen, die auf das Gastbetriebssystem erforderlich ist. Die folgenden virtuellen Computer werden konfiguriert, um ungefilterten SCSI-Befehle zuzulassen:*  
  
\<Liste von Namen virtueller Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Wenden Sie sich an den Hersteller Ihrer speicherlösung, um festzustellen, ob dies erforderlich ist. Auch, wenn im Verwaltungsbetriebssystem oder andere Gastbetriebssysteme kompromittiert wurden, oder ein ungewöhnliches Verhalten aufweisen, konfigurieren Sie den virtuellen Computer, die Befehle blockieren neu.*  
  


