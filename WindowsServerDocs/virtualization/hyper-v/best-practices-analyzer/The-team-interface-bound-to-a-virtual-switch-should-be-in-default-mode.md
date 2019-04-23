---
title: Die teamschnittstelle, die mit einem virtuellen Switch gebunden sollte im standardmäßigen Modus sein.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 22e5ad0eed6e6ea07a83150762b76163442f2c5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872161"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>Die teamschnittstelle, die mit einem virtuellen Switch gebunden sollte im standardmäßigen Modus sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Einige virtuelle Switches auf einem teamschnittstelle gebunden sind, aber die teamschnittstelle nicht auf allen VLANs Datenverkehr übergeben, um die virtuellen Switches.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Die folgenden virtuellen Switches auf allen VLANs sind keine: \n{0}*  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie Server-Manager oder das Windows PowerShell-Cmdlet Set-NetLbfoTeamNic, die teamschnittstelle auf den Standardmodus zurückzusetzen.*  
  


