---
ms.assetid: f6e76ef0-2217-4cdb-980f-22a780a85ebb
title: AD DS-Entwurfsanforderungen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 17338cd00fecec098865095dd9613f62beb3a457
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="ad-ds-design-requirements"></a>AD DS-Entwurfsanforderungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

  
## <a name="designing-the-active-directory-logical-structure"></a>Entwerfen der logischen Active Directory-Struktur  
Bevor Sie Windows Server2008 Active Directory-Domänendienste (AD DS) bereitstellen, müssen Sie planen und entwerfen die logische AD DS-Struktur für Ihre Umgebung. Die logische Struktur der AD DS wird bestimmt, wie Ihre Verzeichnisobjekte organisiert werden, und bietet eine effektive Methode zum Verwalten Ihrer Konten für Netzwerkbenutzer und freigegebene Ressourcen. Beim Entwerfen der logischen Struktur von AD DS definieren Sie einen bedeutenden Teil der Netzwerkinfrastruktur Ihrer Organisation.  
  
Klicken Sie zum Entwerfen der logischen Struktur von AD DS Bestimmen der Anzahl von Gesamtstrukturen, die Ihre Organisation erforderlich ist, und erstellen Sie Designs für Domänen, Domain Name System (DNS)-Infrastruktur und Organisationseinheiten (OUs). Die folgende Abbildungzeigt den Prozess zum Entwerfen der logischen Struktur.  
  
![AD DS-entwurfsanforderungen](media/AD-DS-Design-Requirements/d5cebae6-a752-4063-a98f-473799c251bd.gif)  
  
Weitere Informationen finden Sie unter [Entwerfen der logischen Struktur für Windows Server2008 AD DS](Designing-the-Logical-Structure.md).  
  
## <a name="designing-the-site-topology"></a>Entwerfen der Standorttopologie  
Nachdem Sie die logische Struktur für die AD DS-Infrastruktur entworfen haben, müssen Sie die Standorttopologie für Ihr Netzwerk entwerfen. Die Standorttopologie ist eine logische Darstellung des physischen Netzwerks. Es enthält Informationen über den Speicherort der AD DS-Sites, AD DS-Domänencontroller an jedem Standort sowie Links zu Websites und Standortverknüpfungsbrücken, die AD DS-Replikation zwischen Standorten zu unterstützen. Die folgende Abbildungzeigt den Entwurfsprozess der Standorttopologie.  
  
![AD DS-entwurfsanforderungen](media/AD-DS-Design-Requirements/d34d43c0-437f-47cb-9b64-09c0f9ce6479.gif)  
  
Weitere Informationen finden Sie unter [entwerfen die Website-Topologie für Windows Server2008 AD DS](Designing-the-Site-Topology.md).  
  
## <a name="planning-domain-controller-capacity"></a>Planen der Domänencontrollerkapazität  
Um effizient AD DS-Leistung zu gewährleisten, müssen Sie die entsprechende Anzahl von Domänencontrollern für jeden Standort ermitteln und stellen Sie sicher, dass sie die Hardwareanforderungen für Windows Server2008 erfüllen. Sorgfältige Planung für die Domänencontroller Kapazität wird sichergestellt, dass Sie nicht die Hardwareanforderungen, unterschätzen, die eine schlechte Leistung und Antwortzeit des Domänencontrollers führen können. Die folgende Abbildungzeigt den Prozess der Planung der Domänencontrollerkapazität.  
  
![AD DS-entwurfsanforderungen](media/AD-DS-Design-Requirements/fff6ef22-5c7b-4478-ad76-42b296dcf769.gif)  
  
## <a name="enabling-windows-server-2008-advanced-ad-ds-features"></a>Aktivieren von Windows Server2008 erweiterte AD DS-Features  
Windows Server2008 AD DS können Sie erweiterte Funktionen in Ihrer Umgebung einführen, durch die Funktionsebene der Domäne oder Gesamtstruktur. Sie können die Gesamtstrukturfunktionsebene auf Windows Server2008 auslösen, wenn alle Domänencontroller in der Domäne oder Gesamtstruktur Windows Server2008 ausgeführt werden.  
  
Weitere Informationen finden Sie unter [Aktivieren erweiterter Funktionen für AD DS](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md).  
  


