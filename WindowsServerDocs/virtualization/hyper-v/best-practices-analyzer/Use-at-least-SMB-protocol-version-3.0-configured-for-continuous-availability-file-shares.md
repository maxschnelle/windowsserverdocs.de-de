---
title: Verwenden Sie mindestens SMB-Protokollversion 3,0, die für fortlaufende Verfügbarkeit in Dateifreigaben konfiguriert ist, in denen Dateien für virtuelle Maschinen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a1fa5cf9-8a48-4f63-bb57-d81e63e77b30
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 18943c6b34ab74206483779db5afa06bbde04874
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854203"
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
*Diese Konfiguration wird von Microsoft nicht empfohlen, da Sie sich möglicherweise auf die Verfügbarkeit der virtuellen Computer mithilfe des-Servers auswirkt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
Führen Sie eine der folgenden Aktionen aus:  
  
-   Verschieben Sie die Dateien in eine SMB 3,0-Dateifreigabe, die für die fortlaufende Verfügbarkeit konfiguriert ist.  
  
-   Konfigurieren Sie die aktuelle Dateifreigabe neu, um fortlaufende Verfügbarkeit bereitzustellen.  
  


