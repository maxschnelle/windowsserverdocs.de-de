---
title: Verwenden Sie mindestens SMB-Protokoll, Version 3.0, die für die fortlaufende Verfügbarkeit auf Dateifreigaben, die Dateien für virtuelle Maschinen speichern konfiguriert
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a1fa5cf9-8a48-4f63-bb57-d81e63e77b30
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 67f41293433bd8d14096688fbaa23eb43334c738
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877871"
---
# <a name="use-at-least-smb-protocol-version-30-configured-for-continuous-availability-on-file-shares-that-store-files-for-virtual-machines"></a>Verwenden Sie mindestens SMB-Protokoll, Version 3.0, die für die fortlaufende Verfügbarkeit auf Dateifreigaben, die Dateien für virtuelle Maschinen speichern konfiguriert

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
*Dateien für virtuelle Maschinen oder virtuelle Festplattendateien werden auf einer Netzwerkdateifreigabe gespeichert, die mit dem Feature für fortlaufende Verfügbarkeit von SMB-Protokoll, Version 3.0 nicht konfiguriert ist.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Microsoft empfiehlt diese Konfiguration nicht, da es die Verfügbarkeit der virtuellen Computer mithilfe des Servers auswirken kann. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
Führen Sie eine der folgenden Aktionen aus:  
  
-   Verschieben Sie die Dateien auf eine SMB 3.0-Dateifreigabe, die für die fortlaufende Verfügbarkeit konfiguriert ist.  
  
-   Konfigurieren Sie die aktuelle Dateifreigabe um kontinuierliche Verfügbarkeit bereitzustellen.  
  


