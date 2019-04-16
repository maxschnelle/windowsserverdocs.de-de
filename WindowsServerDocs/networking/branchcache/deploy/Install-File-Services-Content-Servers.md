---
title: Installieren von Dateidienst-Inhaltsservern
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7036323e7cc31bd14be8025b6064a806fb45ef19
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-file-services-content-servers"></a>Installieren von Dateidienst-Inhaltsservern

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Um Inhaltsserver bereitstellen, die die Serverrolle Dateidienste ausgeführt werden, müssen Sie den Rollendienst BranchCache für Netzwerk Dateien der Serverrolle Dateidienste installieren. Darüber hinaus müssen Sie entsprechend Ihren Anforderungen BranchCache auf Dateifreigaben aktivieren.  
  
Während der Konfiguration des Inhaltsservers können Sie BranchCache-Veröffentlichung von Inhalten für alle Dateifreigaben zulassen, oder Sie können eine Teilmenge von Dateifreigaben zur Veröffentlichung auswählen.  
  
> [!NOTE]  
> Wenn Sie einen BranchCache-fähigen Dateiservers oder Webservers als Inhaltsserver bereitstellen, wird Inhaltsinformationen jetzt offline, berechnet, bevor ein BranchCache-Client eine Datei anfordert. Aufgrund dieser Verbesserung müssen Sie keine hashveröffentlichung für Inhaltsserver konfigurieren, wie in der vorherigen Version von BranchCache.  
>   
> Diese automatische Hash Generation bietet bessere Leistung und mehr bandbreiteneinsparungen, weil Inhaltsinformationen für den ersten Client bereit ist, der Inhalt anfordert, und Berechnungen bereits durchgeführt wurden.  
  
Finden Sie unter den folgenden Themen Inhaltsserver bereitstellen.  
  
-   [Konfigurieren der Dateidienst-Serverrolle](../../branchcache/deploy/Configure-the-File-Services-server-role.md)  
  
-   [Aktivieren von Hashveröffentlichung für Dateiserver](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)  
  
-   [Aktivieren von BranchCache auf einer Dateifreigabe & #40; Optional & #41;](../../branchcache/deploy/enable-bc-on-file-share.md)  
  


