---
title: Wiederherstellung der Active Directory-Gesamtstruktur - autoritative Synchronisierung von SYSVOL
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.technology: identity-adds
ms.openlocfilehash: 246a2ea589ee05110362cff99d50e93a0a18c2b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827001"
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>AD-Gesamtstruktur-Wiederherstellung: Ausführen einer autoritativen Synchronisierung des DFSR-repliziertes SYSVOL  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Es gibt verschiedene Möglichkeiten zum Durchführen einer autorisierenden Wiederherstellung von SYSVOL. Sie können entweder Bearbeiten der **MsDFSR-Optionen** Attribut, oder führen eine systemstatuswiederherstellung mit Wbadmin – Authsysvol. Wenn Sie die Option zum Wiederherstellen einer systemstatussicherung verfügen (d. h. sind Sie AD DS mit der gleichen Hardware und Betriebssystem-Instanz wiederherstellen) und dann mit Wbadmin – Authsysvol einfacher ist. Aber wenn Sie eine bare-Metal-Wiederherstellung ausführen müssen, müssen Sie so bearbeiten Sie die **MsDFSR-Optionen** Attribut.  

Gehen Sie folgendermaßen vor, eine autoritative Synchronisierung von SYSVOL durchführen (wenn es mit dem über DFSR repliziert wird), durch Bearbeiten der **MsDFSR-Optionen** Attribut. Wenn Sie SYSVOL über FRS repliziert werden, finden Sie unter [Artikel 290762](https://go.microsoft.com/fwlink/?LinkId=148443).  

## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>Um eine autorisierende Synchronisierung der DFSR-repliziertes SYSVOL auszuführen.  

1. Öffnen Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;.  
2. Klicken Sie auf **Ansicht**, und wählen Sie dann **Benutzer, Kontakte, Gruppen und Computer als Container** und **erweiterte Features**. 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png) 

3. Klicken Sie in der Strukturansicht auf **Domänencontroller**, den Namen des Domänencontrollers, der Sie wiederhergestellt, **DFSR-LocalSettings**, und klicken Sie dann **Systemvolume der Domäne**. 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)  

4. Klicken Sie im Detailbereich mit der Maustaste **SYSVOL-Abonnement**, klicken Sie auf **Eigenschaften**, und klicken Sie auf **Attribut-Editor**.  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png) 

5. Klicken Sie auf **MsDFSR-Optionen**, klicken Sie auf **bearbeiten**, Typ **1**, und klicken Sie auf **OK**  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png) 

6. Klicken Sie auf **OK** um Attribut-Editor zu schließen.  
  
## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
