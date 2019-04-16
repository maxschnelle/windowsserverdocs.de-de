---
title: Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne in einer Gesamtstruktur mit mehreren Domänen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adfs
ms.openlocfilehash: 3a1c9d0671a732eee83aa707e061afdbbf106fa5
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/12/2018
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne in einer Gesamtstruktur mit mehreren Domänen

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

Gelegentlich es erforderlich ist, um nur eine einzige Domäne innerhalb einer Gesamtstruktur mit wiederherstellen, mehrere Domänen, anstatt eine vollständige Gesamtstruktur-Wiederherstellung möglich. In diesem Thema werden Überlegungen zur Wiederherstellung von einer einzelnen Domäne und Strategien für die Wiederherstellung behandelt.  
  
 Eine einzelne Domäne Wiederherstellung stellt eine besondere Herausforderung für die Neuerstellung der globale Katalogserver (GC). Wenn beispielsweise der erste Domänencontroller (DC) für die Domäne wiederhergestellt wird, aus einer Sicherung, die vor einer Woche erstellt wurde, und klicken Sie dann auf alle anderen globalen Kataloge in der Gesamtstruktur haben mehr auf dem neuesten Stand Daten für diese Domäne als der wiederhergestellten Domänencontroller. Um GC Datenkonsistenz wiederherzustellen, stehen einige Optionen zur Verfügung:  
  
-   Unhost, und klicken Sie dann die wiederhergestellte Domänen Partition über alle globalen Kataloge in der Gesamtstruktur, außer in der Domäne wiederhergestellten gleichzeitig rehost.  
  
-   Führen Sie das Verfahren zum Wiederherstellen von Gesamtstrukturen zum Wiederherstellen der Domänenbenutzers, und entfernen Sie veraltete Objekte aus der globalen Kataloge in anderen Domänen.  
  
 Die folgenden Abschnitte enthalten allgemeine Informationen für jede Option. Der vollständige Satz von Schritten, die für die Wiederherstellung ausgeführt werden, variiert für andere Active Directory-Umgebungen.  
  
## <a name="rehost-all-gcs"></a>Alle globalen Kataloge rehost  

> [!WARNING]
>  Das Kennwort des Kontos Domänenadministrator für alle Domänen muss verwendet werden, für den Fall, dass ein Problem mit einem globalen Katalogserver für die Anmeldung Zugriff verhindert.  

 Erneuten Hosten alle globalen Kataloge erfolgen mithilfe von Repadmin//unhost und Repadmin /rehost Befehle (Teil von "Repadmin" /experthelp). Sie würden das Repadmin-Befehle auf GC in jeder Domäne ausführen, die nicht wiederhergestellt werden. Es muss sichergestellt werden kann; die alle globalen Kataloge eine Kopie der wiederhergestellten Domäne nicht mehr enthalten. Um dies zu erreichen, unhost der Domänenpartition zunächst von allen Domänencontrollern in allen keine wiederhergestellte Domänen der Gesamtstruktur zuerst. Nachdem alle globalen Kataloge die Partition nicht mehr enthalten, können Sie es rehost. Beim erneuten hosten, sollten Sie die Website und Replikation-Struktur der Gesamtstruktur, z.B., abzuschließen Sie die mit erneutem Hosten eines Domänencontrollers pro Standort vor dem erneuten Hosten die anderen Domänencontroller dieses Standorts.  
  
 Diese Option kann für ein kleines Unternehmen vorteilhaft sein, die nur wenige Domänencontroller für jede Domäne verfügt. Alle von der globalen Kataloge konnte auf einem nachts Freitag neu erstellt werden, und bei Bedarf Partitionen Replikation für alle schreibgeschützten vor am Montagmorgen. Wenn Sie eine große Domäne wiederherstellen, in der Standorte in der ganzen Welt werden müssen, erneuten Hosten die RODC-Partition auf alle globalen Kataloge für die anderen Domänen können jedoch erheblich Auswirkungen Vorgänge und potenziell Ausfallzeit erforderlich.  
  
## <a name="remove-lingering-objects"></a>Entfernen veralteter Objekte  
 Ähnlich wie der Wiederherstellungsprozess für die Gesamtstruktur, stellen Sie her ein Domänencontroller aus einer Sicherung in der Domäne, die Sie wiederherstellen, Metadatenbereinigung des verbleibenden Domänencontroller ausführen und anschließend AD DS erstellen, der Domäne erneut installieren müssen. Auf der globalen Kataloge aller anderen Domänen in der Gesamtstruktur entfernen Sie die veralteten Objekte für die nur-Lese-Partition der wiederhergestellten Domäne.  
  
 Die Quelle für die veralteten Objekt Bereinigung muss ein Domänencontroller in der wiederhergestellten Domäne sein. Um sicherzustellen, dass der Quelldomänencontroller keine veralteten Objekte für alle Domänenpartitionen verfügt, können Sie den globalen Katalog entfernen, wenn kein globaler Katalogserver war.  
  
 Beim Entfernen veralteter Objekte ist von Vorteil für größere Unternehmen, die die Verbindung mit anderen Optionen Zeit sollte.  
  
 Weitere Informationen finden Sie unter [mit Repadmin zum Entfernen veralteter Objekte](https://technet.microsoft.com/library/cc785298.aspx).

## <a name="next-steps"></a>Nächste Schritte
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md)  
