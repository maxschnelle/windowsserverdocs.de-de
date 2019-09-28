---
title: Konfigurieren virtueller Computer für die Verwendung von SR-IOV nur, wenn diese vom Gast Betriebssystem unterstützt werden
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 33cf5b68-e43e-47ef-adbc-6b266c1d4dce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8c43e06806f66ce0faae255f0f34d80a653fbe10
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366257"
---
# <a name="configure-virtual-machines-to-use-sr-iov-only-when-supported-by-the-guest-operating-system"></a>Konfigurieren virtueller Computer für die Verwendung von SR-IOV nur, wenn diese vom Gast Betriebssystem unterstützt werden

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Mindestens ein virtueller Computer ist für die Verwendung von SR-IOV (Single-root I/O Virtualization) konfiguriert, aber das Gast Betriebssystem unterstützt SR-IOV nicht.*  
  
## <a name="impact"></a>Auswirkungen  
*Die virtuellen SR-IOV-Funktionen werden den folgenden virtuellen Computern nicht zugeordnet:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*Deaktivieren Sie SR-IOV auf allen virtuellen Computern, auf denen Gast Betriebssysteme ausgeführt werden, die SR-IOV nicht unterstützen.*  
  
SR-IOV wird nur in einigen 64-Bit-Windows-Gastbetriebssystemen unterstützt. Weitere Informationen finden Sie unter [Hyper-V-Funktions Kompatibilität nach Generierung und Gast](../Hyper-V-feature-compatibility-by-generation-and-guest.md).  
  


