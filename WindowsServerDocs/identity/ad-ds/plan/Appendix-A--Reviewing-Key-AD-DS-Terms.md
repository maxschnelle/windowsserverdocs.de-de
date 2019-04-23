---
ms.assetid: 87196b65-a356-409f-9af0-b5950797d668
title: Anhang A – Überprüfen der wichtigsten AD DS-Begriffe
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5434db4124c471c613f159dec28e27dee70e7086
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852021"
---
# <a name="appendix-a-reviewing-key-ad-ds-terms"></a>Anhang A: Überprüfen die wichtigsten AD DS-Begriffe

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die folgenden Begriffe sind relevant für den Bereitstellungsprozess für Windows Server 2008 Active Directory Domain Services (AD DS).  
  
## <a name="active-directory-domain"></a>Active Directory-Domäne  
Eine administrative Einheit in einem Computernetzwerk, die zur Vereinfachung der Verwaltung, mehrere Funktionen, einschließlich der folgenden Gruppen:  
  
-   **Die netzwerkweite Benutzeridentität**. In Domänen werden Benutzeridentitäten einmal erstellt und auf jedem Computer, der in der Gesamtstruktur angehört, auf dem die Domäne wird, dann verwiesen. Domänencontroller, auf denen sich Speichern von Benutzerkonten und Benutzeranmeldeinformationen, wie z. B. Kennwörter oder Zertifikate, sicher.  
  
-   **Authentifizierung**. Domänencontroller stellen Authentifizierungsdienste für Benutzer. Sie geben auch zusätzliche Autorisierungsinformationen wie Benutzergruppenmitgliedschaften. Administratoren können diese Dienste verwenden, den Zugriff auf Ressourcen im Netzwerk steuern.  
  
-   **Vertrauensstellungen**. Domänen erweitern Authentifizierungsdienste auf Benutzer in anderen Domänen innerhalb ihrer eigenen Gesamtstruktur durch automatische bidirektionale Vertrauensstellungen. Domänen erweitern Authentifizierungsdienste auf Benutzer in Domänen, die in anderen Gesamtstrukturen auch mithilfe von entweder Gesamtstruktur-Vertrauensstellungen oder manuell erstellte externe Vertrauensstellungen.  
  
-   **Verwaltung von Gruppenrichtlinien**. Eine Domäne ist ein Bereich für Verwaltungsrichtlinien wie Kennwortkomplexität und Regeln zur Wiederverwendung.  
  
-   **Replikation** Eine Domäne definiert eine Partition der Directory-Struktur, die Daten bereitstellt, das ist ausreichend, um die erforderlichen Dienste bereitstellen und zwischen den Domänencontrollern repliziert, werden. Klicken Sie auf diese Weise können alle Domänencontroller sind Peers einer Domäne, und sie werden als Einheit verwaltet.  
  
## <a name="active-directory-forest"></a>Active Directory-Gesamtstruktur  
Eine Auflistung von einer oder mehreren Active Directory-Domänen, die eine gemeinsame logische Struktur, die Directory-Schema, und die Netzwerkkonfiguration sowie automatische, bidirektionale, transitive Vertrauensstellungen gemeinsam nutzen. Jede Gesamtstruktur ist eine einzelne Instanz des Verzeichnisses und definiert eine Sicherheitsgrenze.  
  
## <a name="active-directory-functional-level"></a>Active Directory-Domänenfunktionsebene  
Eine AD DS festlegen, können erweiterte AD DS-Features auf Domänen- oder Gesamtstruktur.  
  
## <a name="migration"></a>Migration  
Der Vorgang zum Verschieben eines Objekts von einer Quelldomäne zu einer Zieldomäne beim beibehalten oder Ändern der Eigenschaften des Objekts, das in der neuen Domäne zugänglich machen.  
  
## <a name="domain-restructure"></a>Domänenumstrukturierung  
Ein Migrationsprozess, das Änderung der Domänenstruktur einer Gesamtstruktur umfasst. Eine Domäne umzustrukturieren kann entweder die Konsolidierung oder das Hinzufügen von Domänen umfassen und es dauert zwischen Gesamtstrukturen oder innerhalb einer Gesamtstruktur vorhanden.  
  
## <a name="domain-consolidation"></a>Domänenkonsolidierung  
Ein Umstrukturierungsprozess, der das Entfernen von AD DS-Domänen durch Zusammenführen von deren Inhalt durch den Inhalt der anderen Domänen umfasst.  
  
## <a name="domain-upgrade"></a>Domänenaktualisierung  
Der Prozess der Aktualisierung des Verzeichnisdiensts einer Domäne auf eine neuere Version des Verzeichnisdiensts. Dies schließt das Upgrade des Betriebssystems auf allen Domänencontrollern und die AD DS-Funktionsebene auslösen, sofern zutreffend.  
  
## <a name="in-place-domain-upgrade"></a>Direkte domänenaktualisierung  
Der Prozess der aktualisieren die Betriebssysteme von allen Domänencontrollern in einer bestimmten Domäne, z. B. Aktualisieren von Windows Server 2003 auf Windows Server 2008 und ggf. die Funktionsebene der Domäne sind, auslösen, während Domänenobjekte, wie z. B. Benutzer und Gruppen vorhanden.  
  
## <a name="forest-root-domain"></a>Gesamtstruktur-Stammdomäne  
Die erste Domäne, die in Active Directory-Gesamtstruktur erstellt wird. Diese Domäne wird automatisch als Stammdomäne der Gesamtstruktur festgelegt werden. Sie bildet die Grundlage für die Active Directory-Gesamtstruktur-Infrastruktur.  
  
## <a name="regional-domain"></a>Regionaldomäne  
Eine untergeordnete Domäne, die in einer geografischen Region, um die Optimierung des Replikationsdatenverkehrs erstellt wird.  
  


