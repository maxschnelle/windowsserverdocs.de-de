---
title: Zertifikatbasierte Authentifizierung wird für die Replikation empfohlen.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5bd131b48b009b43b6379f72f370b4179dea5a03
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873061"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>Zertifikatbasierte Authentifizierung wird für die Replikation empfohlen.

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
*Eine oder mehrere virtuelle Computer, die für die Replikation ausgewählt werden für die Kerberos-Authentifizierung konfiguriert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Die Replikation des Netzwerkdatenverkehrs vom primären Server mit dem Replikationsserver ist unverschlüsselt. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Wenn eine andere Methode zum Verschlüsseln verwendet wird, können Sie dies ignorieren. Andernfalls ändern Sie die Einstellungen des virtuellen Computers um zertifikatbasierte Authentifizierung zu wählen.*  
  


