---
title: Schritt 2 Planen von Clusterservern
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 673c5bfb-b590-4932-8e54-ca0a466d90cc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0dcb14a03f02f931d59743f1b1b8b24b84ba8351
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282858"
---
# <a name="step-2-plan-cluster-servers"></a>Schritt 2 Planen von Clusterservern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nach dem Bereitstellen eines einzelnen Remotezugriffsservers können zusätzliche Server mit dem Cluster hinzufügen möchten.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[2.1 Installieren von Rollen und Features](#BKMK_Install).|Planen Sie der Installation der Rolle "Remotezugriff" und die Windows-NLB-Funktion (falls erforderlich), Planen Sie die Topologie, IP-Adressierung, routing und Weiterleitung, für jeden Server, die mit dem Cluster hinzugefügt werden.|  
|[2.2 Konfigurieren der servereinstellungen](#BKMK_Config)|Konfigurieren Sie Einstellungen für jeden Server, die mit dem Cluster hinzugefügt werden. Beachten Sie, dass Sie eine Load-Clusters mit Lastenausgleich von Servern, die mithilfe von virtuellen Computern konfigurieren können. In der Reihenfolge für routingfähigkeit und Konnektivität ordnungsgemäß funktioniert müssen Sie die virtuellen Computer als verwenden Sie das Spoofing von MAC-Adressen konfigurieren.|  
  
## <a name="BKMK_Install"></a>2.1 Installieren von Rollen und features  
Planen Sie für jeden Server, die Sie mit dem Cluster beitreten möchten, installieren Sie die Rolle "Remotezugriff". Planen Sie außerdem das Feature Netzwerklastenausgleich (Network Load Balancing, NLB) installieren, sollten Sie den Lastenausgleich des Datenverkehrs an den Cluster mithilfe des Windows-Netzwerklastenausgleichs. Weitere Informationen finden Sie unter [Netzwerklastenausgleich](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  
  
## <a name="BKMK_Config"></a>2.2 Konfigurieren der servereinstellungen  
Planen Sie IP-Adressen und Domänen-Einstellungen für jeden Server, die mit dem Cluster hinzugefügt werden. Beachten Sie Folgendes:  
  
1.  Server im Cluster müssen alle derselben Domäne gehören.  
  
2.  Server im Cluster müssen sich im gleichen Subnetz befinden.  
  
3.  Jeder Server im Cluster sollte die gleiche Anzahl von Netzwerkadaptern für den DirectAccess-Bereitstellung verwendet haben.  
  
Wenn Sie für den Cluster mit Windows NLB laden gelten die folgenden Windows-NLB-Einstellungen:  
  
1.  Unicast--Vorgang-Modus. Dies kann zu Multicastadressen, die mit dem NLB-Manager geändert werden. Diese Einstellung kann nicht in der Remotezugriffs-Verwaltungskonsole geändert werden.  
  
2.  Lastgewicht Faktor als gleich ist, definiert, in denen alle Clusterserver Last verfügen.  
  
3.  Filtern von Datenverkehr im wird auf mehreren Hosts mit Lastenausgleich werden.  
  
4.  Affinität – einzelne Affinität definiert ist.  
  
5.  Protocols-Both  

