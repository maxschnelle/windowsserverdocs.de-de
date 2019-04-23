---
ms.assetid: f6e76ef0-2217-4cdb-980f-22a780a85ebb
title: AD DS-Entwurfsanforderungen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 79c694112f39adf5d37cd28f6bd7a770dedf3976
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857521"
---
# <a name="ad-ds-design-requirements"></a>AD DS-Entwurfsanforderungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
## <a name="designing-the-active-directory-logical-structure"></a>Entwerfen der logischen Struktur von Active Directory  
Bevor Sie Windows Server 2008 Active Directory Domain Services (AD DS) bereitstellen, müssen Sie planen und entwerfen die logische AD DS-Struktur für Ihre Umgebung. Die logische Struktur von AD DS bestimmt, wie Ihre Verzeichnisobjekte organisiert sind, und bietet eine effektive Methode zum Verwalten Ihrer Netzwerkkonten und freigegebener Ressourcen. Beim Entwerfen der logischen Struktur der AD DS, definieren Sie ein Großteil der Netzwerkinfrastruktur Ihrer Organisation.  
  
Informationen zum Entwerfen der logischen AD DS-Struktur bestimmt die Anzahl der Gesamtstrukturen, die Ihre Organisation erforderlich sind, und erstellen Sie dann Designs für Domänen, Organisationseinheiten (OUs) und Domain Name System (DNS)-Infrastruktur. Die folgende Abbildung zeigt den Prozess zum Entwerfen der logischen Struktur.  
  
![AD DS-entwurfsanforderungen](media/AD-DS-Design-Requirements/d5cebae6-a752-4063-a98f-473799c251bd.gif)  
  
Weitere Informationen finden Sie unter [Entwerfen der logischen Struktur für Windows Server 2008 AD DS](Designing-the-Logical-Structure.md).  
  
## <a name="designing-the-site-topology"></a>Entwerfen der Standorttopologie  
Nachdem Sie die logische Struktur für die AD DS-Infrastruktur entworfen haben, müssen Sie die Standorttopologie für Ihr Netzwerk entwerfen. Die Standorttopologie ist eine logische Darstellung Ihres physischen Netzwerks. Es enthält Informationen über den Speicherort der AD DS-Standorten, die AD DS-Domänencontroller in jedem Standort und die standortverknüpfungen und Standortverknüpfungsbrücken, die AD DS-Replikation zwischen Standorten zu unterstützen. Die folgende Abbildung zeigt den Entwurfsprozess der Standorttopologie.  
  
![AD DS-entwurfsanforderungen](media/AD-DS-Design-Requirements/d34d43c0-437f-47cb-9b64-09c0f9ce6479.gif)  
  
Weitere Informationen finden Sie unter [entwerfen die Website-Topologie für Windows Server 2008 AD DS](Designing-the-Site-Topology.md).  
  
## <a name="planning-domain-controller-capacity"></a>Planen der Domänencontrollerkapazität  
Um effiziente AD DS-Leistung zu gewährleisten, müssen die passende Anzahl von Domänencontrollern für jeden Standort und stellen Sie sicher, dass sie die hardwareanforderungen für Windows Server 2008 entsprechen. Eine sorgfältige Planen der Kapazität für Ihre Domänencontroller wird sichergestellt, dass Sie nicht die hardwareanforderungen unterschätzen, die was zu schlechter Leistung und Antwortzeit des Domänencontrollers führen kann. Die folgende Abbildung zeigt den Prozess der Planung der Domänencontrollerkapazität.  
  
![AD DS-entwurfsanforderungen](media/AD-DS-Design-Requirements/fff6ef22-5c7b-4478-ad76-42b296dcf769.gif)  
  
## <a name="enabling-windows-server-2008-advanced-ad-ds-features"></a>Aktivieren von Windows Server 2008, erweiterte AD DS-features  
Sie können Windows Server 2008 AD DS verwenden, um erweiterte Funktionen in Ihrer Umgebung einzuführen, durch Anheben der Funktionsebene der Domäne oder Gesamtstruktur. Sie können die Domänenfunktionsebene auf Windows Server 2008 auslösen, wenn alle Domänencontroller in der Domäne oder Gesamtstruktur Windows Server 2008 ausgeführt werden.  
  
Weitere Informationen finden Sie unter [aktivieren erweiterte Funktionen für AD DS](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md).  
  


