---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: Grundlegendes zum ADDS-Entwurf
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f46cad23e13edcef57bf00113e601069c02cfd4f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402459"
---
# <a name="understanding-ad-ds-design"></a>Grundlegendes zum ADDS-Entwurf

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Organisationen können Active Directory Domain Services (AD DS) in Windows Server verwenden, um die Benutzer-und Ressourcenverwaltung beim Erstellen skalierbarer, sicherer und verwaltbarer Infrastrukturen zu vereinfachen. Sie können AD DS zum Verwalten Ihrer Netzwerkinfrastruktur verwenden, einschließlich Zweigstelle, Microsoft Exchange Server und Umgebungen mit mehreren Gesamtstrukturen.  
  
Ein AD DS Bereitstellungs Projekt umfasst drei Phasen: eine Entwurfsphase, eine Bereitstellungs Phase und eine Vorgangs Phase. Während der Entwurfsphase erstellt das Entwurfs Team einen Entwurf für die AD DS logische Struktur, die die Anforderungen der einzelnen Abteilungen in der Organisation, die den Verzeichnisdienst verwenden werden, am besten erfüllt. Nachdem der Entwurf genehmigt wurde, testet das Bereitstellungs Team den Entwurf in einer Lab-Umgebung und implementiert dann den Entwurf in der Produktionsumgebung. Da die Tests vom Bereitstellungs Team durchgeführt werden und sich dies möglicherweise auf die Entwurfsphase auswirkt, handelt es sich um eine zwischen Aktivität, die sowohl den Entwurf als auch die Bereitstellung Wenn die Bereitstellung vollständig ist, ist das Betriebsteam für die Verwaltung des Verzeichnis Dienstanbieter verantwortlich.  
  
Obwohl die Windows Server-AD DS Entwurfs-und Bereitstellungs Strategien, die in diesem Handbuch vorgestellt werden, auf umfassenden Testprogrammen und Pilotprogrammen und erfolgreicher Implementierung in Kundenumgebungen basieren, müssen Sie möglicherweise Ihren AD DS Entwurf anpassen. Bereitstellung für eine bessere Anpassung an bestimmte komplexe Umgebungen.
  
- Weitere Informationen zum Bereitstellen von AD DS in einer Zweigstellen Umgebung finden [Sie im Planungs Handbuch für den schreibgeschützten Domänen Controller (RODC)](https://go.microsoft.com/fwlink/?LinkId=100207).  
- Weitere Informationen zum Bereitstellen von AD DS in einer Exchange-Umgebung finden Sie im Artikel [Exchange 2007-Planning Active Directory](https://go.microsoft.com/fwlink/?LinkId=88904).  
- Weitere Informationen zum Bereitstellen von AD DS in einer Umgebung mit mehreren Gesamtstrukturen finden Sie im Artikel Überlegungen zur Gesamtstruktur [in Windows 2000 und Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=88905).  
