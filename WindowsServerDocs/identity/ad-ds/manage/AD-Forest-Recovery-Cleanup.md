---
title: AD-Gesamtstruktur Wiederherstellung-Bereinigung
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 205c71930c14ef42596b0e08c27abae6646e4ddf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824153"
---
# <a name="ad-forest-recovery---cleanup"></a>AD-Gesamtstruktur Wiederherstellung-Bereinigung

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Führen Sie nach Bedarf die folgenden Schritte nach der Wiederherstellung aus:  
  
- Nachdem die gesamte Gesamtstruktur wieder hergestellt wurde, können Sie die ursprüngliche DNS-Konfiguration wiederherstellen, einschließlich der Konfiguration der bevorzugten und alternativen DNS-Server auf den einzelnen DCS. Nachdem die DNS-Server so konfiguriert wurden, wie Sie vor der Fehlfunktion waren, werden die zuvor beschriebenen Funktionen zur Namensauflösung wieder hergestellt. Löschen Sie alle DNS-Einträge für DCS, die nicht wieder hergestellt wurden.  
- Löschen Sie Windows Internet Name Service (WINS)-Einträge für alle DCS, die noch nicht wieder hergestellt wurden.  
- Sie können die Betriebs Master Rollen auf andere DCS in der Domäne oder Gesamtstruktur übertragen und vor dem Auftreten des Fehlers weitere globale Katalogserver basierend auf der Konfiguration hinzufügen.  
- Da die Gesamtstruktur in einem vorherigen Zustand wieder hergestellt wird, gehen alle Objekte (z. b. Benutzer und Computer), die hinzugefügt wurden, und alle Updates (z. b. Kenn Wort Änderungen), die nach diesem Punkt an vorhandenen Objekten vorgenommen wurden, verloren. Daher sollten Sie diese fehlenden Objekte neu erstellen und die fehlenden Updates nach Bedarf erneut anwenden.  
- Möglicherweise müssen Sie auch ausgehende Vertrauens Stellungen mit externen Domänen und Gesamtstrukturen wiederherstellen, da diese externen Vertrauens Stellungen nicht automatisch aus Sicherungen wieder hergestellt werden.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
