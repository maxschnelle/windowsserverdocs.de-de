---
title: Integrationsservices installiert werden müssen, vor dem primären können Replikat-VMs auch eine alternative IP-Adresse nach einem failover
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel, mit Links zu weiteren Informationen.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a7fdd185-d6c8-4f58-9b58-2df5827bb056
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 1ff8dbfd71655aee86ba7d0feac87ec2267a2171
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865511"
---
# <a name="integration-services-must-be-installed-before-primary-or-replica-virtual-machines-can-use-an-alternate-ip-address-after-a-failover"></a>Integrationsservices installiert werden müssen, vor dem primären können Replikat-VMs auch eine alternative IP-Adresse nach einem failover

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*So, dass eine bestimmte IP-Adresse bei Failover, aber nur, wenn Integrationsdienste im Gastbetriebssystem, das der virtuellen Maschine installiert sind, können virtuelle Computer, die bei der Replikation beteiligt sein.*  
  
## <a name="impact"></a>Auswirkungen  
*Im Fall eines Failovers (geplant, ungeplant oder test) wird der replizierte virtuelle Computer online ist, verwenden die IP-Adresse als der primäre virtuelle Computer stehen. Diese Konfiguration kann dazu führen, dass Probleme mit der Netzwerkkonnektivität. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie Verbindung mit virtuellen Computern, um Integrationsservices auf dem virtuellen Computer zu installieren.*  
  
Ab Windows Server 2016 werden die Integrationsdienste für Windows-VMs über Windows Update bereitgestellt. Stellen Sie sicher, dass diese virtuellen Computer konfiguriert sind, um Windows-Updates, rufen Sie die neueste Version von Integrationsservices zu erhalten. Der Linux-Kernel nun enthält Linux-Integrationsdienste (LIS) und wird für neue Versionen aktualisiert, aber der Linux-Distributionen, die basierend auf älteren Kernels möglicherweise nicht die neuesten Verbesserungen oder Updates. Weitere Informationen finden Sie unter [unterstützt Linux und FreeBSD-VMs für Hyper-V unter Windows](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md).


