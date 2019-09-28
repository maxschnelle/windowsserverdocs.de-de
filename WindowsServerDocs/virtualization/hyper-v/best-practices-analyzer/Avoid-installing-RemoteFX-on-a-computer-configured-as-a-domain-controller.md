---
title: Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 67fd8e2568691b7e9be4b46e30b64bf44558d6d0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366467"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Vermeiden Sie die Installation von remotefx auf einem Computer, der als Active Directory Domänen Controller konfiguriert ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Remotefx ist auf einem Domänen Controller installiert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Für remotefx konfigurierte virtuelle Computer können auf diesen Computern nicht verwendet werden.*  
  
## <a name="resolution"></a>**Auflösung**  
*Entscheiden Sie, ob dieser Server entweder mit remotefx für Hyper-V oder als Active Directory-Domäne Controller konfiguriert werden soll, und konfigurieren Sie den Server bei Bedarf neu.*  
  


