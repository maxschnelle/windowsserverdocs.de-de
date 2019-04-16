---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: Zuordnen Ihren Anforderungen zu einer AD DS-Bereitstellungsstrategie
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b4f625f06fede5b9dc751282cda19b68d7f9e535
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>Zuordnen Ihren Anforderungen zu einer AD DS-Bereitstellungsstrategie

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nach dem Abschluss überprüfen und identifizieren das Active Directory-Domänendienste (AD DS)-Design und Anforderungen für die Bereitstellung und bestimmt haben, die von ihnen für Ihre spezielle Bereitstellung verknüpft sind, können Sie diese Anforderungen zu einer bestimmten AD DS-Bereitstellungsstrategie zuordnen.  
  
Verwenden Sie in der folgende Tabelle, um zu bestimmen, welche AD DS-Bereitstellungsstrategie der Kombination von AD DS-Entwurf und Bereitstellung von Anforderungen für Ihre Organisation zuordnet. ("Ja" bedeutet, dass eine bestimmte Anforderung für Ihre Bereitstellungsstrategie erforderlich ist; "No" bedeutet, dass eine bestimmte Anforderung nicht für Ihre Bereitstellungsstrategie erforderlich ist.)  
  
In dieser Tabelle bezieht sich nur auf die drei primären AD DS-Bereitstellungsstrategien, wie in diesem Handbuch beschrieben:  
  
-   [Bereitstellen von AD DS in einer neuen Organisation](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Bereitstellen von AD DS in einer Windows Server 2003-Organisation](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Bereitstellen von AD DS in einer Windows 2000-Organisation](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
Allerdings können Sie einen Hybriden oder benutzerdefinierten AD DS-Bereitstellungsstrategie mithilfe einer beliebigen Kombination der Anforderungen an AD DS Entwurfs- und den Bedürfnissen Ihrer Organisation erstellen.  
  
|AD DS Entwurfs- und Anforderungen|Bereitstellen von AD DS in einer neuen Organisation|Bereitstellen von AD DS in einer Windows Server 2003-Organisation|Bereitstellen von AD DS in einer Windows 2000-Organisation|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Entwerfen der logischen Struktur für Windows Server2008 AD DS](https://technet.microsoft.com/library/cc770806.aspx)|Ja|Ja|Ja|  
|[Entwerfen der Standorttopologie für Windows Server2008 AD DS](Designing-the-Site-Topology.md)|Ja|Ja|Ja|  
|Planen der Domänencontrollerkapazität|Ja|Ja|Ja|  
|[Bereitstellen einer Gesamtstruktur-Stammdomäne für Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx)|Ja|Nein|Nein|  
|[Bereitstellen von Regionaldomänen für Windows Server 2008](https://technet.microsoft.com/library/cc755118.aspx)|Ja|Ja|Ja|  
|[Aktivieren erweiterter Funktionen für AD DS](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|Ja|Ja, aber alle Domänencontroller in der Umgebung müssen Windows Server 2008 ausgeführt, bevor Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server 2008 festgelegt.|Ja, aber alle Domänencontroller in der Umgebung müssen Windows Server 2008 ausgeführt, bevor Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server 2008 festgelegt.|  
|[Aktualisieren von Active Directory-Domänen auf WindowsServer 2008 und Windows Server 2008 R2 AD DS-Domänen](https://technet.microsoft.com/library/cc731188.aspx)|Nein|Ja|Ja|  
|[Umstrukturieren von AD DS-Domänen zwischen Gesamtstrukturen](https://go.microsoft.com/fwlink/?LinkId=93678)|Ja, wenn Sie eine Pilotprojekte Domäne in die produktionsumgebung migrieren möchten, Zusammenführen mit einer anderen Organisation und die zwei Informationen Informationstechnologie (IT)-Infrastrukturen zu konsolidieren oder Konsolidierung von Ressourcen und Konto Domänen, die Sie direkt von Windows 2000 oder Windows Server 2003-Umgebung aktualisiert.|Ja, wenn Sie mit einer anderen Organisation zusammenführen und zwei IT-Infrastrukturen zu konsolidieren oder Ressource und Konto Domänen, die Sie von Windows 2000 oder Windows Server 2003-Umgebung für das Upgrade zu konsolidieren möchten.|Ja, wenn Sie mit einer anderen Organisation zusammenführen und zwei IT-Infrastrukturen zu konsolidieren oder Ressource und Konto Domänen, die Sie von Windows 2000 oder Windows Server 2003-Umgebung für das Upgrade zu konsolidieren möchten.|  
|[Umstrukturieren von AD DS-Domänen in Gesamtstrukturen](https://go.microsoft.com/fwlink/?LinkId=82740))|Nein|Ja, wenn Sie zum Reduzieren der Anzahl von Domänen, Replikations-Datenverkehr und den Umfang der erforderlichen Benutzer und Gruppe Verwaltung zu reduzieren, oder vereinfachen der Verwaltung von Gruppenrichtlinien.|Ja, wenn Sie zum Reduzieren der Anzahl von Domänen, Replikations-Datenverkehr und den Umfang der erforderlichen Benutzer und Gruppe Verwaltung zu reduzieren, oder vereinfachen der Verwaltung von Gruppenrichtlinien.|  
  


