---
title: Installieren von Dateidienst-Inhaltsservern
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c55f8df57ed98d13d6d0d6d2a281edfb55883bea
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356562"
---
# <a name="install-file-services-content-servers"></a>Installieren von Dateidienst-Inhaltsservern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Zum Bereitstellen von Inhaltsservern, die die Serverrolle Dateidienste ausführen, müssen Sie den BranchCache-Rollendienst für Netzwerkdateien der Serverrolle Dateidienste installieren. Außerdem müssen Sie BranchCache auf Dateifreigaben entsprechend Ihren Anforderungen aktivieren.  
  
Während der Konfiguration des Inhaltsservers können Sie BranchCache-Inhaltsveröffentlichung für alle Dateifreigaben zulassen, oder Sie können eine Teilmenge von Dateifreigaben zur Veröffentlichung auswählen.  
  
> [!NOTE]  
> Beim Bereitstellen eines BranchCache-fähigen Dateiservers oder Webservers als Inhalts Server werden die Inhaltsinformationen jetzt offline berechnet, bevor ein BranchCache-Client eine Datei anfordert. Aufgrund dieser Verbesserung müssen Sie die Hash Veröffentlichung für Inhalts Server nicht wie in der vorherigen Version von BranchCache konfigurieren.  
>   
> Diese automatische Hash Generierung sorgt für eine schnellere Leistung und mehr Bandbreiten Einsparungen, da Inhaltsinformationen für den ersten Client bereit sind, der den Inhalt anfordert, und Berechnungen bereits durchgeführt wurden.  
  
Weitere Informationen zur Bereitstellung von Inhaltsservern finden Sie in den folgenden Themen.  
  
-   [Konfigurieren der Dateidienst-Serverrolle](../../branchcache/deploy/Configure-the-File-Services-server-role.md)  
  
-   [Aktivieren der Hash Veröffentlichung für Dateiserver](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)  
  
-   [Aktivieren von BranchCache auf einer Datei &#40;Freigabe optional&#41;](../../branchcache/deploy/enable-bc-on-file-share.md)  
  


