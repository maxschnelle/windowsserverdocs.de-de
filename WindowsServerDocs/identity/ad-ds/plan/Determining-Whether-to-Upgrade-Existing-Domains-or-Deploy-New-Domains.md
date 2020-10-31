---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: Bestimmen, ob vorhandene Domänen aktualisiert oder neue Domänen bereitgestellt werden sollen
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 2b7a1bcc6bb157c91b32edd9d4465ac54fb1ea42
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069212"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>Bestimmen, ob vorhandene Domänen aktualisiert oder neue Domänen bereitgestellt werden sollen

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Jede Domäne in Ihrem Entwurf ist entweder eine neue Domäne oder eine vorhandene aktualisierte Domäne. Benutzer aus vorhandenen Domänen, die Sie nicht aktualisieren, müssen in neue Domänen verschoben werden.

Das Verschieben von Konten zwischen Domänen kann sich auf Endbenutzer auswirken. Bevor Sie entscheiden, ob Sie Benutzer in eine neue Domäne verschieben oder vorhandene Domänen aktualisieren möchten, bewerten Sie die langfristigen administrativen Vorteile einer neuen AD DS Domäne mit den Kosten für das Verschieben von Benutzern in die Domäne.

Weitere Informationen zum Aktualisieren von Active Directory Domänen auf Windows Server 2008 finden Sie unter [Aktualisieren von Active Directory Domänen auf Windows Server 2008 und Windows Server 2008 R2 AD DS Domänen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731188(v=ws.10)).

Weitere Informationen zur Umstrukturierung von AD DS Domänen innerhalb von und zwischen Gesamtstrukturen finden Sie unter [ADMT Guide: Migrieren und umstrukturieren von Active Directory Domänen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10)).

Für ein Arbeitsblatt, das Sie bei der Dokumentation Ihrer Pläne für neue und aktualisierte Domänen unterstützt, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus den [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608) herunter, und öffnen Sie "Domänen Planung" (DSSLOGI_5.doc).
