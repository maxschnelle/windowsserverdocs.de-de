---
title: Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 174e83c950d2aff8afba4f05641a74861b9a7938
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865461"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie Active Directory Domain Services (AD DS) verwenden, können Sie die Gruppenrichtlinie auf Domänenebene verwenden, um BranchCache-hashveröffentlichung für mehrere Server zu aktivieren. In diesem Fall müssen Sie eine Organisationseinheit (OU), Erstellen der Organisationseinheit Dateiserver hinzufügen, erstellen Sie einen BranchCache-hashveröffentlichung (Group Policy Object, GPO) und dann konfigurieren Sie das Gruppenrichtlinienobjekt.  
  
Finden Sie unter den folgenden Themen zum Aktivieren von hashveröffentlichung für mehrere Server.  
  
-   [Erstellen der BranchCache-Dateiserver-Organisationseinheit](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [Verschieben Sie Dateiserver, die BranchCache-Dateiserver-Organisationseinheit](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [Erstellen der BranchCache-Hash Gruppenrichtlinienobjekts](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  
-   [Konfigurieren Sie die BranchCache-Hash Gruppenrichtlinienobjekts](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  


