---
ms.assetid: 87196b65-a356-409f-9af0-b5950797d668
title: 'Anhang A: Überprüfen der Schlüssel AD DS Bedingungen'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ad8c1cf769c0c2a22e2d55f7bd2d111095410afe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822863"
---
# <a name="appendix-a-reviewing-key-ad-ds-terms"></a>Anhang A: Die wichtigsten AD DS-Begriffe

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die folgenden Begriffe sind für den Bereitstellungs Prozess für Windows Server 2008 Active Directory Domain Services (AD DS) relevant.  
  
## <a name="active-directory-domain"></a>Active Directory-Domäne  
Eine administrative Einheit in einem Computernetzwerk, die zur einfacheren Verwaltung verschiedene Funktionen gruppiert, einschließlich der folgenden:  
  
-   **Netzwerkweite Benutzeridentität**. In Domänen können Benutzer Identitäten einmalig erstellt und dann auf jedem Computer verwiesen werden, der der Gesamtstruktur hinzugefügt wird, in der sich die Domäne befindet. Domänen Controller, die eine Domäne bilden, speichern Benutzerkonten und Benutzer Anmelde Informationen, z. b. Kenn Wörter oder Zertifikate, sicher.  
  
-   **Authentifizierung**. Domänen Controller stellen Authentifizierungsdienste für Benutzer bereit. Außerdem stellen Sie zusätzliche Autorisierungs Daten bereit, wie z. b. Benutzergruppen Mitgliedschaften. Administratoren können diese Dienste verwenden, um den Zugriff auf Ressourcen im Netzwerk zu steuern.  
  
-   **Vertrauens**Stellungen. Domänen erweitern Authentifizierungsdienste auf Benutzer in anderen Domänen in ihrer eigenen Gesamtstruktur mithilfe automatischer bidirektionaler Vertrauens Stellungen. Domänen erweitern außerdem Authentifizierungsdienste für Benutzer in Domänen in anderen Gesamtstrukturen mithilfe von Gesamtstruktur-Vertrauens Stellungen oder manuell erstellten externen Vertrauens Stellungen.  
  
-   **Richtlinien Verwaltung**. Eine Domäne ist ein Bereich von Verwaltungsrichtlinien, wie z. b. die Kenn Wort Komplexität und die Wiederverwendung von Kenn Wörtern  
  
-   **Replikation** Eine Domäne definiert eine Partition der Verzeichnisstruktur, die Daten bereitstellt, die für die Bereitstellung erforderlicher Dienste geeignet sind und zwischen Domänen Controllern repliziert werden. Auf diese Weise handelt es sich bei allen Domänen Controllern um Peers in einer Domäne, die als Einheit verwaltet werden.  
  
## <a name="active-directory-forest"></a>Active Directory-Gesamtstruktur  
Eine Auflistung von einer oder mehreren Active Directory Domänen, die über eine gemeinsame logische Struktur, ein gemeinsames Verzeichnisschema und eine gemeinsame Netzwerkkonfiguration verfügen, sowie automatische, bidirektionale transitiv Vertrauens Stellungen. Jede Gesamtstruktur ist eine einzelne Instanz des Verzeichnisses und definiert eine Sicherheitsgrenze.  
  
## <a name="active-directory-functional-level"></a>Funktionsebene "Active Directory"  
Eine AD DS Einstellung, die erweiterte Domänen weite oder Gesamtstruktur weite AD DS Features ermöglicht.  
  
## <a name="migration"></a>Migration  
Der Prozess, bei dem ein Objekt aus einer Quell Domäne in eine Zieldomäne verschoben wird, während die Eigenschaften des Objekts beibehalten oder geändert werden, um es in der neuen Domäne zugänglich zu machen.  
  
## <a name="domain-restructure"></a>Domänen Umstrukturierung  
Ein Migrationsprozess, bei dem die Domänen Struktur einer Gesamtstruktur geändert wird. Eine Domänen Umstrukturierung kann entweder die Konsolidierung oder das Hinzufügen von Domänen umfassen und kann zwischen Gesamtstrukturen oder innerhalb einer Gesamtstruktur stattfinden.  
  
## <a name="domain-consolidation"></a>Domänen Konsolidierung  
Ein Umstrukturierungsprozess, bei dem AD DS Domänen durch Zusammenführen des Inhalts mit dem Inhalt anderer Domänen eliminiert werden.  
  
## <a name="domain-upgrade"></a>Domänen Upgrade  
Der Prozess, bei dem der Verzeichnisdienst einer Domäne auf eine spätere Version des Verzeichnis Dienstanbieter aktualisiert wird. Dies umfasst das Upgrade des Betriebssystems auf allen Domänen Controllern und das Erhöhen der AD DS Funktionsebene, sofern zutreffend.  
  
## <a name="in-place-domain-upgrade"></a>Direktes Domänen Upgrade  
Der Upgradevorgang für die Betriebssysteme aller Domänen Controller in einer bestimmten Domäne, z. b. ein Upgrade von Windows Server 2003 auf Windows Server 2008 und das Erhöhen der Funktionsebene der Domäne (falls zutreffend), ohne Domänen Objekte (z. b. Benutzer und Gruppen) zu belassen.  
  
## <a name="forest-root-domain"></a>Gesamtstruktur-Stamm Domäne  
Die erste Domäne, die in der Active Directory Gesamtstruktur erstellt wird. Diese Domäne wird automatisch als Stamm Domäne der Gesamtstruktur bezeichnet. Sie bildet die Grundlage für die Infrastruktur der Active Directory Gesamtstruktur.  
  
## <a name="regional-domain"></a>Regionale Domäne  
Eine untergeordnete Domäne, die in einer geografischen Region erstellt wird, um Replikations Datenverkehr zu optimieren.  
  


