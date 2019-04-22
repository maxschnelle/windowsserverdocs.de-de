---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS und AD DS
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f6d75a78119d76a0f8380967292b1d0abc720597
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813141"
---
# <a name="dns-and-ad-ds"></a>DNS und AD DS

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory-Domänendienste (AD DS) verwendet Namensauflösungsdienste Domain Name System (DNS), damit Clients Domänencontroller finden und für die Domänencontroller können diesem Host den Verzeichnisdienst miteinander kommunizieren.  
  
AD DS ermöglicht die einfache Integration von Active Directory-Namespace in eine vorhandene DNS-Namespace. Features wie z. B. Active Directory-integrierte DNS-Zonen einfacher für Sie zum Bereitstellen von DNS durch den Wegfall zum Einrichten von sekundärer Zones und zonenübertragungen konfigurieren.  
  
Informationen zur Unterstützung von AD DS in DNS finden Sie im Abschnitt [DNS-Unterstützung für technische Referenz zu Active Directory](https://go.microsoft.com/fwlink/?LinkID=48147).  
  
> [!NOTE]  
> Wenn Sie einen zusammenhanglosen Namespace implementieren, in dem Namen der AD DS-Domäne aus dem primären DNS-Suffix unterscheidet, die Clients verwenden, ist die AD DS-Integration mit DNS komplexer. Weitere Informationen finden Sie unter [Disjoint Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md).  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
- [Adresse des Domänencontrollers](../../ad-ds/plan/Domain-Controller-Location.md)  
- [Active Directory-integrierte DNS-Zonen](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
- [Benennen Computer](../../ad-ds/plan/Computer-Naming.md)  
- [Zusammenhangloser Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
