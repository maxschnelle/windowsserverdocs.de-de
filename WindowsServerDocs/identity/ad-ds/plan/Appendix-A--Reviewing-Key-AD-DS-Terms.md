---
ms.assetid: 87196b65-a356-409f-9af0-b5950797d668
title: "Anhang A – Überprüfen der wichtigsten AD DS-Begriffe"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ce7c0b639ded498b15200dfd594b3f34d6492dce
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-a-reviewing-key-ad-ds-terms"></a>AnhangA: Überprüfen der wichtigsten AD DS-Begriffe

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die folgenden Begriffe sind relevant, um den Bereitstellungsprozess für Windows Server 2008 Active Directory-Domänendienste (AD DS).  
  
## <a name="active-directory-domain"></a>Active Directory-Domäne  
Eine administrative Einheit in einem Computernetzwerk, die für die Verwaltung der Einfachheit halber mehrere Funktionen, u. a. folgende Gruppen:  
  
-   **Die netzwerkweite Benutzeridentität**. In Domänen Benutzeridentitäten einmal erstellt und dann auf die verwiesen wird auf jedem Computer, der in der Gesamtstruktur gehört, in dem sich die Domäne befindet. Domänencontroller, die einer Domäne bilden Speichern von Benutzerkonten und Anmeldeinformationen, z. B. Kennwörter oder Zertifikate, sicher.  
  
-   **Authentifizierung**. Domänencontroller stellen Authentifizierungsdienste für Benutzer. Sie geben auch zusätzliche Autorisierungsdaten, z. B. Gruppenmitgliedschaften. Diese Dienste können Administratoren den Zugriff auf Ressourcen im Netzwerk steuern.  
  
-   **Vertrauensstellungen**. Domänen erweitern Authentifizierungsdienste für Benutzer in anderen Domänen in ihrer eigenen Gesamtstruktur durch automatische bidirektionale Vertrauensstellungen. Domänen erweitern Authentifizierungsdienste für Benutzer in Domänen in anderen Gesamtstrukturen auch über Gesamtstruktur-Vertrauensstellungen oder manuell erstellte externe Vertrauensstellungen.  
  
-   **Verwaltung von Gruppenrichtlinien**. Eine Domäne ist eine administrative Richtlinien wie z. B. Kennwortkomplexität und Regeln wiederverwenden.  
  
-   **Replikation**. Eine Domäne definiert eine Partition der Verzeichnisstruktur, die Daten enthält, ausreicht, um die erforderlichen Dienste bereitzustellen und zwischen den Domänencontrollern repliziert. Klicken Sie auf diese Weise alle Domänencontroller Peers in einer Domäne sind, und sie als eine Einheit verwaltet werden.  
  
## <a name="active-directory-forest"></a>Active Directory-Gesamtstruktur  
Eine Auflistung von einem oder mehreren Active Directory-Domänen, die eine logische Struktur, Directory-Schema und Netzwerkkonfiguration sowie automatische, bidirektionale, transitive Vertrauensstellungen gemeinsam nutzen. Jede Gesamtstruktur ist eine einzelne Instanz des Verzeichnisses, und es wird eine Sicherheitsgrenze definiert.  
  
## <a name="active-directory-functional-level"></a>Active Directory-Domänenfunktionsebene  
Eine Einstellung, die AD-DS ermöglicht erweiterte AD DS-Features auf Domänen- oder Gesamtstruktur.  
  
## <a name="migration"></a>Migration  
Der Vorgang zum Verschieben eines Objekts aus einer Quelldomäne zu einer Zieldomäne beim beibehalten oder Ändern von Eigenschaften des Objekts, das in der neuen Domäne zugänglich machen.  
  
## <a name="domain-restructure"></a>Umstrukturieren von Domänen  
Eine Migration umfasst, die Änderung der Domänenstruktur einer Gesamtstruktur. Eine Domäne Umstrukturierung beinhalten die Konsolidierung oder das Hinzufügen von Domänen, und es kann stattfinden zwischen Gesamtstrukturen oder innerhalb einer Gesamtstruktur.  
  
## <a name="domain-consolidation"></a>Konsolidierung  
Ein Neustrukturieren von Prozess, der das Entfernen von AD DS-Domänen durch Zusammenführen ihrer Inhalte mit den Inhalten der anderen Domänen umfasst.  
  
## <a name="domain-upgrade"></a>Update der Domäne  
Der Vorgang zur Aktualisierung des Verzeichnisdiensts, der einer Domäne zu einer neueren Version des Verzeichnisdiensts. Dazu gehören ein Upgrade des Betriebssystems auf allen Domänencontrollern und die Funktionsebene der AD DS gegebenenfalls.  
  
## <a name="in-place-domain-upgrade"></a>Direktes Domänenupgrade  
Der Prozess die Betriebssysteme aller Domänencontroller in einer bestimmten Domäne, z. B. aktualisieren, Aktualisieren von Windows Server 2003 auf Windows Server 2008 und der Funktionsebene der der Domäne, falls zutreffend, ohne Domänenobjekte, z. B. Benutzer und Gruppen vorhanden.  
  
## <a name="forest-root-domain"></a>Gesamtstruktur-Stammdomäne  
Die erste Domäne, die in Active Directory-Gesamtstruktur erstellt wird. Diese Domäne wird automatisch als Stammdomäne der Gesamtstruktur verwendet. Er bildet die Grundlage für die Infrastruktur der Active Directory-Gesamtstruktur.  
  
## <a name="regional-domain"></a>Regionale Domäne  
Eine untergeordnete Domäne, die in einer geografischen Region Replikationsdatenverkehr optimieren erstellt wird.  
  


