---
title: "AD-Gesamtstruktur-Wiederherstellung – das Krbtgt-Kennwort zurücksetzen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adfs
ms.openlocfilehash: 445fa18503e26d04e20a61cfe652424f78631abe
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>AD-Gesamtstruktur-Wiederherstellung – das Krbtgt-Kennwort zurücksetzen 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Verwenden Sie das folgende Verfahren, um das Krbtgt-Kennwort für die Domäne zurückzusetzen. Das folgende Verfahren betrifft beschreibbaren Domänencontroller, aber keine schreibgeschützten Domänencontrollern (RODCs).  
  
> [!IMPORTANT]
>  Wenn Sie RODCs online während der Wiederherstellung der Gesamtstruktur wiederherstellen möchten, löschen Sie das Krbtgt-Konten für die RODCs. Das Krbtgt-Konto für einen RODC ist aufgeführt, in dem Format Krbtgt_*Anzahl*.  
>   
>  Wenn Sie einen benutzerdefiniertes Kennwortfilter (z.B. passfilt.dll) auf einem Domänencontroller verwenden, können Sie einen Fehler erhalten, wenn Sie versuchen, das Krbtgt-Kennwort zurücksetzen. Weitere Informationen, einschließlich dieses Problem zu umgehen, finden Sie im Microsoft Knowledge Base [Artikel 2549833](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833).  
  
## <a name="to-reset-the-krbtgt-password"></a>Das Krbtgt-Kennwort zurücksetzen  
  
1.  Klicken Sie auf **starten**, zeigen Sie auf **Systemsteuerung**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.  
2.  2.  Klicken Sie auf **Ansicht**, und klicken Sie dann auf **erweiterte Funktionen**.  
3.  In der Konsolenstruktur, doppelklicken Sie auf den Domänencontainer, und klicken Sie dann auf **Benutzer**.  
4.  Klicken Sie im Detailbereich mit der rechten Maustaste die **Krbtgt** Benutzerkonto ein, und klicken Sie dann auf **Kennwort zurücksetzen**.  
![Zurücksetzen des Kennworts](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5.  In **neues Kennwort**, geben Sie ein neues Kennwort ein, das Kennwort in **Kennwort bestätigen**, und klicken Sie dann auf **OK**. Das Kennwort, das Sie angeben, ist nicht wichtig, da das System ein sicheres Kennwort für das Kennwort automatisch unabhängig generiert wird, die Sie angeben.  
  
    > [!NOTE]
    >  Sie sollten diesen Vorgang zweimal ausführen. Die Kennwortchronik des Krbtgt-Kontos ist zwei, was bedeutet, dass sie die beiden letzten Kennwörter enthält. Durch Zurücksetzen des Kennworts zweimal effektiv alte Kennwörter aus dem Verlauf löschen, daher keine Möglichkeit besteht, repliziert einem anderen Domänencontroller mit diesen Domänencontroller ein altes Kennwort mit.  
 
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md) 
  
