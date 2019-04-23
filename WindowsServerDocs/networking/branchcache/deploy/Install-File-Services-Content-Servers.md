---
title: Installieren von Dateidienst-Inhaltsservern
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 496c0c1408c64216f29a31d5b22d3d9b48d4f44c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855061"
---
# <a name="install-file-services-content-servers"></a>Installieren von Dateidienst-Inhaltsservern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Zum Bereitstellen von Inhaltsservern, die die Serverrolle Dateidienste ausführen, müssen Sie den BranchCache-Rollendienst für Netzwerkdateien der Serverrolle Dateidienste installieren. Darüber hinaus müssen Sie entsprechend Ihren Anforderungen BranchCache auf Dateifreigaben aktivieren.  
  
Während der Konfiguration des Inhaltsservers können Sie BranchCache-Inhaltsveröffentlichung für alle Dateifreigaben zulassen, oder Sie können eine Teilmenge von Dateifreigaben zur Veröffentlichung auswählen.  
  
> [!NOTE]  
> Wenn Sie einen BranchCache-fähigen Dateiservers oder Webservers als Inhaltsserver bereitstellen, wird Inhaltsinformationen jetzt offline berechnet, bevor eine Datei von einem BranchCache-Client angefordert. Aufgrund dieser Verbesserung müssen Sie keine hashveröffentlichung für Inhaltsserver konfigurieren, wie in der vorherigen Version von BranchCache.  
>   
> Diese automatische Hashgenerierung für bietet bessere Leistung und mehr bandbreiteneinsparungen, weil Inhaltsinformationen für den ersten Client bereit ist, der Inhalt anfordert, und Berechnungen bereits durchgeführt wurden.  
  
Weitere Informationen zur Bereitstellung von Inhaltsservern finden Sie in den folgenden Themen.  
  
-   [Konfigurieren Sie die Serverrolle "Dateidienste"](../../branchcache/deploy/Configure-the-File-Services-server-role.md)  
  
-   [Aktivieren von Hashveröffentlichung für Dateiserver](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)  
  
-   [Aktivieren von BranchCache auf einer Dateifreigabe &#40;Optional&#41;](../../branchcache/deploy/enable-bc-on-file-share.md)  
  


