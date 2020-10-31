---
title: 'AD-Gesamtstruktur Wiederherstellung: autoritative Synchronisierung von SYSVOL'
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.openlocfilehash: 63b894e8abe0ac50f59f5ebf38566d97050a11c4
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068022"
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>AD-Gesamtstruktur Wiederherstellung: Ausführen einer autoritativen Synchronisierung von DFSR-replizierten SYSVOL

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Es gibt verschiedene Möglichkeiten, eine autoritative Wiederherstellung von SYSVOL auszuführen. Sie können entweder das Attribut **msdfsr-Options** bearbeiten oder mithilfe von Wbadmin – authsysvol eine Systemstatus Wiederherstellung durchführen. Wenn Sie die Möglichkeit haben, eine Systemstatus Sicherung wiederherzustellen (d. h., Sie stellen AD DS auf derselben Hardware-und Betriebssystem Instanz wieder her), ist die Verwendung von Wbadmin – authsysvol einfacher. Wenn Sie jedoch eine Bare-Metal-Wiederherstellung ausführen müssen, müssen Sie das **msdfsr-Options-** Attribut bearbeiten.

Führen Sie die folgenden Schritte aus, um eine autoritative Synchronisierung von SYSVOL auszuführen (bei Verwendung von DFSR), indem Sie das **msdfsr-Options-** Attribut bearbeiten. Wenn SYSVOL mithilfe von FRS repliziert wird, finden Sie weitere Informationen im [Artikel 290762](https://go.microsoft.com/fwlink/?LinkId=148443).

## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>So führen Sie eine autoritative Synchronisierung von DFSR-replizierten SYSVOL durch

1. Öffnen Sie „Active Directory-Benutzer und -Computer“.
2. Klicken Sie auf **anzeigen** , und wählen Sie dann **Benutzer, Kontakte, Gruppen und Computer als Container** und **Erweiterte Features** aus.

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png)

3. Klicken Sie in der Strukturansicht auf **Domänen Controller** , auf den Namen des wiederhergestellten DC, auf **DFSR-LocalSettings** und dann auf **Domänen System Volume** .

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)

4. Klicken Sie im Detailfenster mit der rechten Maustaste auf **SYSVOL-Abonnement** , klicken Sie auf **Eigenschaften** , und klicken Sie auf **Attribut-Editor** .

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png)

5. Klicken Sie auf **msdfsr-Options** , auf **Bearbeiten** , geben Sie **1 ein** , und klicken Sie auf **OK** .

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png)

6. Klicken Sie auf **OK** , um den Attribut Editor zu schließen.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
