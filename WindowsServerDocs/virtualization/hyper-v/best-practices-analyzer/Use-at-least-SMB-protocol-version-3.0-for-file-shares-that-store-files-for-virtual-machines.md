---
title: Verwenden Sie mindestens SMB-Protokoll, Version 3.0 für Dateifreigaben, die Dateien für virtuelle Maschinen speichern.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 28e0f3769fd4fc993710d0a0b800dfad7c9ab157
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834341"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>Verwenden Sie mindestens SMB-Protokoll, Version 3.0 für Dateifreigaben, die Dateien für virtuelle Maschinen speichern.

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
*Dateien für virtuelle Maschinen oder virtuelle Festplattendateien werden gespeichert, auf einer Dateifreigabe, die nicht mindestens unterstützt SMB 3.0-Protokoll-Version.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Diese Konfiguration wird von Microsoft nicht unterstützt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verschieben Sie die Dateien an eine Dateifreigabe, die mindestens verwendet SMB-Protokoll, Version 3.0.*  
  


