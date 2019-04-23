---
title: 'AD-Gesamtstruktur-Wiederherstellung: das Krbtgt-Kennwort zurücksetzen'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adds
ms.openlocfilehash: 1ac0dcb9da1d10a417c128cb8498a5d8362d9a9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883741"
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>AD-Gesamtstruktur-Wiederherstellung: das Krbtgt-Kennwort zurücksetzen

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren zum Zurücksetzen des Kennworts "Krbtgt" für die Domäne ein. Das folgende Verfahren gilt beschreibbaren DCs, aber nicht schreibgeschützten Domänencontrollern (RODCs).
  
> [!IMPORTANT]
> Wenn Sie RODCs online während der Wiederherstellung der Gesamtstruktur wiederherstellen möchten, löschen Sie die Krbtgt-Konten nicht für die RODCs. Das Krbtgt-Konto für einen RODC ist aufgeführt, in dem Format Krbtgt_*Anzahl*.
>
> Wenn Sie einen benutzerdefiniertes Kennwort-Filter (z. B. passfilt.dll) auf einem Domänencontroller verwenden, klicken Sie dann Sie erhalten möglicherweise eine Fehlermeldung beim Versuch, das Krbtgt-Kennwort zurückzusetzen. Weitere Informationen einschließlich dieses Problem zu umgehen, finden Sie unter Microsoft Knowledge Base [Artikel 2549833](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833).
  
## <a name="to-reset-the-krbtgt-password"></a>Das Krbtgt-Kennwort zurücksetzen  
  
1. Klicken Sie auf **starten**, zeigen Sie auf **Systemsteuerung**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**.
2. Klicken Sie auf **Ansicht** und dann auf **Erweiterte Funktionen**.
3. Klicken Sie in der Konsolenstruktur, doppelklicken Sie auf den Domänencontainer, und klicken Sie dann auf **Benutzer**.
4. Klicken Sie im Detailbereich mit der Maustaste der **Krbtgt** Benutzerkonto ein, und klicken Sie dann auf **Kennwort zurücksetzen**.
   ![Zurücksetzen des Kennworts](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5. In **neues Kennwort**, ein neues Kennwort ein, geben Sie das Kennwort erneut ein **Bestätigungskennwort**, und klicken Sie dann auf **OK**. Das Kennwort, das Sie angeben, ist nicht erheblich, da das System ein sicheres Kennwort das Kennwort automatisch unabhängig erstellt, die Sie angeben.
  
> [!NOTE]
> Sie sollten diesen Vorgang wird zweimal ausführen. Der Kennwortverlauf des Krbtgt-Kontos ist zwei, was bedeutet, dass sie die beiden letzten Kennwörter enthält. Durch Zurücksetzen des Kennworts zweimal Sie effektiv alte Kennwörter aus dem Verlauf löschen, daher keine Möglichkeit besteht wird einem anderen Domänencontroller mit diesem Domänencontroller replizieren mithilfe von einem alten Kennwort.

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md) 
