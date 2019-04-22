---
title: Stellen Sie sicher, dass alle obligatorischen virtuellen switcherweiterungen verfügbar sind.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 53ceeb9aab6ca7196454fbcd7f0fdae8b34d05d2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825941"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>Stellen Sie sicher, dass alle obligatorischen virtuellen switcherweiterungen verfügbar sind.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Eine oder mehrere virtuelle Netzwerkadapter verbunden sind mit einem virtuellen Switch mit erforderliche Erweiterungen, die deaktiviert oder nicht installiert werden.*  
  
## <a name="impact"></a>Auswirkungen  
*Netzwerkdatenverkehr ist auf eine oder mehrere virtuelle Netzwerkadapter auf die folgenden virtuellen Computer blockiert:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Zunächst stellen Sie sicher, dass die erforderliche Erweiterung auf dem Host installiert wurde, und installieren Sie die Erweiterung aus, falls erforderlich. Klicken Sie dann, wenn die erforderliche Erweiterung deaktiviert ist, verwenden Sie Manager für virtuelle Switches oder das Windows PowerShell-Cmdlet Enable-VMSwitchExtension zum Aktivieren der Erweiterung.*  
  


