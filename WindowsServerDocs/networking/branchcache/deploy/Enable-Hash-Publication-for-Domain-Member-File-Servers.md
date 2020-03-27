---
title: Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: dd39a8d7f08e3ac3e6249017a042c343d9179566
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319287"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Wenn Sie Active Directory Domain Services (AD DS) verwenden, können Sie Domänen Gruppenrichtlinie verwenden, um die BranchCache-Hash Veröffentlichung für mehrere Dateiserver zu aktivieren. Hierzu müssen Sie eine Organisationseinheit (OU) erstellen, der Organisationseinheit Dateiserver hinzufügen, ein BranchCache-Hash Veröffentlichungs Gruppenrichtlinie Objekt (GPO) erstellen und dann das Gruppenrichtlinien Objekt konfigurieren.  
  
Weitere Informationen zum Aktivieren der Hash Veröffentlichung für mehrere Dateiserver finden Sie in den folgenden Themen.  
  
-   [Erstellen der BranchCache-Dateiserver-Organisationseinheit](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [Verschieben von Dateiservern in die Organisationseinheit der BranchCache-Dateiserver](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [Erstellen der BranchCache-Hash Veröffentlichung Gruppenrichtlinie-Objekts](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  
-   [Konfigurieren des BranchCache-Hash Veröffentlichungs Gruppenrichtlinie Objekts](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  


