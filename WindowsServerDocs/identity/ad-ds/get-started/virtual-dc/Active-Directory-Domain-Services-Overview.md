---
ms.assetid: f052dfcd-dace-4485-8d0a-cc7df5cf3751
title: Übersicht über Active Directory Domain Services
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8087a6c7698952793546d6266a6a112bb810ac70
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88940330"
---
# <a name="active-directory-domain-services-overview"></a>Übersicht über Active Directory Domain Services

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


Ein Verzeichnis ist eine hierarchische Struktur, in der Informationen zu Objekten im Netzwerk gespeichert werden. Ein Verzeichnisdienst, wie z. b. Active Directory Domain Services (AD DS), stellt die Methoden zum Speichern von Verzeichnis Daten und zum Bereitstellen dieser Daten für Netzwerk Benutzer und Administratoren bereit. AD DS speichert beispielsweise Informationen über Benutzerkonten wie Namen, Kennwörter, Telefonnummern usw. und ermöglicht anderen autorisierten Benutzern im gleichen Netzwerk, auf diese Informationen zuzugreifen.

In Active Directory werden Informationen zu Objekten im Netzwerk gespeichert, sodass sie von Administratoren und Benutzern leicht gefunden und verwendet werden können. Für Active Directory wird ein strukturierter Datenspeicher als Basis für eine logische, hierarchische Organisation von Verzeichnisinformationen eingesetzt.

Dieser Datenspeicher, auch als Verzeichnis bezeichnet, enthält Informationen über Active Directory Objekte. Diese Objekte umfassen in der Regel freigegebene Ressourcen, z. b. Server, Volumes, Drucker und Netzwerk Benutzer-und Computer Konten. Weitere Informationen zum Active Directory Datenspeicher finden Sie unter [Verzeichnis Datenspeicher](/previous-versions/windows/it-pro/windows-server-2003/cc736627(v=ws.10)).

Die Sicherheit wird in Active Directory durch die Anmelde Authentifizierung und die Zugriffs Steuerung für Objekte im Verzeichnis integriert. Mit einer einzigen Netzwerkanmeldung können Administratoren Verzeichnisdaten und die Organisation im gesamten Netzwerk verwalten, und autorisierte Netzwerkbenutzer können überall im Netzwerk auf Ressourcen zugreifen. Durch die richtlinienbasierte Verwaltung wird selbst die Verwaltung der komplexesten Netzwerke erleichtert. Weitere Informationen zur Active Directory Sicherheit finden Sie unter [Sicherheitsübersicht](../../plan/security-best-practices/best-practices-for-securing-active-directory.md).

Active Directory umfasst auch Folgendes:
* Ein Satz von Regeln, **das Schema**, das die Klassen von Objekten und Attributen definiert, die im Verzeichnis enthalten sind, die Einschränkungen und Begrenzungen für Instanzen dieser Objekte und das Format ihrer Namen. Weitere Informationen zum Schema finden Sie unter Schema.


* Ein **globaler Katalog** , der Informationen zu jedem Objekt im Verzeichnis enthält. Dadurch können Benutzer und Administratoren Verzeichnisinformationen suchen, unabhängig davon, welche Domäne im Verzeichnis die Daten tatsächlich enthält. Weitere Informationen zum globalen Katalog finden Sie unter der Rolle des globalen Katalogs.


* Ein **Abfrage-und Index Mechanismus**, sodass Objekte und ihre Eigenschaften veröffentlicht und von Netzwerk Benutzern oder-Anwendungen gefunden werden können. Weitere Informationen zum Abfragen des Verzeichnisses finden Sie untersuchen von Verzeichnisinformationen.


* Ein **Replikations Dienst** , mit dem Verzeichnis Daten in einem Netzwerk verteilt werden. Alle Domänen Controller in einer Domäne nehmen an der Replikation Teil und enthalten eine vollständige Kopie aller Verzeichnisinformationen für Ihre Domäne. Jede Änderung an den Verzeichnisdaten wird zu allen Domänencontrollern in der Domäne repliziert. Weitere Informationen zur Active Directory Replikation finden Sie unter Übersicht über die Replikation.

## <a name="understanding-active-directory"></a>Grundlegendes zu Active Directory
 Dieser Abschnitt enthält Links zu den grundlegenden Active Directory Konzepten:

* [Active Directory Struktur und Speichertechnologien](/previous-versions/windows/it-pro/windows-server-2003/cc759186(v=ws.10))
* [Domänen Controller Rollen](/previous-versions/windows/it-pro/windows-server-2003/cc786438(v=ws.10))
* [Active Directory-Schema](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771796(v=ws.10))
* [Grundlegendes zu Vertrauensstellungen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771568(v=ws.10))
* [Active Directory Replikations Technologien](/previous-versions/windows/it-pro/windows-server-2003/cc776877(v=ws.10))
* [Technologien für die Active Directory Suche und Veröffentlichung](/previous-versions/windows/it-pro/windows-server-2003/cc775686(v=ws.10))
* [Interoperabilität mit DNS und Gruppenrichtlinie](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd197486(v=ws.10))
* [Grundlegendes zum Schema](/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10))

Eine ausführliche Liste der Active Directory Konzepte finden Sie unter [Understanding Active Directory](/previous-versions/windows/it-pro/windows-server-2003/cc781408(v=ws.10)).
