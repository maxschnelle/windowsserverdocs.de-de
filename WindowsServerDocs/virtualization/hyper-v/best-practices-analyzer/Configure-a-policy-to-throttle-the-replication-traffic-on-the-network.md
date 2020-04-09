---
title: Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 2c358cd930f2b95412b40aa6c87b0bf9ebb5b741
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862173"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>Konfigurieren einer Richtlinie zur Drosselung des Replikations Datenverkehrs im Netzwerk

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
*Möglicherweise gibt es keine Beschränkung für die Menge an Netzwerkbandbreite, die von der Replikation beansprucht werden darf.*  
  
## <a name="impact"></a>Auswirkungen  
*Die Netzwerkbandbreite könnte vollständig von Replikations Datenverkehr dominiert werden Dies wirkt sich auf die folgenden Ports aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Wenn Sie eine andere Methode zum Einschränken des Netzwerk Datenverkehrs verwenden, können Sie dies ignorieren. Verwenden Sie andernfalls Gruppenrichtlinie-Editor, um eine Richtlinie zu konfigurieren, die den Netzwerk Datenverkehr zum relevanten Port des Replikat Servers drosselt.*  
  
  


