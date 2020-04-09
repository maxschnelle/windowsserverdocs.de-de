---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS und AD DS
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0eaddb6e94011a14b352b813cf508062116001f1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822723"
---
# <a name="dns-and-ad-ds"></a>DNS und AD DS

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS) verwendet Domain Name System-Namensauflösungsdienste (DNS), damit Clients Domänen Controller suchen können und die Domänen Controller, die den Verzeichnisdienst hosten, miteinander kommunizieren können.  
  
AD DS ermöglicht eine einfache Integration des Active Directory-Namespace in einen vorhandenen DNS-Namespace. Features wie Active Directory integrierte DNS-Zonen erleichtern Ihnen die Bereitstellung von DNS, da Sie keine sekundären Zonen einrichten müssen und dann Zonenübertragungen konfigurieren können.  
  
Informationen dazu, wie AD DS DNS unterstützt, finden Sie im Abschnitt [DNS-Unterstützung für Active Directory Technische Referenz](https://go.microsoft.com/fwlink/?LinkID=48147).  
  
> [!NOTE]  
> Wenn Sie einen Zusammenhang losen Namespace implementieren, in dem sich der AD DS Domänen Namens vom primären DNS-Suffix unterscheidet, das von Clients verwendet wird, ist AD DS Integration in DNS komplexer. Weitere Informationen finden Sie unter [Disjoint Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md).  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
- [Domänencontrollersuche](../../ad-ds/plan/Domain-Controller-Location.md)  
- [In Active Directory integrierte DNS-Zonen](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
- [Computerbenennung](../../ad-ds/plan/Computer-Naming.md)  
- [Zusammenhangloser Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
