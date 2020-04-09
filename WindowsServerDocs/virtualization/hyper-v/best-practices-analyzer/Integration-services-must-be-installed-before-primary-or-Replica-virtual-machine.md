---
title: Integration Services muss installiert werden, bevor primäre oder virtuelle Replikat Computer nach einem Failover eine Alternative IP-Adresse verwenden können.
description: Online Version des Texts für diese Best Practices Analyzer Regel mit Links zu weiteren Informationen.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a7fdd185-d6c8-4f58-9b58-2df5827bb056
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: d532d58d21b39963b41de969d83b720ed077e9c7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861903"
---
# <a name="integration-services-must-be-installed-before-primary-or-replica-virtual-machines-can-use-an-alternate-ip-address-after-a-failover"></a>Integration Services muss installiert werden, bevor primäre oder virtuelle Replikat Computer nach einem Failover eine Alternative IP-Adresse verwenden können.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Virtuelle Computer, die an der Replikation teilnehmen, können so konfiguriert werden, dass bei einem Failover eine bestimmte IP-Adresse verwendet wird, jedoch nur, wenn Integrationsdienste im Gast Betriebssystem des virtuellen Computers installiert sind.*  
  
## <a name="impact"></a>Auswirkungen  
*Im Falle eines Failovers (geplant, nicht geplant oder testen) wird der virtuelle Replikat Computer mit der gleichen IP-Adresse wie der primäre virtuelle Computer online geschaltet. Diese Konfiguration kann Verbindungsprobleme verursachen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie die Verbindung mit dem virtuellen Computer, um Integration Services auf dem virtuellen Computer zu installieren.*  
  
Ab Windows Server 2016 werden die Integrationsdienste für virtuelle Windows-Computer über Windows Update bereitgestellt. Stellen Sie sicher, dass diese virtuellen Computer für den Empfang von Windows-Updates konfiguriert sind, um die neueste Version von Integration Services zu erhalten Der Linux-Kernel enthält jetzt Linux-Integrationsdienste (LIS) und wird für neue Releases aktualisiert, aber Linux-Distributionen, die auf älteren Kernel basieren, verfügen möglicherweise nicht über die neuesten Verbesserungen oder Korrekturen. Weitere Informationen finden Sie [unter Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md).


