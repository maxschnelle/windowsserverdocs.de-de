---
ms.assetid: 62708b2e-4090-4cf7-8ae6-a557f31f561f
title: Grundlegendes zum logischen Active Directory-Modell
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0f8cdc4789d1b3008f3b53104e5517d4ef1e65b9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="understanding-the-active-directory-logical-model"></a>Grundlegendes zum logischen Active Directory-Modell

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Entwerfen der logischen Struktur für Active Directory-Domänendienste (AD DS) umfasst die Beziehungen zwischen den Containern in Ihrem Verzeichnis definieren. Diese Beziehungen möglicherweise auf Verwaltungsaufwand, z.B. die Delegierung von Autorität, oder er können definiert werden, indem betriebsanforderungen, z.B. die Notwendigkeit zum Steuern der Replikation.  
  
Bevor Sie Ihre logische Active Directory-Struktur entwerfen, ist es wichtig zu verstehen, die logische Active Directory-Modell. AD DS ist eine verteilte Datenbank, die gespeichert und verwaltet Informationen zu Netzwerkressourcen und anwendungsspezifische Daten aus AD-aktivierte Anwendungen. AD DS kann Administratoren zum Organisieren der Elemente eines Netzwerks (z.B. Benutzer, Computer und Geräte) in einer hierarchischen Containerstruktur. Der Container der obersten Ebene ist die Gesamtstruktur. Domänen in Gesamtstrukturen sind und innerhalb von Domänen sind Organisationseinheiten (OUs). Das logische Modell wird bezeichnet, da es unabhängig von der physischen Aspekte der Bereitstellung, z.B. die Anzahl der Domänencontroller in jeder Domäne und Netzwerktopologie erforderlich ist.  
  
## <a name="active-directory-forest"></a>Active Directory-Gesamtstruktur  
Eine Gesamtstruktur ist eine Sammlung von einem oder mehreren Active Directory-Domänen, die eine gemeinsame logische Struktur haben Directory-Schema (Klassen- und Attributdefinitionen), Directory-Konfiguration (Site- und Replikationsinformationen Informationen) und globalen Katalog (gesamtstrukturweite Suchfunktionen). Mit bidirektionale, transitive Vertrauensstellungen zwischen Domänen in derselben Gesamtstruktur automatisch verknüpft.  
  
## <a name="active-directory-domain"></a>Active Directory-Domäne  
Eine Domäne ist eine Partition in einer Active Directory-Gesamtstruktur. Partitionierung von Daten kann Organisationen replizieren Daten nur an dem er benötigt wird. Auf diese Weise kann das Verzeichnis global über ein Netzwerk skaliert werden, die verfügbare Bandbreite eingeschränkt ist. Darüber hinaus unterstützt die Domäne eine Reihe von anderen zentralen Funktionen in Zusammenhang stehen, einschließlich:  
  
-   Die netzwerkweite Benutzeridentität. Domänen können Benutzeridentitäten einmal erstellt und auf einem beliebigen Computer in der Gesamtstruktur, in der sich die Domäne befindet, verwiesen werden. Domänencontroller, die einer Domäne bilden werden verwendet, um Benutzerkonten und Anmeldeinformationen des Benutzers (z.B. Kennwörter oder Zertifikate) sicher zu speichern.  
  
-   Authentifizierung. Domänencontroller stellen Authentifizierungsdienste bereit für Benutzer und zusätzliche Autorisierungsinformationen wie z.B. Gruppenmitgliedschaften des Benutzers, die zum Steuern des Zugriffs auf Ressourcen im Netzwerk verwendet werden können.  
  
-   Vertrauensstellungen. Domänen können Authentifizierungsdienste für Benutzer in Domänen außerhalb ihrer eigenen Gesamtstruktur über Vertrauensstellungen erweitern.  
  
-   Replikation. Die Domäne definiert eine Partition des Verzeichnisses mit den enthält genügend Daten zur Domänendienste bereitzustellen, und klicken Sie dann zwischen den Domänencontrollern repliziert. Auf diese Weise werden alle Domänencontroller Peers in einer Domäne sind und als Einheit verwaltet werden.  
  
## <a name="active-directory-organizational-units"></a>Active Directory-Organisationseinheiten  
Organisationseinheiten können verwendet werden, um eine Hierarchie von Containern innerhalb einer Domäne zu bilden. Organisationseinheiten dienen zum Gruppieren von Objekten für administrative Zwecke, wie die Anwendung der Gruppenrichtlinie oder der Delegierung von Autorität. Steuerelement (über eine Organisationseinheit und die darin enthaltenen Objekte) wird bestimmt, indem Sie die Zugriffssteuerungslisten (ACLs) auf die Organisationseinheit und die Objekte in der Organisationseinheit. Um die Verwaltung einer großen Anzahl von Objekten zu ermöglichen, unterstützt AD DS das Konzept der Delegierung von Autorität. Durch die Delegierung können Besitzer vollen oder begrenzten administrativen Kontrolle über Objekte auf anderen Benutzern oder Gruppen übertragen. Delegierung ist wichtig, da er erleichtert um die Verwaltung einer großen Anzahl von Objekten in einer Reihe von Personen zu verteilen, die zum Ausführen von Verwaltungsaufgaben vertrauenswürdig sind.  
  


