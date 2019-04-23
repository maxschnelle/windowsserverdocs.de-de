---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: Zuordnen Ihren Anforderungen zu einer AD DS-Bereitstellungsstrategie
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a61e5e6d429acd92e48a353bc829cb620dd66054
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881831"
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>Zuordnen Ihren Anforderungen zu einer AD DS-Bereitstellungsstrategie

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie abgeschlossen haben, überprüfen und identifizieren den Entwurf des Active Directory Domain Services (AD DS) und Anforderungen für die Bereitstellung und bestimmt haben, die von ihnen für Ihre spezielle Bereitstellung verknüpft sind, können Sie diese Anforderungen in eine bestimmte AD DS-Bereitstellung zuordnen. Strategie.  
  
Verwenden Sie in der folgende Tabelle, um zu bestimmen, welche AD DS-Bereitstellungsstrategie die geeignete Kombination von AD DS-Entwurf und Bereitstellung von Anforderungen für Ihre Organisation zugeordnet. ("Ja" bedeutet, dass eine bestimmte Anforderung für Ihre Strategie für die Bereitstellung erforderlich ist; "Nein" bedeutet, dass eine bestimmte Anforderung nicht für Ihre Strategie für die Bereitstellung erforderlich ist.)  
  
In dieser Tabelle bezieht sich nur auf die drei primären AD DS-Bereitstellungsstrategien, wie in diesem Handbuch beschrieben:  
  
-   [Bereitstellen von AD DS in einer neuen Organisation](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Bereitstellen von AD DS in einer Windows Server 2003-Organisation](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Bereitstellen von AD DS in einer Windows 2000-Organisation](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
Allerdings können Sie einer Hybrid- oder benutzerdefinierten AD DS-Bereitstellungsstrategie erstellen, mit der eine beliebige Kombination aus den AD DS-Entwurf und Bereitstellung von Anforderungen für die Bedürfnisse Ihrer Organisation.  
  
|AD DS-Entwurf und Bereitstellung von Anforderungen|Bereitstellen von AD DS in einer neuen Organisation|Bereitstellen von AD DS in einer Windows Server 2003-Organisation|Bereitstellen von AD DS in einer Windows 2000-Organisation|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Entwerfen der logischen Struktur für Windows Server 2008 AD DS](https://technet.microsoft.com/library/cc770806.aspx)|Ja|Ja|Ja|  
|[Entwerfen der Standorttopologie für Windows Server 2008 AD DS](Designing-the-Site-Topology.md)|Ja|Ja|Ja|  
|Planen der Domänencontrollerkapazität|Ja|Ja|Ja|  
|[Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne](https://technet.microsoft.com/library/cc731174.aspx)|Ja|Nein|Nein|  
|[Bereitstellen von Regionaldomänen für Windows Server 2008](https://technet.microsoft.com/library/cc755118.aspx)|Ja|Ja|Ja|  
|[Aktivieren erweiterter Funktionen für AD DS](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|Ja|Ja, aber alle Domänencontroller in der Umgebung müssen Windows Server 2008 ausführen, bevor Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server 2008 festlegen.|Ja, aber alle Domänencontroller in der Umgebung müssen Windows Server 2008 ausführen, bevor Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server 2008 festlegen.|  
|[Aktualisieren von Active Directory-Domänen auf WindowsServer 2008 und Windows Server 2008 R2 AD DS-Domänen](https://technet.microsoft.com/library/cc731188.aspx)|Nein|Ja|Ja|  
|[Umstrukturieren von AD DS-Domänen zwischen Gesamtstrukturen](https://go.microsoft.com/fwlink/?LinkId=93678)|Ja, wenn Sie eine Pilotprojekt Domäne in Ihrer produktionsumgebung migrieren möchten, mit einer anderen Organisation Zusammenführen Sie und konsolidieren Sie die beiden Informationen Informationstechnologie (IT)-Infrastrukturen zu oder konsolidieren Sie Ressourcenmanagement und Kundenmanagement Domänen, die Sie direkt aus Windows aktualisiert 2000 oder Windows Server 2003-Umgebungen.|Ja, wenn der merge mit einer anderen Organisation und die beiden IT-Infrastrukturen zu konsolidieren oder konsolidieren Ressourcenmanagement und Kundenmanagement Domänen, die Sie direkt von Windows 2000 oder Windows Server 2003-Umgebungen aktualisiert werden sollen.|Ja, wenn der merge mit einer anderen Organisation und die beiden IT-Infrastrukturen zu konsolidieren oder konsolidieren Ressourcenmanagement und Kundenmanagement Domänen, die Sie direkt von Windows 2000 oder Windows Server 2003-Umgebungen aktualisiert werden sollen.|  
|[AD DS-Domänen innerhalb der Gesamtstrukturen umstrukturieren](https://go.microsoft.com/fwlink/?LinkId=82740))|Nein|Ja, bei Bedarf, um die Anzahl der Domänen zu reduzieren, verringern Sie der Replikationsdatenverkehr und die Menge der erforderlichen Benutzer- und gruppenverwaltung und vereinfachen Sie die Verwaltung von Gruppenrichtlinien.|Ja, bei Bedarf, um die Anzahl der Domänen zu reduzieren, verringern Sie der Replikationsdatenverkehr und die Menge der erforderlichen Benutzer- und gruppenverwaltung und vereinfachen Sie die Verwaltung von Gruppenrichtlinien.|  
  


