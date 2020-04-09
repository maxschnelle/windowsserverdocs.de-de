---
ms.assetid: f6e76ef0-2217-4cdb-980f-22a780a85ebb
title: AD DS-Entwurfsanforderungen
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e33681088706d60b7d33047d38eb55730725129f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822913"
---
# <a name="ad-ds-design-requirements"></a>AD DS-Entwurfsanforderungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
## <a name="designing-the-active-directory-logical-structure"></a>Entwerfen der logischen Active Directory-Struktur  
Vor der Bereitstellung von Windows Server 2008 Active Directory Domain Services (AD DS) müssen Sie die AD DS logische Struktur für Ihre Umgebung planen und entwerfen. Die AD DS logische Struktur bestimmt, wie Ihre Verzeichnisobjekte organisiert werden, und stellt eine effektive Methode zum Verwalten von Netzwerk Konten und freigegebenen Ressourcen dar. Wenn Sie Ihre AD DS logische Struktur entwerfen, definieren Sie einen wichtigen Teil der Netzwerkinfrastruktur Ihres Unternehmens.  
  
Wenn Sie die AD DS logische Struktur entwerfen möchten, legen Sie die Anzahl der Gesamtstrukturen fest, die für Ihre Organisation erforderlich sind, und erstellen Sie dann Entwürfe für Domänen, Domain Name System (DNS)-Infrastruktur und Organisationseinheiten (OUs). Die folgende Abbildung zeigt den Prozess zum Entwerfen der logischen Struktur.  
  
![AD DS Entwurfs Anforderungen](media/AD-DS-Design-Requirements/d5cebae6-a752-4063-a98f-473799c251bd.gif)  
  
Weitere Informationen finden Sie unter [Entwerfen der logischen Struktur für Windows Server 2008 AD DS](Designing-the-Logical-Structure.md).  
  
## <a name="designing-the-site-topology"></a>Entwerfen der Standort Topologie  
Nachdem Sie die logische Struktur für Ihre AD DS-Infrastruktur entworfen haben, müssen Sie die Standort Topologie für Ihr Netzwerk entwerfen. Bei der Standort Topologie handelt es sich um eine logische Darstellung ihres physischen Netzwerks. Sie enthält Informationen über den Speicherort der AD DS Standorte, die AD DS Domänen Controller an jedem Standort und die Standort Verknüpfungen und Standort Verknüpfungs Brücken, die die AD DS Replikation Zwischenstand Orten unterstützen. Die folgende Abbildung zeigt den Entwurfsprozess der Standort Topologie.  
  
![AD DS Entwurfs Anforderungen](media/AD-DS-Design-Requirements/d34d43c0-437f-47cb-9b64-09c0f9ce6479.gif)  
  
Weitere Informationen finden Sie unter [Entwerfen der Standort Topologie für Windows Server 2008 AD DS](Designing-the-Site-Topology.md).  
  
## <a name="planning-domain-controller-capacity"></a>Planen der Domänen Controller Kapazität  
Um eine effiziente AD DS Leistung zu gewährleisten, müssen Sie die entsprechende Anzahl von Domänen Controllern für jeden Standort ermitteln und überprüfen, ob die Hardwareanforderungen für Windows Server 2008 erfüllt werden. Die sorgfältige Kapazitätsplanung für Ihre Domänen Controller stellt sicher, dass Sie die Hardwareanforderungen nicht unterschätzen, was zu einer unzureichenden Leistung des Domänen Controllers und der Reaktionszeit der Anwendung führen kann Die folgende Abbildung zeigt den Prozess der Kapazitätsplanung des Domänen Controllers.  
  
![AD DS Entwurfs Anforderungen](media/AD-DS-Design-Requirements/fff6ef22-5c7b-4478-ad76-42b296dcf769.gif)  
  
## <a name="enabling-windows-server-2008-advanced-ad-ds-features"></a>Aktivieren von Windows Server 2008-Features für erweiterte AD DS  
Mithilfe von Windows Server 2008 AD DS können Sie erweiterte Features in Ihre Umgebung einführen, indem Sie die Domänen-oder Gesamtstruktur Funktionsebene erhöhen. Sie können die Funktionsebene auf Windows Server 2008 erhöhen, wenn alle Domänen Controller in der Domäne oder Gesamtstruktur Windows Server 2008 ausführen.  
  
Weitere Informationen finden Sie unter [Aktivieren erweiterter Funktionen für AD DS](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md).  
  


