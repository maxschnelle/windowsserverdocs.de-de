---
title: "Ändern der Reihenfolge und Gruppierung von Registerkarten"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79a417fd-1b3e-47ab-ae33-bb1faf95c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 578c5619cfdf076bb2735254494f393d56d35713
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="change-the-order-and-grouping-of-tabs"></a>Ändern der Reihenfolge und Gruppierung von Registerkarten

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können die Reihenfolge der Registerkarten im Dashboard ändern, sodass Ihre Registerkarte die erste (auf der linken Seite) in der Reihe der Registerkarten ist. Zu diesem Zweck fügen Sie einen Eintrag in der Registrierung. Sie können auch die Gruppierung von Registerkarten beeinflussen, indem Sie Einträge zur Registrierung hinzufügen. Die Reihenfolge der Registerkarten kann Ihre Hauptregisterkarte, gefolgt von integrierten Microsoft-Registerkarten, gefolgt von Ihren weiteren Registerkarten, und dann durch Drittanbieter-Registerkarten werden.  
  
## <a name="change-the-order-of-the-tabs-in-the-dashboard"></a>Ändern der Reihenfolge der Registerkarten im Dashboard  
 Sie müssen den Bezeichner des Add-Ins hinzufügen, die Ihre Registerkarte, zu der Registrierung anzeigt, um die Reihenfolge zu definieren.  
  
#### <a name="to-display-your-tab-first-in-the-list-of-tabs"></a>Um Ihre Registerkarte zuerst in der Liste der Registerkarten anzuzeigen  
  
1.  Klicken Sie auf dem Referenzcomputer auf **starten**, geben Sie **Regedit**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, und erweitern Sie dann **Windows Server**. Wenn die **OEM** Schlüssel ist nicht vorhanden, müssen Sie die folgenden Schritte aus, um ihn zu erstellen:  
  
    1.  Mit der rechten Maustaste **Windows Server**, zeigen Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Typ **OEM** für den Namen des Schlüssels.  
  
3.  Mit der rechten Maustaste **OEM**, zeigen Sie auf **neu**, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
4.  Typ **DashboardMainTabID** als Zeichenfolgennamen ein, und drücken Sie dann die **EINGABETASTE**.  
  
5.  Mit der rechten Maustaste im rechten Bereich der neuen Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
6.  Geben Sie die GUID, die für die Registerkarte der obersten Ebene definiert wurde, und drücken Sie dann die **EINGABETASTE**.  
  
     Weitere Informationen zum Erstellen und Identifizieren von Registerkarten der obersten Ebene finden Sie unter [Erstellen einer Registerkarte der obersten Ebene](https://msdn.microsoft.com/library/gg513957) im SDK für Windows Server Solutions.  
  
7.  Speichern Sie die Änderungen an der Registrierung.  
  
8.  Sie müssen auch die GUID für Ihre Hauptregisterkarte der obersten Ebene in der Liste der Bezeichner zum Gruppieren von Registerkarten aufnehmen. Führen Sie dazu die Schritte in **Ändern der Gruppierung von Registerkarten im Dashboard**.  
  
## <a name="change-the-grouping-of-tabs-in-the-dashboard"></a>Ändern der Gruppierung von Registerkarten im Dashboard  
 Sie können sicherstellen, dass Ihre Registerkarten gruppiert und in der Liste der integrierten Microsoft-Registerkarten, indem Sie der Registrierung die Bezeichner hinzufügen enthalten sind.  
  
#### <a name="to-change-the-grouping-of-tabs"></a>So ändern Sie die Gruppierung von Registerkarten  
  
1.  Wenn "regedit" nicht geöffnet ist, klicken Sie auf **starten**, geben Sie **Regedit**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, und erweitern Sie dann **Windows Server**.  
  
3.  Mit der rechten Maustaste **OEM**, zeigen Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.  
  
4.  Typ **DashboardAddins** als Schlüsselnamen ein, und drücken Sie dann die **EINGABETASTE**.  
  
5.  Mit der rechten Maustaste **DashboardAddins**, zeigen Sie auf **neu**, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
6.  Geben Sie die GUID für Ihre Registerkarte als Zeichenfolge ein. Ein Wert ist nicht erforderlich.  
  
7.  Wiederholen Sie die Schritte 5 und 6 für jede der Registerkarten und Unterregisterkarten.  
  
8.  Speichern Sie Änderungen an der Registrierung.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)