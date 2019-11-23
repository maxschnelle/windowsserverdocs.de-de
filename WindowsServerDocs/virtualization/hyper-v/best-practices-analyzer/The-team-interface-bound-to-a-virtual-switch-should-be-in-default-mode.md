---
title: Die an einen virtuellen Switch gebundene Team Schnittstelle sollte sich im Standardmodus befinden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9bfd0c98e865a0faae8dd70e97696e2c2682531b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393431"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>Die an einen virtuellen Switch gebundene Team Schnittstelle sollte sich im Standardmodus befinden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Einige virtuelle Switches sind an eine Team Schnittstelle gebunden, aber die Team Schnittstelle übergibt nicht den Datenverkehr für alle VLANs an die virtuellen Switches.*  
  
## <a name="impact"></a>**Auswirkt**  
*Die folgenden virtuellen Switches können nicht auf alle VLANs zugreifen: \n{0}*  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie Server-Manager oder das Windows PowerShell-Cmdlet Set-netlbfoteamnic, um die Team Schnittstelle auf den Standardmodus zurückzusetzen.*  
  


