---
title: Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0eac99fddd8bbc6dc585931cd25f2a440be16c76
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365181"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>Die Zertifikat basierte Authentifizierung wird für die Replikation empfohlen.

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
*Mindestens eine für die Replikation ausgewählte virtuelle Maschine ist für die Kerberos-Authentifizierung konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*der Replikations Netzwerk-Datenverkehr vom primären Server zum Replikationsserver ist nicht verschlüsselt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>**Auflösung**  
*wenn eine andere Methode zum Durchführen der Verschlüsselung verwendet wird, können Sie dies ignorieren. Andernfalls ändern Sie die Einstellungen der virtuellen Maschine, um die Zertifikat basierte Authentifizierung auszuwählen.*  
  


