---
ms.assetid: f052dfcd-dace-4485-8d0a-cc7df5cf3751
title: "Übersicht über Active Directory-Domänendienste"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b502017315d2b8b6b3d6ddfdad40c6d0f913e6c3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="active-directory-domain-services-overview"></a>Übersicht über Active Directory-Domänendienste

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


Ein Verzeichnis ist eine hierarchische Struktur, die Informationen zu Objekten im Netzwerk gespeichert. Ein Verzeichnisdienst wie Active Directory-Domänendienste (AD DS) bietet Methoden für die Speicherung von Verzeichnisdaten und diese Daten für Netzwerkbenutzer und Administratoren zur Verfügung stellen. Z. B. AD DS speichert Informationen über Benutzerkonten wie Namen, Kennwörter, Telefonnummern usw., und ermöglicht anderen autorisierten Benutzern im selben Netzwerk auf diese Informationen zuzugreifen.

Active Directory speichert Informationen zu Objekten im Netzwerk und erleichtert diese Informationen für Administratoren und Benutzer suchen und verwenden. Active Directory verwendet einen strukturierten Datenspeicher als Grundlage für die logische, hierarchische Anordnung von Verzeichnisinformationen.

Dieser Datenspeicher, der auch als Verzeichnis bezeichnet wird, enthält Informationen zu Active Directory-Objekte. Zu diesen Objekten gehören in der Regel freigegebene Ressourcen wie z. B. Server, Volumes, Drucker und das Netzwerk Benutzer- und Computerkonten. Weitere Informationen zu den Active Directory-Datenspeicher, finden Sie unter [Verzeichnisdatenspeicher](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx).

Sicherheit ist in Active Directory über die Anmeldeauthentifizierung und Steuerung des Zugriffs auf Objekte im Verzeichnis integriert. Mit einer einzigen netzwerkanmeldung Administratoren Verzeichnisdaten und die Organisation im gesamten Netzwerk verwalten und autorisierte Netzwerkbenutzer können Ressourcen an einer beliebigen Stelle im Netzwerk zugreifen. Richtlinienbasierte Verwaltung wird die Verwaltung der komplexesten Netzwerke erleichtert. Weitere Informationen zur Active Directory-Sicherheit finden Sie in der Übersicht über die Sicherheit.

Active Directory enthält:
* Eine Reihe von Regeln **das Schema**, definiert die Klassen der Objekte und Attribute enthalten, dem Verzeichnis, die Einschränkungen und Beschränkungen auf Instanzen dieser Objekte und das Format ihrer Namen. Weitere Informationen zum Schema finden Sie im Schema.


* Ein **globalen Katalog** , enthält Informationen zu jedem Objekt im Verzeichnis. Dadurch können Benutzer und Administratoren Verzeichnisinformationen Verzeichnisinformationen suchen, welche Domäne im Verzeichnis die Daten tatsächlich enthält. Weitere Informationen zum globalen Katalog finden Sie unter der Rolle des globalen Katalogs.


* Ein **Abfrage- und indexmechanismus**, sodass Objekte und ihre Eigenschaften veröffentlicht und von Netzwerkbenutzern bzw. Anwendungen gefunden werden können. Weitere Informationen zu Abfragen des Verzeichnisses finden Sie in der Verzeichnisinformationen suchen.


* Ein **Replikationsdienst** , die Verzeichnisdaten in einem Netzwerk verteilt. Alle Domänencontroller in einer Domäne bei der Replikation Teil und enthalten eine vollständige Kopie aller Verzeichnisinformationen für ihre Domäne. Jede Änderung an den Verzeichnisdaten wird auf allen Domänencontrollern in der Domäne repliziert. Weitere Informationen zur Active Directory-Replikation finden Sie in der Replikation (Übersicht).

## <a name="understanding-active-directory"></a>Grundlegendes zur Active Directory
 Dieser Abschnitt enthält Links zu den grundlegenden Active Directory-Konzepte:
 
* [Active Directory-Struktur und Speichertechnologien](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)
* [Domänen-Controller-Rollen](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* Active Directory-Schema 
* [Grundlegendes zu Vertrauensstellungen](https://technet.microsoft.com/library/cc771294(v=ws.10).aspx) 
* [Active Directory-Replikation-Technologien](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory-Suche und Veröffentlichung Technologien](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx) 
* Zusammenarbeit mit DNS und Gruppenrichtlinien 
* [Grundlegendes zum Schema](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx) 

Eine detaillierte Liste der Active Directory-Konzepte, finden Sie unter [Grundlegendes zur Active Directory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx). 


