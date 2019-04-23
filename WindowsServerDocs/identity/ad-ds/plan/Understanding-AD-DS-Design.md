---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: Grundlegendes zum ADDS-Entwurf
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c94f6ddd19e3178243545b0cc71f6f4c7bb4dbec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828791"
---
# <a name="understanding-ad-ds-design"></a>Grundlegendes zum ADDS-Entwurf

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Organisationen können Active Directory Domain Services (AD DS) in Windows Server verwenden, um Benutzer und ressourcenverwaltung zu vereinfachen, während der Erstellung der skalierbare, sichere und verwaltbare Infrastruktur. Sie können AD DS verwenden, Ihre Netzwerkinfrastruktur einschließlich Branch Office, Microsoft Exchange Server und Umgebungen mit mehreren Gesamtstrukturen verwalten.  
  
Ein AD DS-Bereitstellungsprojekt besteht aus drei Phasen: einer Entwurfsphase, einer Bereitstellungsphase und einer Einsatzphase. Während der Entwurfsphase erstellt das Designteam ein Design für die logischen AD DS-Struktur, die die Anforderungen der einzelnen Abteilungen in der Organisation am besten, die den Verzeichnisdienst verwendet werden. Nachdem das Design gebilligt wurde, wird das Bereitstellungsteam das Design in einer testumgebung getestet und implementiert das Design anschließend in der produktionsumgebung. Da Tests durch das Bereitstellungsteam durchgeführt wird, und sie potenziell wirkt sich auf der Entwurfsphase, ist es ein Zwischenschritt, der Entwurf und der Bereitstellung überschneidet. Wenn die Bereitstellung abgeschlossen ist, ist das Betriebsteam für die Wartung des Verzeichnisdiensts verantwortlich.  
  
Obwohl die Windows Server AD DS-Entwurf und Bereitstellung von Strategien, die in diesem Handbuch angezeigt werden, die sich auf die umfangreichen und Tests und erfolgreiche Implementierung in kundenumgebungen basieren, müssen Sie möglicherweise Ihren AD DS-Entwurf anpassen und Bereitstellung besser spezifische, komplexe Umgebungen entsprechend anpassen.
  
- Weitere Informationen zum Bereitstellen von AD DS in einer Umgebung mit unternehmensniederlassungen finden Sie unter den [Read-Only-Domänencontroller (RODC) Branch Office Planning Guide](https://go.microsoft.com/fwlink/?LinkId=100207).  
- Weitere Informationen zum Bereitstellen von AD DS in einer Exchange-Umgebung finden Sie im Artikel [Exchange 2007 - Planen von Active Directory](https://go.microsoft.com/fwlink/?LinkId=88904).  
- Weitere Informationen zum Bereitstellen von AD DS in einer Umgebung mit mehreren Gesamtstrukturen finden Sie im Artikel [Multiple Forest Considerations in Windows 2000 und Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=88905).  
