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
ms.openlocfilehash: 2afc6f87a321625ae693d1a49c56f260a7d8c305
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962242"
---
# <a name="dns-and-ad-ds"></a>DNS und AD DS

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS) verwendet Domain Name System-Namensauflösungsdienste (DNS), damit Clients Domänen Controller suchen können und die Domänen Controller, die den Verzeichnisdienst hosten, miteinander kommunizieren können.

AD DS ermöglicht eine einfache Integration des Active Directory-Namespace in einen vorhandenen DNS-Namespace. Features wie Active Directory integrierte DNS-Zonen erleichtern Ihnen die Bereitstellung von DNS, da Sie keine sekundären Zonen einrichten müssen und dann Zonenübertragungen konfigurieren können.

Informationen dazu, wie AD DS DNS unterstützt, finden Sie im Abschnitt [DNS-Unterstützung für Active Directory Technische Referenz](/previous-versions/windows/it-pro/windows-server-2003/cc781627(v=ws.10)).

> [!NOTE]
> Wenn Sie einen Zusammenhang losen Namespace implementieren, in dem sich der AD DS Domänen Namens vom primären DNS-Suffix unterscheidet, das von Clients verwendet wird, ist AD DS Integration in DNS komplexer. Weitere Informationen finden Sie unter [Disjoint Namespace](Disjoint-Namespace.md).

## <a name="in-this-section"></a>In diesem Abschnitt

- [Domänencontrollersuche](Domain-Controller-Location.md)
- [In Active Directory integrierte DNS-Zonen](Active-Directory-Integrated-DNS-Zones.md)
- [Computerbenennung](Computer-Naming.md)
- [Zusammenhangloser Namespace](Disjoint-Namespace.md)
