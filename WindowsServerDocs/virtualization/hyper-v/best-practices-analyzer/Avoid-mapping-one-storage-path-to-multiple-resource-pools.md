---
title: Vermeiden Sie die Zuordnung von einem Speicherpfad zu mehreren Ressourcenpools.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e89c0382d20d586d8c0b50396ddbd56d6fdadf0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365263"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>Vermeiden Sie die Zuordnung von einem Speicherpfad zu mehreren Ressourcenpools.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>**Problem:**  
*Ein Speicher Dateipfad ist mehreren Ressourcenpools zugeordnet.*  
  
## <a name="impact"></a>**Auswirkt**  
*Für den angegebenen Speicher Pooltyp verwenden die folgenden über-und untergeordneten Pools denselben Speicherpfad:*  
  
\<liste der Pools >  
  
## <a name="resolution"></a>**Auflösung**  
*Verwenden Sie Windows PowerShell, um die Speicherressourcen Pools so neu zu konfigurieren, dass mehrere Pools nicht denselben Speicherpfad verwenden.*  
  


