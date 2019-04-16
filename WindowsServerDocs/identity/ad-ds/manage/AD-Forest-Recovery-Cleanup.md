---
title: Wiederherstellung der Active Directory-Gesamtstruktur - Bereinigung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 2f652d08304a17ecbfde51bbb6f35e4666cd9eca
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---cleanup"></a>Wiederherstellung der Active Directory-Gesamtstruktur - Bereinigung 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Führen Sie die folgenden Schritteder Post-Wiederherstellung, bei Bedarf:  
  
-   Nach der Wiederherstellung der Gesamtstruktur können Sie die ursprüngliche DNS-Konfiguration, einschließlich der Konfiguration der bevorzugten und alternativen DNS-Server auf jedem Domänencontroller wiederherstellen. Nachdem die DNS-Server konfiguriert sind, wie vor die Fehlfunktion, werden ihre vorherigen Name Resolution-Funktionen wiederhergestellt. Löschen Sie alle DNS-Einträge für Domänencontroller, die nicht wiederhergestellt wurden.  
  
-   Löschen von Windows Internet Name Service (WINS)-Einträge für alle Domänencontroller, die nicht wiederhergestellt wurden.  
  
-   Sie können übertragen der Betriebsmasterrollen zu einem anderen Domänencontroller in der Domäne oder Gesamtstruktur, und fügen weitere globale Katalogserver basierend auf der Konfiguration vor Auftreten des Fehlers.  
  
-   Da die Gesamtstruktur auf einen früheren Zustand wiederhergestellt wird, sind alle Objekte (z.B. Benutzer und Computer), die hinzugefügt wurden, und alle Updates (z.B. Kennwortänderungen), die nach diesem Zeitpunkt an bestehenden Objekten vorgenommen wurden verloren. Daher sollten Sie diese fehlende Objekte neu erstellen und erneut die fehlenden Updates nach Bedarf.  
  
-   Sie müssen auch ausgehende Vertrauensstellungen mit externen Domänen und Gesamtstrukturen, wiederherstellen, da diese externen Vertrauensstellungen von Sicherungen nicht automatisch wiederhergestellt werden.

## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  



