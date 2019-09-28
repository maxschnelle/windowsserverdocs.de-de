---
title: Verwenden Sie mindestens SMB-Protokollversion 3,0, die für fortlaufende Verfügbarkeit in Dateifreigaben konfiguriert ist, in denen Dateien für virtuelle Maschinen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a1fa5cf9-8a48-4f63-bb57-d81e63e77b30
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3a6cbb6052e2e50b7fd78792c5e01885d7672932
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393341"
---
# <a name="use-at-least-smb-protocol-version-30-configured-for-continuous-availability-on-file-shares-that-store-files-for-virtual-machines"></a>Verwenden Sie mindestens SMB-Protokollversion 3,0, die für fortlaufende Verfügbarkeit in Dateifreigaben konfiguriert ist, in denen Dateien für virtuelle Maschinen

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
*Dateien für virtuelle Computer oder virtuelle Festplatten Dateien werden auf einer Netzwerkdatei Freigabe gespeichert, die nicht mit dem Feature für die kontinuierliche Verfügbarkeit der SMB-Protokollversion 3,0 konfiguriert ist.*  
  
## <a name="impact"></a>**Auswirkt**  
*Microsoft empfiehlt diese Konfiguration nicht, da Sie sich möglicherweise auf die Verfügbarkeit der virtuellen Computer mithilfe des-Servers auswirkt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>**Auflösung**  
Führen Sie eines der folgenden Verfahren aus:  
  
-   Verschieben Sie die Dateien in eine SMB 3,0-Dateifreigabe, die für die fortlaufende Verfügbarkeit konfiguriert ist.  
  
-   Konfigurieren Sie die aktuelle Dateifreigabe neu, um fortlaufende Verfügbarkeit bereitzustellen.  
  


