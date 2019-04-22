---
title: PVLAN-Konfiguration auf einem virtuellen Switch muss konsistent sein.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b7d6d068027aa9497b00138bd1d889ea86aa3308
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813251"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>PVLAN-Konfiguration auf einem virtuellen Switch muss konsistent sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016| 
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>**Problem:**  
*Private virtuelle lokale Netzwerk (PVLAN) ist auf eine oder mehrere virtuelle Netzwerkadapter nicht ordnungsgemäß konfiguriert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*PVLAN möglicherweise nicht ordnungsgemäß isolieren Sie Netzwerkdatenverkehr zwischen virtuellen Computern.*  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie das Windows PowerShell-Cmdlet Set-VMNetworkAdapterVlan, um PVLAN ordnungsgemäß zu konfigurieren.*  
  


