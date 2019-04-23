---
title: Übersicht über Active Directory Domain Services
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6cfe9479-5d17-41d5-939a-891e5233fdca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 3d0e849edbff3a481ffd28f83d7f14089030920d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843131"
---
# <a name="active-directory-domain-services-overview"></a>Übersicht über Active Directory Domain Services

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016
  
Ein Verzeichnis ist eine hierarchische Struktur, die Informationen zu Objekten im Netzwerk gespeichert. Ein Verzeichnisdienst wie Active Directory Domain Services (AD DS), stellt die Methoden für die Speicherung von Verzeichnisdaten und die Verfügbarmachung dieses Daten für Netzwerkbenutzer und Administratoren bereit. Z. B. AD DS speichert Informationen über Benutzerkonten wie Namen, Kennwörter, Telefonnummern und So weiter, und ermöglicht anderen autorisierten Benutzern im selben Netzwerk auf diese Informationen zuzugreifen.  
  
Active Directory speichert Informationen zu Objekten im Netzwerk und erleichtert diese Informationen für Administratoren und Benutzer suchen und verwenden. Active Directory verwendet einen strukturierter Datenspeicher als Grundlage für einen logischen, hierarchischen Organisation von Verzeichnisinformationen.  
  
Dieser Datenspeicher, auch bekannt als das Verzeichnis enthält Informationen zu Active Directory-Objekte. Diese Objekte enthalten in der Regel freigegebene Ressourcen wie Server, Volumes, Drucker und die Netzwerk-Benutzer- und Computerkonten. Weitere Informationen zu den Active Directory-Datenspeicher, finden Sie unter [Verzeichnisdatenspeicher](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx).  
  
Sicherheit ist in Active Directory über die Anmeldeauthentifizierung und Steuerung des Zugriffs auf Objekte im Verzeichnis integriert. Klicken Sie mit einer einzigen netzwerkanmeldung können Administratoren Verzeichnisdaten und die Organisation im gesamten Netzwerk verwalten, und autorisierte Netzwerkbenutzer können Ressourcen im Netzwerk zugreifen. Durch die richtlinienbasierte Verwaltung wird selbst die Verwaltung der komplexesten Netzwerke erleichtert. Weitere Informationen zu Active Directory-Sicherheit finden Sie unter Übersicht über die Sicherheit.  
  
Active Directory enthält außerdem:  
* Eine Reihe von Regeln **Schema**, definiert die Klassen der Objekte und Attribute enthalten, dem Verzeichnis, Einschränkungen und Grenzwerte für Instanzen dieser Objekte und das Format ihrer Namen. Weitere Informationen zum Schema finden Sie unter "Schema".  
  
  
* Ein **globalen Katalog** , Informationen über jedes Objekt in das Verzeichnis enthält. Dadurch können Benutzer und Administratoren zum unabhängig davon, Suchen nach Verzeichnisinformationen von der Domäne in das Verzeichnis die Daten tatsächlich enthält. Weitere Informationen zu den globalen Katalog finden Sie unter der Rolle des globalen Katalogs.  
  
  
* Ein **Abfrage- und indexmechanismus**, sodass Objekte und ihre Eigenschaften veröffentlicht und von Netzwerkbenutzern bzw. Anwendungen gefunden werden können. Weitere Informationen zu das Verzeichnis Abfragen finden Sie in der Verzeichnisinformationen suchen.  
  
  
* Ein **Replikationsdienst** , die Verzeichnisdaten in einem Netzwerk verteilt. Alle Domänencontroller in einer Domäne Replikation beteiligt und enthalten eine vollständige Kopie aller Verzeichnisinformationen für ihre Domäne. Jede Änderung an den Verzeichnisdaten wird zu allen Domänencontrollern in der Domäne repliziert. Weitere Informationen zu Active Directory-Replikation finden Sie unter Übersicht über die Replikation.  
  
## <a name="understanding-active-directory"></a>Grundlegendes zur Active Directory  
 Dieser Abschnitt enthält Links zu den grundlegenden Active Directory-Konzepte:  
   
* [Struktur von Active Directory und Speichertechnologien](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)  
* [Domänen-Controller-Rollen](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* Active Directory-Schema   
* [Grundlegendes zu Vertrauensstellungen](https://technet.microsoft.com/library/cc771294(v=ws.10).aspx)   
* [Active Directory-Replikation-Technologien](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* [Active Directory-Suche und Veröffentlichung-Technologien](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx)   
* Zusammenarbeit mit DNS und der Gruppenrichtlinie   
* [Grundlegendes zum Schema](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx)   
  
Eine detaillierte Liste der Active Directory-Konzepte, finden Sie unter [Understanding Active Directory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx).   

