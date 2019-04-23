---
title: Konfigurieren von Gastbetriebssystemen für VSS-Sicherungen zum Aktivieren von App-konsistente Momentaufnahmen für Hyper-V-Replikat
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b4300dd4b7adc0cef8544215b5da62044a97301b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863891"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>Konfigurieren von Gastbetriebssystemen für VSS-Sicherungen zum Aktivieren von App-konsistente Momentaufnahmen für Hyper-V-Replikat

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*App-konsistente Momentaufnahmen erfordert, dass die Volumeschattenkopie-Dienst (Volume Shadow Copy Services, VSS) aktiviert und konfiguriert werden, in die Gastbetriebssysteme von virtuellen Computern, die bei der Replikation beteiligt ist.*  
  
## <a name="impact"></a>Auswirkungen  
*Auch wenn die Konfiguration der Replikation mit anwendungskonsistenten Momentaufnahmen angegeben werden, wird Hyper-V nicht verwenden, wenn VSS konfiguriert ist. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie Verbindung mit virtuellen Computern, um Integrationsservices auf dem virtuellen Computer zu installieren.*  
  


