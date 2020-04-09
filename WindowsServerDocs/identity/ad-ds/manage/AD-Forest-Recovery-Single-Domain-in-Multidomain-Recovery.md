---
title: 'Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne in einer Gesamtstruktur mit mehreren'
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adds
ms.openlocfilehash: 13153358f50302de722109bfe101911e3bac4708
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823443"
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne in einer Gesamtstruktur mit mehreren

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Es kann vorkommen, dass es erforderlich ist, nur eine einzelne Domäne innerhalb einer Gesamtstruktur mit mehreren Domänen anstatt einer vollständigen Gesamtstruktur Wiederherstellung wiederherzustellen. In diesem Thema werden Überlegungen zum Wiederherstellen einer einzelnen Domäne und mögliche Strategien für die Wiederherstellung behandelt.  
  
Eine einzelne Domänen Wiederherstellung stellt eine besondere Herausforderung für die Neuerstellung von globalen Katalog Servern (GC) dar. Wenn beispielsweise der erste Domänen Controller (DC) für die Domäne aus einer Sicherung wieder hergestellt wird, die eine Woche früher erstellt wurde, verfügen alle anderen GCS in der Gesamtstruktur über aktuellere Daten für diese Domäne als der wiederhergestellte DC. Um die Konsistenz der GC-Daten wiederherzustellen, gibt es einige Optionen:  
  
- Die Partition der wiederhergestellten Domänen wird von allen GCS in der Gesamtstruktur, außer den in der wiederhergestellten Domäne, gleichzeitig aus-und neu gehostet.  
- Führen Sie den Wiederherstellungsprozess für die Gesamtstruktur aus, um die Domäne wiederherzustellen, und entfernen Sie dann veraltete Objekte aus GCS in anderen Domänen.  
  
In den folgenden Abschnitten finden Sie allgemeine Überlegungen zu den einzelnen Optionen. Der gesamte Satz von Schritten, die für die Wiederherstellung ausgeführt werden müssen, unterscheidet sich für verschiedene Active Directory Umgebungen.  
  
## <a name="rehost-all-gcs"></a>Alle GCS neu hosten  

> [!WARNING]
> Das Kennwort des Domänen Administrator Kontos für alle Domänen muss zur Verwendung bereit sein, falls ein Problem den Zugriff auf einen GC für die Anmeldung verhindert.  

Das erneute Hosting aller GCS kann mithilfe der Befehle repadmin/Unhost und repadmin/Rehost (Teil von Repadmin/experthelp) ausgeführt werden. Sie führen die repadmin-Befehle für jede GC in jeder Domäne aus, die nicht wieder hergestellt wird. Es muss sichergestellt werden, dass alle GCS eine Kopie der wiederhergestellten Domäne nicht mehr enthalten. Um dies zu erreichen, müssen Sie die Domänen Partition zuerst von allen Domänen Controllern für alle wiederhergestellten Domänen der Gesamtstruktur von allen Domänen Controllern aus Wenn die Partition nicht mehr in allen GCS enthalten ist, können Sie Sie neu hosten. Wenn Sie das erneute hosten durchführen, sollten Sie die Standort-und Replikations Struktur Ihrer Gesamtstruktur in Erwägung gezogen, indem Sie z. b. das erneute Hosten eines Domänen Controllers pro Standort abschließen, bevor Sie die anderen DCS dieses Standorts  
  
Diese Option kann für eine kleine Organisation vorteilhaft sein, die nur über einige Domänen Controller für jede Domäne verfügt. Alle GCS konnten an einer Freitagnacht neu erstellt werden und ggf. die Replikation für alle schreibgeschützten Domänen Partitionen vor Montagmorgen abzuschließen. Wenn Sie jedoch eine große Domäne wiederherstellen müssen, die Standorte auf der ganzen Welt abdeckt, kann das erneute Hosting der schreibgeschützten Domänen Partition auf allen GCS für andere Domänen den Betrieb erheblich beeinträchtigen und möglicherweise zu einer Verlangsamung der Zeit erforderlich sein.  
  
## <a name="remove-lingering-objects"></a>Veraltete Objekte entfernen

Ähnlich wie bei der Wiederherstellung in der Gesamtstruktur stellen Sie einen Domänen Controller aus einer Sicherung in der Domäne wieder her, die Sie wiederherstellen müssen, führen eine Metadatenbereinigung der verbleibenden DCS durch und installieren AD DS dann erneut, um die Domäne zu erstellen. In den GCS aller anderen Domänen in der Gesamtstruktur werden die veralteten Objekte für die schreibgeschützte Partition der wiederhergestellten Domäne entfernt.  

Die Quelle für das Bereinigung von veralteten Objekten muss in der wiederhergestellten Domäne ein Domänen Controller sein. Um sicherzustellen, dass der Quell Domänen Controller über keine veralteten Objekte für Domänen Partitionen verfügt, können Sie den globalen Katalog entfernen, wenn es sich um einen GC handelt.  

Das Entfernen veralteter Objekte ist für größere Unternehmen vorteilhaft, die die mit den anderen Optionen verbundene Zeitüberschreitung nicht riskieren können.  

Weitere Informationen finden Sie unter [Verwenden von Repadmin zum Entfernen](https://technet.microsoft.com/library/cc785298.aspx)veralteter Objekte.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [AD-Gesamtstruktur Wiederherstellung: Entwerfen eines benutzerdefinierten Wiederherstellungs Plans](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD-Gesamtstruktur Wiederherstellung: Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
- [AD-Gesamtstruktur Wiederherstellung: häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur mit mehreren](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Active Directory-Gesamtstruktur Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md)  
