---
title: Wiederherstellung der Active Directory-Gesamtstruktur - autoritative Synchronisierung von SYSVOL
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.technology: identity-adfs
ms.openlocfilehash: 5bdc619ddf9f28fb074e90dfbf22a7be076a05d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>AD-Gesamtstruktur-Wiederherstellung – führt eine autorisierende Synchronisation der DFSR-repliziertes SYSVOL  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Es gibt verschiedene Möglichkeiten, eine autorisierende Wiederherstellung von SYSVOL durchführen. Sie können entweder die **MsDFSR-Optionen** Attribut, oder führen Sie die Wiederherstellung des Systemstatus mit Wbadmin – Authsysvol. Wenn Sie die Option zum Wiederherstellen einer systemstatussicherung haben (d.h., sind Sie AD DS auf die gleiche Hardware und Betriebssystem-Instanz wiederherstellen) und dann mit Wbadmin – Authsysvol einfacher ist. Aber wenn Sie eine bare-Metal-Recovery ausführen müssen, müssen Sie bearbeiten die **MsDFSR-Optionen** Attribut.  
  
 Gehen Sie folgendermaßen eine autoritative Synchronisierung von SYSVOL durchführen (sofern er über DFSR repliziert wird), durch Bearbeiten der **MsDFSR-Optionen** Attribut. Wenn SYSVOL über FRS repliziert wird, finden Sie unter [Artikel 290762](https://go.microsoft.com/fwlink/?LinkId=148443).  
  
## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>Eine autoritative Synchronisierung von DFSR-repliziertes SYSVOL durchführen  
  
1.  Active Directory-Benutzer und -Computer zu öffnen.  
2.  Klicken Sie auf **Ansicht**, und wählen Sie dann **Benutzer, Kontakte, Gruppen und Computer als Container** und **erweiterte Funktionen**. 
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png) 
3.  Klicken Sie in der Strukturansicht auf **Domänencontroller**, den Namen der Domänencontroller, der Sie wiederhergestellt, **DFSR-LocalSettings**, und klicken Sie dann **Domain System Volume**. 
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)  
4.  Klicken Sie im Detailbereich mit der rechten Maustaste **SYSVOL-Abonnement**, klicken Sie auf **Eigenschaften**, und klicken Sie auf **Attribut-Editor**.  
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png) 
5.  Klicken Sie auf **MsDFSR-Optionen**, klicken Sie auf **bearbeiten**, Typ **1**, und klicken Sie auf **OK**  
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png) 
6.  Klicken Sie auf **OK** Attribut-Editor zu schließen.  
  
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
