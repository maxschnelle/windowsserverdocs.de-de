---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: Benennung von Computern
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d0dbe2da76a1cf3d1a4dd74183b5dd7106ef17b9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="computer-naming"></a>Benennung von Computern

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn ein Computer, auf denen das Betriebssystem Windows2000, Windows XP, Windows Server2003, Windows Server2008 oder Windows Vista Beitritt weist eine Domäne wird standardmäßig der Computer sich selbst einen Namen. Der Name selbst weist besteht aus den Hostnamen des Computers (d.h. Computername in den Systemeigenschaften) und den Domain Name System (DNS)-Namen des Active Directory-Domäne, die der Computer Mitglied (d.h. primären DNS-Suffix in den Systemeigenschaften). Die Verkettung von den Hostnamen und den DNS-Namen der Domäne wird als den vollständig qualifizierten Domänennamen (FQDN) bezeichnet. Wenn ein Computer mit Hostnamen Server1 corp.contoso.com der Domäne beitritt, wird der FQDN des Computers beispielsweise server1.corp.contoso.com.  
  
Verfügt ein Computer bereits einen anderen DNS-Domänennamen, der statisch in einer DNS-Zone eingegeben oder durch ein integrierter DNS/Dynamic Host Configuration Protocol (DHCP) Serverdienst registriert wurde, ist der FQDN des Computers von der Name, der bereits registriert wurde. Der Computer kann entweder Namen verwiesen werden.  
  
Weitere Informationen zu Namenskonventionen in Active Directory-Domänendienste (AD DS), finden Sie unter Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten ([https://go.microsoft.com/fwlink/?LinkID=106629](https://go.microsoft.com/fwlink/?LinkID=106629)).  
  


