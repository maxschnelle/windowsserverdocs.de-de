---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: Zuordnen Ihren Anforderungen zu einer AD DS-Bereitstellungsstrategie
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 1e2d089919f8f09cd241f336748a66c4f52f19d4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822214"
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>Zuordnen Ihren Anforderungen zu einer AD DS-Bereitstellungsstrategie

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie die Entwurfs-und Bereitstellungs Anforderungen für Active Directory Domain Services (AD DS) überprüft und identifiziert haben und Sie feststellen, welche von Ihnen mit ihrer spezifischen Bereitstellung in Zusammenhang stehen, können Sie diese Anforderungen einer bestimmten AD DS Bereitstellungs Strategie zuordnen.  
  
Verwenden Sie die folgende Tabelle, um zu bestimmen, welche AD DS Bereitstellungs Strategie der entsprechenden Kombination von AD DS Entwurfs-und Bereitstellungs Anforderungen für Ihre Organisation entspricht. ("Ja" bedeutet, dass eine bestimmte Anforderung für Ihre Bereitstellungs Strategie erforderlich ist. "Nein" bedeutet, dass eine bestimmte Anforderung für Ihre Bereitstellungs Strategie nicht erforderlich ist.)  
  
Diese Tabelle bezieht sich nur auf die drei primären AD DS Bereitstellungs Strategien, die in diesem Handbuch beschrieben werden:  
  
-   [Bereitstellen der AD DS in einer neuen Organisation](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Bereitstellen der AD DS in einer Organisation mit Windows Server 2003](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Bereitstellen der AD DS in einer Organisation mit Windows 2000](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
Sie können jedoch eine Hybrid-oder benutzerdefinierte AD DS Bereitstellungs Strategie erstellen, indem Sie eine beliebige Kombination der AD DS Entwurfs-und Bereitstellungs Anforderungen verwenden, um die Anforderungen Ihrer Organisation zu erfüllen.  
  
|AD DS Entwurfs-und Bereitstellungs Anforderungen|Bereitstellen von AD DS in einer neuen Organisation|Bereitstellen von AD DS in einer Windows Server 2003-Organisation|Bereitstellen von AD DS in einer Windows 2000-Organisation|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Entwerfen der logischen Struktur für Windows Server 2008 AD DS](https://technet.microsoft.com/library/cc770806.aspx)|Ja|Ja|Ja|  
|[Entwerfen der Standort Topologie für Windows Server 2008 AD DS](Designing-the-Site-Topology.md)|Ja|Ja|Ja|  
|Planen der Domänencontrollerkapazität|Ja|Ja|Ja|  
|[Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stamm Domäne](https://technet.microsoft.com/library/cc731174.aspx)|Ja|Nein|Nein|  
|[Bereitstellen von regionalen Windows Server 2008-Domänen](https://technet.microsoft.com/library/cc755118.aspx)|Ja|Ja|Ja|  
|[Aktivieren erweiterter Funktionen für die AD DS](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|Ja|Ja, allerdings müssen alle Domänen Controller in der Umgebung Windows Server 2008 ausführen, bevor Sie die Domänen-oder Gesamtstruktur Funktionsebene auf Windows Server 2008 festlegen.|Ja, allerdings müssen alle Domänen Controller in der Umgebung Windows Server 2008 ausführen, bevor Sie die Domänen-oder Gesamtstruktur Funktionsebene auf Windows Server 2008 festlegen.|  
|[Aktualisieren von Active Directory Domänen auf Windows Server 2008 und Windows Server 2008 R2 AD DS Domänen](https://technet.microsoft.com/library/cc731188.aspx)|Nein|Ja|Ja|  
|[Umstrukturierung von AD DS Domänen zwischen Gesamtstrukturen](https://go.microsoft.com/fwlink/?LinkId=93678)|Ja, wenn Sie eine Pilot Domäne in Ihre Produktionsumgebung migrieren möchten, führen Sie eine Zusammenführung mit einer anderen Organisation durch, und konsolidieren Sie die beiden IT-Infrastrukturen, oder konsolidieren Sie Ressourcen-und Konto Domänen, die Sie direkt aus den Umgebungen Windows 2000 oder Windows Server 2003 aktualisiert haben.|Ja, wenn Sie mit einer anderen Organisation zusammenführen und die beiden IT-Infrastrukturen konsolidieren oder Ressourcen-und Konto Domänen konsolidieren möchten, die Sie direkt aus den Umgebungen Windows 2000 oder Windows Server 2003 aktualisiert haben.|Ja, wenn Sie mit einer anderen Organisation zusammenführen und die beiden IT-Infrastrukturen konsolidieren oder Ressourcen-und Konto Domänen konsolidieren möchten, die Sie direkt aus den Umgebungen Windows 2000 oder Windows Server 2003 aktualisiert haben.|  
|[Umstrukturierung AD DS Domänen in](https://go.microsoft.com/fwlink/?LinkId=82740)Gesamtstrukturen)|Nein|Ja, wenn Sie die Anzahl der Domänen reduzieren müssen, verringern Sie den Replikations Datenverkehr und die erforderliche Benutzer-und Gruppenverwaltung, oder vereinfachen Sie die Verwaltung von Gruppenrichtlinie.|Ja, wenn Sie die Anzahl der Domänen reduzieren müssen, verringern Sie den Replikations Datenverkehr und die erforderliche Benutzer-und Gruppenverwaltung, oder vereinfachen Sie die Verwaltung von Gruppenrichtlinie.|  
  


