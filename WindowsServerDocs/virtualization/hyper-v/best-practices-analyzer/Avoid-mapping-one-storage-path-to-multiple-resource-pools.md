---
title: Vermeiden Sie die Zuordnung einen Speicherpfad auf mehreren Ressourcenpools
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 7c012836309f722e55c28b2ddbe3d54de641b4af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823961"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>Vermeiden Sie die Zuordnung einen Speicherpfad auf mehreren Ressourcenpools

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>**Problem:**  
*Ein Pfad zur Speicherdatei ist mehreren Ressourcenpools zugeordnet.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Für den angegebenen Pool Speichertyp teilen die folgenden übergeordneten und untergeordneten Pools den gleichen Speicherpfad:*  
  
\<Liste der Pools >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie Windows PowerShell, um die Speicherpools für die Ressource neu konfigurieren, damit mehrere Pools nicht den gleichen Speicherpfad verwenden.*  
  


