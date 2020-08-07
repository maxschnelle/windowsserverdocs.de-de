---
title: Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: df03945a80ae86aad91a004ea710ac6eff10c3ad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971857"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>Aktivieren der Hashveröffentlichung für Dateiserver in der Domäne

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie Active Directory Domain Services (AD DS) verwenden, können Sie Domänen Gruppenrichtlinie verwenden, um die BranchCache-Hash Veröffentlichung für mehrere Dateiserver zu aktivieren. Hierzu müssen Sie eine Organisationseinheit (OU) erstellen, der Organisationseinheit Dateiserver hinzufügen, ein BranchCache-Hash Veröffentlichungs Gruppenrichtlinie Objekt (GPO) erstellen und dann das Gruppenrichtlinien Objekt konfigurieren.

Weitere Informationen zum Aktivieren der Hash Veröffentlichung für mehrere Dateiserver finden Sie in den folgenden Themen.

-   [Erstellen der BranchCache-Dateiserver-Organisationseinheit](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Verschieben von Dateiservern in die Organisationseinheit mit den BranchCache-Dateiservern](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Erstellen des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)

-   [Konfigurieren des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)



