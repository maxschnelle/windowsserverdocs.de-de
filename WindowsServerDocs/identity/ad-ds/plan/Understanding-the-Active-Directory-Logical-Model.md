---
ms.assetid: 62708b2e-4090-4cf7-8ae6-a557f31f561f
title: Grundlegendes zum logischen Active Directory-Modell
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: c8f1cb2d7e3970ace95f2d0a4fac6b12efba1ca9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408651"
---
# <a name="understanding-the-active-directory-logical-model"></a>Grundlegendes zum logischen Active Directory-Modell

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Das Entwerfen der logischen Struktur für Active Directory Domain Services (AD DS) umfasst das Definieren der Beziehungen zwischen den Containern in Ihrem Verzeichnis. Diese Beziehungen basieren möglicherweise auf administrativen Anforderungen, z. b. die Delegierung der Zertifizierungsstelle, oder Sie werden möglicherweise durch betriebliche Anforderungen definiert, z. b. die Notwendigkeit, die Replikation zu steuern.  
  
Bevor Sie Ihre Active Directory logische Struktur entwerfen, ist es wichtig, das logische Modell Active Directory zu verstehen. AD DS ist eine verteilte Datenbank, in der Informationen zu Netzwerkressourcen und anwendungsspezifische Daten aus Verzeichnis fähigen Anwendungen gespeichert und verwaltet werden. AD DS ermöglicht es Administratoren, Elemente eines Netzwerks (z. b. Benutzer, Computer und Geräte) in einer hierarchischen Containment-Struktur zu organisieren. Der Container der obersten Ebene ist die Gesamtstruktur. In Gesamtstrukturen sind Domänen, und innerhalb von Domänen sind Organisationseinheiten (OUs). Dies wird als logisches Modell bezeichnet, da es unabhängig von den physischen Aspekten der Bereitstellung ist, z. b. von der Anzahl der Domänen Controller, die in jeder Domäne und der Netzwerktopologie erforderlich sind.  
  
## <a name="active-directory-forest"></a>Active Directory Gesamtstruktur  
Eine Gesamtstruktur ist eine Sammlung von einer oder mehreren Active Directory Domänen, die gemeinsam eine gemeinsame logische Struktur, ein Verzeichnisschema (Klassen-und Attribut Definitionen), Verzeichnis Konfiguration (Standort-und Replikations Informationen) und globalen Katalog (Gesamtstruktur weite Suche) verwenden. Funktionen). Domänen in derselben Gesamtstruktur werden automatisch mit bidirektionalen transitiven Vertrauens Stellungen verknüpft.  
  
## <a name="active-directory-domain"></a>Active Directory-Domäne  
Eine Domäne ist eine Partition in einer Active Directory-Gesamtstruktur. Durch die Partitionierung von Daten können Organisationen Daten nur an die Stelle replizieren, an der Sie benötigt Auf diese Weise kann das Verzeichnis global in einem Netzwerk skaliert werden, das eine begrenzte verfügbare Bandbreite aufweist. Außerdem unterstützt die Domäne eine Reihe weiterer Kernfunktionen im Zusammenhang mit der Verwaltung, einschließlich:  
  
-   Netzwerkweite Benutzeridentität. Mit Domänen können Benutzer Identitäten einmalig erstellt und auf jedem Computer verwiesen werden, der der Gesamtstruktur hinzugefügt wurde, in der sich die Domäne befindet. Domänen Controller, die eine Domäne bilden, werden verwendet, um Benutzerkonten und Benutzer Anmelde Informationen (z. b. Kenn Wörter oder Zertifikate) sicher zu speichern.  
  
-   Authentifizierung Domänen Controller stellen Authentifizierungsdienste für Benutzer bereit und geben zusätzliche Autorisierungs Daten wie z. b. Benutzergruppen Mitgliedschaften an, mit denen der Zugriff auf Ressourcen im Netzwerk gesteuert werden kann.  
  
-   Vertrauens Stellungen. Domänen können Authentifizierungsdienste mithilfe von Vertrauens Stellungen für Benutzer in Domänen außerhalb ihrer eigenen Gesamtstruktur erweitern.  
  
-   Replikation Die Domäne definiert eine Partition des Verzeichnisses, das genügend Daten enthält, um Domänen Dienste bereitzustellen, und repliziert Sie dann zwischen den Domänen Controllern. Auf diese Weise handelt es sich bei allen Domänen Controllern um Peers in einer Domäne, die als Einheit verwaltet werden.  
  
## <a name="active-directory-organizational-units"></a>Organisationseinheiten Active Directory  
Organisationseinheiten können verwendet werden, um eine Hierarchie von Containern innerhalb einer Domäne zu bilden. Organisationseinheiten werden verwendet, um Objekte zu Verwaltungszwecken zu gruppieren, z. b. die Anwendung Gruppenrichtlinie oder die Delegierung der Zertifizierungsstelle. Die Steuerung (über eine Organisationseinheit und die darin enthaltenen Objekte) wird durch die Zugriffs Steuerungs Listen (Access Control Lists, ACLs) in der Organisationseinheit und für die Objekte in der Organisationseinheit festgelegt. Um die Verwaltung einer großen Anzahl von Objekten zu vereinfachen, unterstützt AD DS das Konzept der Delegierung von Autorität. Mithilfe der Delegierung können Besitzer die vollständige oder eingeschränkte administrative Kontrolle über Objekte auf andere Benutzer oder Gruppen übertragen. Die Delegierung ist wichtig, da Sie die Verwaltung einer großen Anzahl von Objekten auf mehrere Personen verteilt, die für die Durchführung von Verwaltungsaufgaben vertrauenswürdig sind.  
  


