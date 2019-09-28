---
title: Schritt 2 Planen von Cluster Servern
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 673c5bfb-b590-4932-8e54-ca0a466d90cc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 17aadbb789052be7f33822ce49f3b797f2211d55
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367379"
---
# <a name="step-2-plan-cluster-servers"></a>Schritt 2 Planen von Cluster Servern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Planen Sie nach der Bereitstellung eines einzelnen RAS-Servers zusätzliche Server zum Cluster hinzu.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[2,1 Installieren von Rollen und Features](#BKMK_Install).|Planen Sie für jeden Server, der dem Cluster hinzugefügt werden soll, die Installation der Remote Zugriffs Rolle und des Windows-NLB-Features (falls erforderlich), planen Sie die Topologie, die IP-Adressierung, das Routing und die Weiterleitung.|  
|[2,2 Konfigurieren von Servereinstellungen](#BKMK_Config)|Konfigurieren Sie die Einstellungen für jeden Server, der dem Cluster hinzugefügt wird. Beachten Sie, dass Sie einen Server Cluster mit Lastenausgleich mithilfe von virtuellen Computern konfigurieren können. Damit Routing und Konnektivität ordnungsgemäß funktionieren, müssen Sie die virtuellen Computer so konfigurieren, dass Sie das Spoofing von Mac-Adressen verwenden.|  
  
## <a name="BKMK_Install"></a>2,1 Installieren von Rollen und Features  
Planen Sie die Installation der Remote Zugriffs Rolle für jeden Server, den Sie dem Cluster hinzufügen möchten. Planen Sie zusätzlich die Installation des Netzwerk Lastenausgleichs (Network Load Balancing, NLB), wenn Sie einen Lastenausgleich für den Datenverkehr mithilfe von Windows NLB zum Cluster ausführen möchten. Weitere Informationen finden Sie unter [Netzwerk Lastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  
  
## <a name="BKMK_Config"></a>2,2 Konfigurieren von Servereinstellungen  
Planen Sie die IP-Adresse und die Domänen Einstellungen für jeden Server, der dem Cluster hinzugefügt wird. Beachten Sie Folgendes:  
  
1.  Die Server im Cluster müssen alle derselben Domäne angehören.  
  
2.  Die Server im Cluster müssen sich im selben Subnetz befinden.  
  
3.  Jeder Server im Cluster muss die gleiche Anzahl von Netzwerkadaptern aufweisen, die für die DirectAccess-Bereitstellung verwendet werden.  
  
Wenn Sie einen Lastenausgleich für den Cluster mithilfe von Windows NLB durchgeführt haben, werden die folgenden Windows NLB-Einstellungen angewendet:  
  
1.  Vorgangs Modus-Unicast. Dies kann mit dem NLB-Manager in Multicast geändert werden. Diese Einstellung kann in der Remote Zugriffs-Verwaltungskonsole nicht geändert werden.  
  
2.  Lastfaktor ist als gleichwertig definiert, wobei alle Cluster Server über eine gleichmäßige Auslastung verfügen.  
  
3.  Filter Modus: für den Datenverkehr wird ein Lastenausgleich über mehrere Hosts ausgeführt.  
  
4.  Affinität: einzelne Affinität ist definiert.  
  
5.  Protokolle: beides  

