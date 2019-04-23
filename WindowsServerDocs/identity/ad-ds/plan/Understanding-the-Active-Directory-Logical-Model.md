---
ms.assetid: 62708b2e-4090-4cf7-8ae6-a557f31f561f
title: Grundlegendes zum logischen Active Directory-Modell
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e909d4e9c1fb26aa0f7cb97a7dc06192db5cc21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834271"
---
# <a name="understanding-the-active-directory-logical-model"></a>Grundlegendes zum logischen Active Directory-Modell

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entwerfen Ihre logischen Struktur für die Active Directory Domain Services (AD DS) sind die Beziehungen zwischen den Containern in Ihrem Verzeichnis. Diese Beziehungen basiert möglicherweise auf verwaltungsanforderungen, z. B. die Delegierung von Autorität umgestellt haben, oder sie können definiert werden, durch die operativen Anforderungen, z.B. die Notwendigkeit zum Steuern der Replikation.  
  
Bevor Sie Ihre logischen Struktur von Active Directory entwerfen, ist es wichtig zu verstehen, das logische Modell des Active Directory. AD DS ist eine verteilte Datenbank, die Informationen gespeichert und verwaltet über Netzwerkressourcen und anwendungsspezifische Daten aus AD-fähigen Anwendungen. AD DS kann Administratoren Elemente eines Netzwerks (z. B. Benutzer, Computer und Geräte) Organisieren in einer hierarchischen Containerstruktur. Container der obersten Ebene ist die Gesamtstruktur. In Gesamtstrukturen, Domänen sind, und in Domänen werden Organisationseinheiten (OUs). Das logische Modell wird bezeichnet, da sie unabhängig von die physikalischen Aspekte der Bereitstellung, z.B. die Anzahl der Domänencontroller, die in jeder Domäne und Netzwerktopologie erforderlich ist.  
  
## <a name="active-directory-forest"></a>Active Directory-Gesamtstruktur  
Eine Gesamtstruktur ist eine Sammlung von ein oder mehrere Active Directory-Domänen, die eine gemeinsame logische Struktur ist, verwenden das Verzeichnisschema (Klassen- und Attributdefinitionen), Verzeichniskonfiguration (Site- und Replikationsinformationen-Informationen) und globalen Katalog (Gesamtstruktur suchen Funktionen). Domänen in derselben Gesamtstruktur werden automatisch mit bidirektionale, transitive Vertrauensstellungen verknüpft.  
  
## <a name="active-directory-domain"></a>Active Directory-Domäne  
Eine Domäne ist eine Partition in einer Active Directory-Gesamtstruktur. Partitionieren von Daten, ermöglicht Organisationen das Replizieren von Daten nur an, wo sie benötigt wird. Auf diese Weise kann das Verzeichnis global über ein Netzwerk skaliert werden, die verfügbare Bandbreite eingeschränkt ist. Darüber hinaus unterstützt die Domäne eine Anzahl von anderen Funktionen im Zusammenhang mit der Verwaltung, einschließlich:  
  
-   Die netzwerkweite Benutzeridentität. Domänen können Benutzeridentitäten einmal erstellt und auf die verwiesen wird auf einem beliebigen Computer in der Gesamtstruktur, in der sich die Domäne befindet. Domänencontroller, auf denen sich werden verwendet, um Benutzerkonten und Benutzeranmeldeinformationen (z. B. Kennwörter oder Zertifikate) sicher zu speichern.  
  
-   Authentifizierung Domänencontroller liefern Authentifizierungsdienste für Benutzer und zusätzliche Autorisierungsinformationen wie Benutzergruppenmitgliedschaften, die zum Steuern des Zugriffs auf Ressourcen im Netzwerk verwendet werden kann.  
  
-   Vertrauensstellungen. Domänen können Authentifizierungsdienste für Benutzer in Domänen außerhalb ihrer eigenen Gesamtstruktur über Vertrauensstellungen erweitern.  
  
-   Replikation Die Datendomäne definiert eine Partition des Verzeichnisses, das Domain Services bieten ausreichend Daten enthält, und es zwischen den Domänencontrollern repliziert werden. Auf diese Weise werden alle Domänencontroller Peers einer Domäne sind und als Einheit verwaltet werden.  
  
## <a name="active-directory-organizational-units"></a>Active Directory-Organisationseinheiten  
Organisationseinheiten können verwendet werden, um eine Hierarchie von Containern innerhalb einer Domäne zu erstellen. Organisationseinheiten dienen zum Gruppieren von Objekten zu administrativen Zwecken, wie die Anwendung der Gruppenrichtlinie oder die Delegierung von Autorität. Kontrolle (über eine Organisationseinheit und die darin befindlichen Objekte) richtet sich nach der Zugriffssteuerungslisten (ACLs) auf die Organisationseinheit und auf die Objekte in der Organisationseinheit. Zur Vereinfachung der Verwaltung einer großen Anzahl von Objekten unterstützt AD DS das Konzept der Delegierung von Autorität. Mithilfe der Delegierung können Besitzer vollen oder begrenzten administrative Kontrolle der Objekte für andere Benutzer oder Gruppen übertragen. Delegierung ist wichtig, da es dabei hilft, um die Verwaltung einer großen Anzahl von Objekten auf eine Anzahl von Personen zu verteilen, die Verwaltungsaufgaben vertrauenswürdig sind.  
  


