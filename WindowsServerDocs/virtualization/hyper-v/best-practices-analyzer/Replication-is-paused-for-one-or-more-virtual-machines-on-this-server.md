---
title: Replikation wird für eine oder mehrere virtuelle Computer auf diesem Server angehalten.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e1119a40-eda3-4058-8648-7df81cbc6c29
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 248b5fbdbfb54380e441d14cde6beaa9146ce800
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827771"
---
# <a name="replication-is-paused-for-one-or-more-virtual-machines-on-this-server"></a>Replikation wird für eine oder mehrere virtuelle Computer auf diesem Server angehalten.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Replikation wird für eine oder mehrere virtuelle Computer angehalten. Während der primäre virtuelle Computer angehalten wird, werden alle Änderungen, die auftreten, werden gesammelt werden und werden an den replizierten virtuellen Computer gesendet werden, nachdem die Replikation fortgesetzt wird.*  
  
## <a name="impact"></a>Auswirkungen  
*Solange die Replikation angehalten wurde, werden die angefallenen Änderungen, die in den primären virtuellen Computer auftreten verfügbarer Speicherplatz auf dem primären Server genutzt. Nachdem die Replikation fortgesetzt wird, gibt es möglicherweise ein großes plötzlichen Ansturms von Netzwerkdatenverkehr an den Replikatserver. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Vergewissern Sie sich, dass die Replikation angehalten vorgesehen war. Wenn zu wenig Speicherplatz oder die Netzwerkkonnektivität Adresse Replikation angehalten wurde, setzen die Replikation fort, sobald diese Probleme behoben wurden.*  
  


