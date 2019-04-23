---
title: Wiederherstellung der Gesamtstruktur der Active Directory - Bereinigung
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: fa7193cc800eac0fee6425a66bd5cd82d8c822c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868961"
---
# <a name="ad-forest-recovery---cleanup"></a>Wiederherstellung der Gesamtstruktur der Active Directory - Bereinigung

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Führen Sie die folgenden Nachbearbeitungsschritte der Wiederherstellung, je nach Bedarf:  
  
- Nach der Wiederherstellung der Gesamtstruktur ist, können Sie die ursprünglichen DNS-Konfiguration, einschließlich der Konfiguration von der bevorzugten und alternativen DNS-Server auf jedem Domänencontroller wiederherstellen. Nachdem die DNS-Server wie vor der Fehlfunktion konfiguriert wurden, werden ihre vorherigen Name Resolution-Funktionen wiederhergestellt. Löschen Sie alle DNS-Einträge für Domänencontroller, die nicht wiederhergestellt wurden.  
- Löschen von Windows Internet Name Service (WINS)-Datensätze für alle Domänencontroller, die nicht wiederhergestellt wurden.  
- Sie können die Betriebsmasterrollen auf anderen DCs in der Domäne oder Gesamtstruktur übertragen und Hinzufügen von mehr globale Katalogserver, die auf Basis der Konfiguration vor Auftreten des Fehlers.  
- Weil die Gesamtstruktur auf einen früheren Zustand wiederhergestellt wird, gehen verloren, beliebige Objekte (z. B. Benutzer und Computer), die hinzugefügt wurden und alle Updates (z. B. kennwortänderungen), die nach diesem Zeitpunkt an bestehenden Objekten vorgenommen wurden. Aus diesem Grund sollten Sie diese fehlenden Objekte neu erstellen und erneut anwenden fehlender Updates nach Bedarf.  
- Sie sollten auch ausgehende Vertrauensstellungen mit externen Domänen und Gesamtstrukturen, wiederherstellen, da diese externen Vertrauensstellungen nicht automatisch aus Sicherungen wiederhergestellt werden.

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
