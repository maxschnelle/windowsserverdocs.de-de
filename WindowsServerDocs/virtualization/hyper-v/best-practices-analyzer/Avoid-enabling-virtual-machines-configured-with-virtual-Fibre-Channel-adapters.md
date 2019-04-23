---
title: Aktivieren Sie die virtuellen Computer mit virtuellen Fibre Channel-Adapter zum live-Migrationen zu ermöglichen, wenn es weniger Pfade auf Fibre Channel logische Einheiten (LUNs) auf dem Zielserver als auf dem Quellcomputer sind konfiguriert
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6ff69d5cb09133a806c2a2df3446713264a4e892
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849551"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>Aktivieren Sie die virtuellen Computer mit virtuellen Fibre Channel-Adapter zum live-Migrationen zu ermöglichen, wenn es weniger Pfade auf Fibre Channel logische Einheiten (LUNs) auf dem Zielserver als auf dem Quellcomputer sind konfiguriert

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
*Eine oder mehrere virtuelle Computer müssen die AllowReducedFcRedunancy-Eigenschaft, die in der Virtualisierungs-WMI-Anbieter festgelegt.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Live Migration die folgenden virtuellen Computer möglicherweise dazu führen, dass Daten verloren gehen oder e/a in den Speicher zu unterbrechen:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Erwägen Sie die AllowReducedFcRedundancy WMI-Eigenschaft auf die betroffenen virtuellen Computer deaktivieren. Wenn diese Eigenschaft deaktiviert ist, können Sie eine Livemigration ausführen, auf virtuellen Computern, die mit virtuellen Fibre Channel-Adapter konfiguriert werden, nur, wenn die Anzahl der Pfade mit Fibre Channel auf dem Ziel identisch oder größer als die Anzahl von Pfaden für die Quelle ist. Mit diesen Überprüfungen können Daten verloren gehen oder Unterbrechung der e/a in den Speicher zu verhindern.* 