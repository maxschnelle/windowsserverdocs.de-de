---
title: Verwenden Sie mindestens SMB-Protokollversion 3,0 für Dateifreigaben, in denen Dateien für virtuelle Maschinen gespeichert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 64c78c4725c84cbd02276cb2c0eadffae42d7060
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854193"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>Verwenden Sie mindestens SMB-Protokollversion 3,0 für Dateifreigaben, in denen Dateien für virtuelle Maschinen gespeichert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Dateien für virtuelle Computer oder virtuelle Festplatten Dateien werden in einer Dateifreigabe gespeichert, die mindestens SMB-Protokollversion 3,0 nicht unterstützt.*  
  
## <a name="impact"></a>**Auswirkt**  
*Diese Konfiguration wird von Microsoft nicht unterstützt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verschieben Sie die Dateien in eine Dateifreigabe, die mindestens die SMB-Protokollversion 3,0 verwendet.*  
  


