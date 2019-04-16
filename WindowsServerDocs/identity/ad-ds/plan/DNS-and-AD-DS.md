---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS und AD DS
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8e7ee494c157396a7d58e9fd1b4b80060c4d99fc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="dns-and-ad-ds"></a>DNS und AD DS

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Active Directory-Domänendienste (AD DS) verwendet Domain Name System (DNS)-Namensauflösungsdienste für Clients mit einem Domänencontroller und Domänencontrollern können, dass dieser Host dem Verzeichnisdienst kommunizieren.  
  
AD DS ermöglicht die einfache Integration von Active Directory-Namespace in eine vorhandene DNS-Namespace. Features wie z.B. Active Directory-integrierte DNS-Zonen erleichtern Sie zum Bereitstellen von DNS durch den Wegfall Sekundärzonen einrichten und konfigurieren Sie dann die Übertragung der Zone.  
  
Informationen dazu, wie AD DS von DNS unterstützt, finden Sie unter der DNS-Unterstützung für die technische Referenz zu Active Directory ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147)).  
  
> [!NOTE]  
> Wenn Sie einen separaten Namespace implementieren, der Namen der AD DS-Domäne von das primäre DNS-Suffix unterscheidet, die Clients verwenden, ist die AD DS-Integration in DNS komplexer. Weitere Informationen finden Sie unter [zusammenhanglosen Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Adresse des Domänencontrollers](../../ad-ds/plan/Domain-Controller-Location.md)  
  
-   [Active Directory-integrierte DNS-Zonen](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
  
-   [Benennung von Computern](../../ad-ds/plan/Computer-Naming.md)  
  
-   [Nicht zusammenhängenden Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
  


