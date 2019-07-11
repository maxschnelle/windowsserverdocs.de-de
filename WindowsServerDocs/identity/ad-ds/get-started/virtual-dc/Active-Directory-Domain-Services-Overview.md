---
ms.assetid: f052dfcd-dace-4485-8d0a-cc7df5cf3751
title: Übersicht über Active Directory Domain Services
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ed8a22881cd20633e6fcd61b146f3b0aad7a757b
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792278"
---
# <a name="active-directory-domain-services-overview"></a>Übersicht über Active Directory Domain Services

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


Ein Verzeichnis ist eine hierarchische Struktur, die Informationen zu Objekten im Netzwerk gespeichert. Ein Verzeichnisdienst wie Active Directory Domain Services (AD DS), stellt die Methoden für die Speicherung von Verzeichnisdaten und die Verfügbarmachung dieses Daten für Netzwerkbenutzer und Administratoren bereit. Z. B. AD DS speichert Informationen über Benutzerkonten wie Namen, Kennwörter, Telefonnummern und So weiter, und ermöglicht anderen autorisierten Benutzern im selben Netzwerk auf diese Informationen zuzugreifen.

Active Directory speichert Informationen zu Objekten im Netzwerk und erleichtert diese Informationen für Administratoren und Benutzer suchen und verwenden. Active Directory verwendet einen strukturierter Datenspeicher als Grundlage für einen logischen, hierarchischen Organisation von Verzeichnisinformationen.

Dieser Datenspeicher, auch bekannt als das Verzeichnis enthält Informationen zu Active Directory-Objekte. Diese Objekte enthalten in der Regel freigegebene Ressourcen wie Server, Volumes, Drucker und die Netzwerk-Benutzer- und Computerkonten. Weitere Informationen zu den Active Directory-Datenspeicher, finden Sie unter [Verzeichnisdatenspeicher](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx).

Sicherheit ist in Active Directory über die Anmeldeauthentifizierung und Steuerung des Zugriffs auf Objekte im Verzeichnis integriert. Klicken Sie mit einer einzigen netzwerkanmeldung können Administratoren Verzeichnisdaten und die Organisation im gesamten Netzwerk verwalten, und autorisierte Netzwerkbenutzer können Ressourcen im Netzwerk zugreifen. Durch die richtlinienbasierte Verwaltung wird selbst die Verwaltung der komplexesten Netzwerke erleichtert. Weitere Informationen zu Active Directory-Sicherheit, finden Sie unter [Sicherheitsübersicht](../../plan/security-best-practices/best-practices-for-securing-active-directory.md).

Active Directory enthält außerdem:
* Eine Reihe von Regeln **Schema**, definiert die Klassen der Objekte und Attribute enthalten, dem Verzeichnis, Einschränkungen und Grenzwerte für Instanzen dieser Objekte und das Format ihrer Namen. Weitere Informationen zum Schema finden Sie unter "Schema".


* Ein **globalen Katalog** , Informationen über jedes Objekt in das Verzeichnis enthält. Dadurch können Benutzer und Administratoren zum unabhängig davon, Suchen nach Verzeichnisinformationen von der Domäne in das Verzeichnis die Daten tatsächlich enthält. Weitere Informationen zu den globalen Katalog finden Sie unter der Rolle des globalen Katalogs.


* Ein **Abfrage- und indexmechanismus**, sodass Objekte und ihre Eigenschaften veröffentlicht und von Netzwerkbenutzern bzw. Anwendungen gefunden werden können. Weitere Informationen zu das Verzeichnis Abfragen finden Sie in der Verzeichnisinformationen suchen.


* Ein **Replikationsdienst** , die Verzeichnisdaten in einem Netzwerk verteilt. Alle Domänencontroller in einer Domäne Replikation beteiligt und enthalten eine vollständige Kopie aller Verzeichnisinformationen für ihre Domäne. Jede Änderung an den Verzeichnisdaten wird zu allen Domänencontrollern in der Domäne repliziert. Weitere Informationen zu Active Directory-Replikation finden Sie unter Übersicht über die Replikation.

## <a name="understanding-active-directory"></a>Grundlegendes zur Active Directory
 Dieser Abschnitt enthält Links zu den grundlegenden Active Directory-Konzepte:
 
* [Struktur von Active Directory und Speichertechnologien](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)
* [Domänen-Controller-Rollen](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory-Schema](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771796(v=ws.10))
* [Grundlegendes zu Vertrauensstellungen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771568(v=ws.10)) 
* [Active Directory-Replikation-Technologien](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory-Suche und Veröffentlichung-Technologien](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx) 
* [Zusammenarbeit mit DNS und der Gruppenrichtlinie](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197486(v=ws.10))
* [Grundlegendes zum Schema](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx) 

Eine detaillierte Liste der Active Directory-Konzepte, finden Sie unter [Understanding Active Directory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx). 


