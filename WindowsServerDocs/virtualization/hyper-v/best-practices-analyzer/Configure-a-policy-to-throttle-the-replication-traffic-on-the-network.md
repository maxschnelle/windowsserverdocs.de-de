---
title: Konfigurieren Sie eine Richtlinie zum Einschränken der Replikations-Datenverkehr im Netzwerk
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2c1f1865fa1d611c0b5baaf981140f9807b51458
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818691"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>Konfigurieren Sie eine Richtlinie zum Einschränken der Replikations-Datenverkehr im Netzwerk

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
*Gibt es möglicherweise kein Grenzwert für die Menge an Netzwerkbandbreite ist zulässig, dass die Replikation nutzen.*  
  
## <a name="impact"></a>Auswirkungen  
*Die Netzwerkbandbreite kann vollständig von Replikationsdatenverkehr, Auswirkungen auf andere kritische Netzwerkaktivität beherrscht werden. Dies wirkt sich die folgenden Ports:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Wenn Sie eine andere Methode zum Einschränken des Netzwerkdatenverkehrs verwenden, können Sie dies ignorieren. Verwenden Sie andernfalls die Gruppenrichtlinien-Editor zum Konfigurieren einer Richtlinie, die den Netzwerkdatenverkehr auf diesen Port des Replikatservers einschränkt.*  
  
  


