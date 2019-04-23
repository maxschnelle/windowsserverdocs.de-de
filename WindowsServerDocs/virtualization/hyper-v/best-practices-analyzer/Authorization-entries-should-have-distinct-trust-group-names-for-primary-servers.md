---
title: Replikationsautorisierungseinträge müssen unterschiedliche Vertrauensstellung Gruppennamen primären Servern mit virtuellen Computern, die nicht Teil die gleiche vertrauensgruppe sind
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8827a3a7-9f3c-4f51-826a-8e2ec43e01df
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e5c5b1a6bf8ef0bbceb5dde6b28cd951f399fc5e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882961"
---
# <a name="authorization-entries-should-have-distinct-trust-group-names-for-primary-servers-with-virtual-machines-that-are-not-part-of-the-same-trust-group"></a>Replikationsautorisierungseinträge müssen unterschiedliche Vertrauensstellung Gruppennamen primären Servern mit virtuellen Computern, die nicht Teil die gleiche vertrauensgruppe sind

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
*Der Server akzeptiert replikationsanforderungen für den replizierten virtuellen Computer aus einem der Server in der Authorization-Liste, die mit dem gleichen Tag der Replikation wie der virtuelle Computer verknüpft ist.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Es gibt möglicherweise Datenschutz- und Sicherheitsaspekte mit einem virtuellen Computer akzeptieren die Replikation vom primären Server, die zu verschiedenen replikationsautorisierungseinträge gehören. Dies wirkt sich auf die folgenden autorisierungseinträge: \<Liste der replikationsautorisierungseinträge >*  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie unterschiedliche Tags in den Einträgen für die Autorisierung für den primären Server mit virtuellen Computern, die nicht die gleiche Sicherheitsgruppe gehören. Ändern Sie die Hyper-V-Einstellungen, um die Tags für die Replikation konfigurieren.*  
  


