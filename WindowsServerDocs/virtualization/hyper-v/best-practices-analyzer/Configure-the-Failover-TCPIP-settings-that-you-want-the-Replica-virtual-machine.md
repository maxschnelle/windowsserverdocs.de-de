---
title: Konfigurieren Sie die TCP/IP-Einstellungen, die Sie mit den replizierten virtuellen Computer im Falle eines Failovers verwenden möchten
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c16fbc95c9d679611d57327992a6621d58d4e201
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855751"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>Konfigurieren Sie die TCP/IP-Einstellungen, die Sie mit den replizierten virtuellen Computer im Falle eines Failovers verwenden möchten

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
*Virtuelle replikatcomputer, die mit einer statischen IP-Adresse konfiguriert sollten konfiguriert werden, um eine andere IP-Adresse in ihre Gegenstücke primären virtuellen Computer bei einem Failover zu verwenden.*  
  
## <a name="impact"></a>Auswirkungen  
*Mithilfe der Workload, die von den primären virtuellen Computer unterstützt werden Clients möglicherweise keine Verbindung mit der virtuelle replikatcomputer nach einem Failover. Darüber hinaus ist der primäre virtuelle Computer in der ursprüngliche IP-Adresse nicht in der Replikat-VM-Netzwerktopologie gültig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie Hyper-V-Manager, um die IP-Adresse konfigurieren, die bei einem Failover der Replikat-VM verwenden soll.*  
  


