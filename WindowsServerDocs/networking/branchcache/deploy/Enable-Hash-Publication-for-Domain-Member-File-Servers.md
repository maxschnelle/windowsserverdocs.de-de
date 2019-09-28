---
title: Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1e450b9a2282cb4820b8802aa6d36e822f56ca12
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356594"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie Active Directory Domain Services (AD DS) verwenden, können Sie Domänen Gruppenrichtlinie verwenden, um die BranchCache-Hash Veröffentlichung für mehrere Dateiserver zu aktivieren. Hierzu müssen Sie eine Organisationseinheit (OU) erstellen, der Organisationseinheit Dateiserver hinzufügen, ein BranchCache-Hash Veröffentlichungs Gruppenrichtlinie Objekt (GPO) erstellen und dann das Gruppenrichtlinien Objekt konfigurieren.  
  
Weitere Informationen zum Aktivieren der Hash Veröffentlichung für mehrere Dateiserver finden Sie in den folgenden Themen.  
  
-   [Erstellen der BranchCache-Dateiserver-Organisationseinheit](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [Verschieben von Dateiservern in die Organisationseinheit der BranchCache-Dateiserver](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [Erstellen der BranchCache-Hash Veröffentlichung Gruppenrichtlinie-Objekts](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  
-   [Konfigurieren des BranchCache-Hash Veröffentlichungs Gruppenrichtlinie Objekts](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  


