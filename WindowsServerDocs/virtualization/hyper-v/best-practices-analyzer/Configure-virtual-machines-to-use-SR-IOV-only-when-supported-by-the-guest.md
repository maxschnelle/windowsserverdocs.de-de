---
title: Konfigurieren von virtuellen Computern zur Verwendung von SR-IOV nur, wenn durch das Gastbetriebssystem unterstützt.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 33cf5b68-e43e-47ef-adbc-6b266c1d4dce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e5c2acb21fe8b11e8f020c6d2ab1742116c23b28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833361"
---
# <a name="configure-virtual-machines-to-use-sr-iov-only-when-supported-by-the-guest-operating-system"></a>Konfigurieren von virtuellen Computern zur Verwendung von SR-IOV nur, wenn durch das Gastbetriebssystem unterstützt.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Eine oder mehrere virtuelle Computer sind für die Verwendung von Single-Root i/o-Virtualisierung (SR-IOV) konfiguriert, aber das Gastbetriebssystem SR-IOV nicht unterstützt*  
  
## <a name="impact"></a>Auswirkungen  
*Virtuelle SR-IOV-Funktionen werden nicht die folgenden virtuellen Computer zugeordnet werden:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Deaktivieren Sie SR-IOV auf allen virtuellen Computern, die Gastbetriebssysteme ausgeführt, die keine SR-IOV unterstützen.*  
  
SR-IOV wird nur in eine 64-Bit-Windows-Gäste unterstützt. Weitere Informationen finden Sie unter [Hyper-V-Feature-Kompatibilität nach Generation und Gast](../Hyper-V-feature-compatibility-by-generation-and-guest.md).  
  


