---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: Computerbenennung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ae2483571d67b4cdb32c2a547b924b1315573da0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842161"
---
# <a name="computer-naming"></a>Computerbenennung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn ein Computer, auf denen das Betriebssystem Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 oder Windows Vista Beitritt weist eine Domäne wird standardmäßig der Computer sich selbst einen Namen. Der Name selbst weist besteht aus den Hostnamen des Computers (d. h. Computernamen in den Systemeigenschaften) und der Domain Name System (DNS) Name des Active Directory-Domäne, die der Computer hinzugefügt (d. h. primäre DNS-Suffix in den Systemeigenschaften). Der vollqualifizierte Domänenname (FQDN) wird die Verkettung von den Hostnamen und den DNS-Namen der Domäne genannt. Wenn ein Computer mit Host Server1 Joins der Domäne "corp.contoso.com" Namen verwenden, ist der FQDN des Computers, z. B. server1.corp.contoso.com.  
  
Wenn ein Computer bereits einen anderen DNS-Domänennamen, der statisch in einer DNS-Zone eingegeben oder von einem integrierten DNS/Dynamic Host Configuration Protocol (DHCP) Serverdienst registriert wurde verfügt, unterscheidet sich der FQDN des Computers nicht mit dem Namen, der registriert wurde zuvor. Der Computer kann entweder über Namen verwiesen werden.  
  
Weitere Informationen zu Namenskonventionen in Active Directory Domain Services (AD DS), finden Sie unter Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten ([https://go.microsoft.com/fwlink/?LinkID=106629](https://go.microsoft.com/fwlink/?LinkID=106629)).  
  


