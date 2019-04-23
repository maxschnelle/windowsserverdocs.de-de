---
title: 'AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne in einer Gesamtstruktur mit mehreren Domänen'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adds
ms.openlocfilehash: fae2cc40af0b43dd38d72c2622720a6bb17b0a66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863471"
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne in einer Gesamtstruktur mit mehreren Domänen

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Es kann Zeiten, in denen es erforderlich, die nur eine einzelne Domäne innerhalb einer Gesamtstruktur mit wiederherstellen, statt eine Wiederherstellung der vollständigen Gesamtstruktur mehrere Domänen vorhanden sein. In diesem Thema werden Überlegungen zum Wiederherstellen einer einzelnen Domäne und mögliche Strategien für die Wiederherstellung behandelt.  
  
Eine einzelne Domäne Recovery stellt eine besondere Herausforderung für die Neuerstellung der globalen Katalogserver (GC). Wenn der erste Domänencontroller (DC) für die Domäne aus einer Sicherung, die eine Woche früher erstellt wurde, und klicken Sie dann auf alle anderen GCs, die in der Gesamtstruktur wiederhergestellt wird z. B. müssen weitere aktuellen Daten für diese Domäne als dem wiederhergestellten DC. Um die Konsistenz der GC-Daten erneut hergestellt haben, stehen einige Optionen zur Verfügung:  
  
- Unhost, und klicken Sie dann die wiederhergestellte Domänen Partition über alle globalen Kataloge in der Gesamtstruktur, mit Ausnahme derjenigen in der wiederhergestellten gleichzeitig hosten.  
- Führen Sie zum Wiederherstellen der Domänenadministrators den Gesamtstruktur-Wiederherstellungsprozess, und klicken Sie dann entfernen Sie veralteter Objekte aus GCs in anderen Domänen.  
  
Die folgenden Abschnitte enthalten allgemeine Informationen für jede Option. Der vollständige Satz der Schritte, die für die Wiederherstellung ausgeführt werden müssen, variieren für Active Directory-Umgebungen.  
  
## <a name="rehost-all-gcs"></a>Alle globalen Kataloge rehosten  

> [!WARNING]
> Das Kennwort für das Domänenadministratorkonto für alle Domänen muss zur Verwendung bereit sein, für den Fall, dass Sie den Zugriff mit einem globalen Katalogserver für die Anmeldung aufgrund eines Problems.  

Erneutes hosten aller globalen Kataloge erfolgen mithilfe von Repadmin / unhost und Repadmin /rehost Befehle (Teil von Repadmin/experthelp). Sie würden das Repadmin-Befehle auf alle globalen Katalogserver in jeder Domäne ausführen, die nicht wiederhergestellt wird. Es muss sichergestellt werden kann; die eine Kopie der wiederhergestellten Domäne auf alle globalen Kataloge nicht mehr geeignet sind. Um dies zu erreichen, unhost der Domänenpartition zunächst von allen Domänencontrollern in allen keine wiederhergestellten Domänen der Gesamtstruktur zuerst. Nachdem alle globalen Kataloge nicht die Partition nicht mehr enthalten, können Sie es zum erneuten hosten. Beim erneuten hosten, sollten Sie die Website und Replikation-Struktur der Gesamtstruktur, z. B., Fertig stellen Sie, die zum erneuten Hosten von einem Domänencontroller für den Standort vor dem rehosting von den anderen DCs dieses Standorts.  
  
Diese Option kann für eine kleine Organisation vorteilhaft sein, die nur wenige Domänencontroller für jede Domäne verfügt. Alle der kann auf einen Freitag Abend neu erstellt werden, und bei Bedarf vollständige Replikation für alle schreibgeschützten Partitionen, bevor Sie am Montag wieder hoch. Wenn Sie möchten eine große Domäne wiederherstellen, die Websites auf der ganzen Welt abdeckt, Erneutes hosten die schreibgeschützten Partitionen auf alle globalen Kataloge für andere Domänen können jedoch erheblich Auswirkungen auf Vorgänge und muss möglicherweise außer Betrieb genommen.  
  
## <a name="remove-lingering-objects"></a>Entfernen von veralteten Objekten

Ähnlich wie der Wiederherstellungsprozess Gesamtstruktur, stellen Sie einen DC aus einer Sicherung in der Domäne, die Sie wiederherstellen, Metadatenbereinigung der restlichen Domänencontroller ausführen und anschließend AD DS erstellen, der Domäne erneut installieren müssen. Klicken Sie auf die globalen Kataloge aller anderen Domänen in der Gesamtstruktur entfernen Sie die veralteten Objekte für die Partition "schreibgeschützt" der wiederhergestellten Domäne.  

Die Quelle für die Bereinigung der veralteten Objekte muss es sich um einen Domänencontroller in der wiederhergestellten Domäne sein. Um sicherzustellen, dass der Quell-DC keine veralteten Objekte für alle Domänenpartitionen verfügt, können Sie den globalen Katalog entfernen, wenn es sich um einen globalen Katalog war.  

Entfernen veralteter Objekte ist für größere Organisationen, die den nach-unten-Zeit im Zusammenhang mit den anderen Optionen besteht das Risiko, können nicht vorteilhaft.  

Weitere Informationen finden Sie unter [zum Entfernen veralteter Objekte mithilfe von Repadmin](https://technet.microsoft.com/library/cc785298.aspx).

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der Gesamtstruktur der Active Directory - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten eines Wiederherstellungsplans für die benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Gesamtstruktur des Active Directory - Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur-Wiederherstellung: Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md)  
