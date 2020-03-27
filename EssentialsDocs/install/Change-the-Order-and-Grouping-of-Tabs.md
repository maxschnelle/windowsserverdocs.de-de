---
title: Ändern der Reihenfolge und der Gruppierung von Registerkarten
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79a417fd-1b3e-47ab-ae33-bb1faf95c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: abb443994b413f35f6d70510191bc543fad418f5
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312236"
---
# <a name="change-the-order-and-grouping-of-tabs"></a>Ändern der Reihenfolge und der Gruppierung von Registerkarten

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können die Reihenfolge der Registerkarten im Dashboard ändern, damit Ihre Registerkarte die erste (auf der linken Seite) in der Reihe von Registerkarten ist. Dazu fügen Sie der Registrierung einen Eintrag hinzu. Sie können auch die Gruppierung von Registerkarten beeinflussen, indem Sie der Registrierung Einträge hinzufügen. Mögliche Reihenfolge der Registerkarten: Ihre Hauptregisterkarte, gefolgt von integrierten Microsoft-Registerkarten, gefolgt von Ihren weiteren Registerkarten, gefolgt von Registerkarten von Drittanbietern.  
  
## <a name="change-the-order-of-the-tabs-in-the-dashboard"></a>Ändern der Reihenfolge der Registerkarten im Dashboard  
 Sie müssen der Registrierung den Bezeichner des Add-Ins hinzufügen, das Ihre Registerkarte anzeigt, um die Reihenfolge zu definieren.  
  
#### <a name="to-display-your-tab-first-in-the-list-of-tabs"></a>So wird Ihre Registerkarte als erste in der Liste der Registerkarten angezeigt  
  
1.  Klicken Sie auf dem Referenzcomputer auf **Start**, geben Sie **regedit** ein, und drücken Sie die **Eingabetaste**.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, **SOFTWARE**, dann **Microsoft** und schließlich **Windows Server**. Wenn der Schlüssel **OEM** nicht vorhanden ist, müssen Sie ihn mit den folgenden Schritten erstellen:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Geben Sie **OEM** als Namen des Schlüssels ein.  
  
3.  Klicken Sie mit der rechten Maustaste auf **OEM**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
4.  Geben Sie **DashboardMainTabID** als Zeichenfolgennamen ein, und drücken Sie dann die **EINGABETASTE**.  
  
5.  Klicken Sie im rechten Fensterbereich mit der rechten Maustaste auf die neue Zeichenfolge, und klicken Sie anschließend auf **Ändern**.  
  
6.  Geben Sie die GUID ein, die für die Registerkarte der obersten Ebene definiert wurde, und drücken Sie dann die**EINGABETASTE**.  
  
     Weitere Informationen zum Erstellen und Identifizieren von Registerkarten der obersten Ebene finden Sie unter [Erstellen einer Registerkarte der obersten Ebene](https://msdn.microsoft.com/library/gg513957) im SDK für Windows Server-Lösungen.  
  
7.  Speichern Sie die Änderungen an der Registrierung.  
  
8.  Sie müssen die GUID für Ihre Hauptregisterkarte der obersten Ebene auch in die Liste der Bezeichner zum Gruppieren von Registerkarten aufnehmen. Führen Sie dazu die Schritte unter **Ändern der Gruppierung von Registerkarten im Dashboard** durch.  
  
## <a name="change-the-grouping-of-tabs-in-the-dashboard"></a>Ändern der Gruppierung von Registerkarten im Dashboard  
 Sie können sicherstellen, dass Ihre Registerkarten gruppiert und in der Liste der integrierten Microsoft-Registerkarten enthalten sind, indem Sie der Registrierung die Bezeichner hinzufügen.  
  
#### <a name="to-change-the-grouping-of-tabs"></a>So ändern Sie die Gruppierung von Registerkarten  
  
1.  Wenn "Regedit" nicht geöffnet ist, klicken Sie auf **Start**, geben Sie **regedit** ein, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, **SOFTWARE**, dann **Microsoft** und schließlich **Windows Server**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **OEM**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
4.  Geben Sie **DashboardAddIns** als Schlüsselname ein, und drücken Sie dann die **EINGABETASTE**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **DashboardAddIns**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
6.  Geben Sie den GUID-Bezeichner für die Registerkarte als Zeichenfolge ein. Ein Wert ist nicht erforderlich.  
  
7.  Wiederholen Sie die Schritte 5 und 6 für alle Registerkarten und Unterregisterkarten.  
  
8.  Speichern Sie die Änderungen an der Registrierung.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)