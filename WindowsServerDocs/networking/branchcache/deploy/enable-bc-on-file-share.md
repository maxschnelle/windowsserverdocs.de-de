---
title: Aktivieren von BranchCache auf einer Dateifreigabe (optional)
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-bc
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d2b98e7ccd3604de60bfabf865404506569f8c82
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319129"
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>Aktivieren von BranchCache auf einer Dateifreigabe (optional)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mit diesem Verfahren können Sie BranchCache auf einer Dateifreigabe aktivieren.  
  
> [!IMPORTANT]  
> Sie müssen dieses Verfahren nicht ausführen, wenn Sie die Hash Veröffentlichungs Einstellung mit dem Wert **Hash Veröffentlichung für alle freigegebenen Ordner zulassen**konfigurieren.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>So aktivieren Sie BranchCache auf einer Dateifreigabe  
  
1.  Öffnen Sie Windows PowerShell, geben Sie die Zeichenfolge **mmc** ein, und drücken Sie die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  Doppelklicken Sie in **Snap-Ins hinzufügen bzw. entfernen**unter **Verfügbare Snap-** ins auf frei **gegebene Ordner**. Der Assistent für freigegebene Ordner wird geöffnet, und das lokale Computer Objekt ist ausgewählt. Konfigurieren Sie die gewünschte Ansicht, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK**.  
  
4.  Doppelklicken **Sie auf frei** **gegebene Ordner (lokal)** , und klicken Sie dann auf Freigaben.  
  
5.  Klicken Sie im Detailfenster mit der rechten Maustaste auf eine Freigabe, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften** der Freigabe wird geöffnet.  
  
6.  Klicken Sie im Dialogfeld **Eigenschaften** auf der Registerkarte **Allgemein** auf **Offline Einstellungen**. Das Dialogfeld **Offline Einstellungen** wird geöffnet.  
  
7.  Stellen Sie sicher, dass **nur die von den Benutzern angegebenen Dateien und Programme offline verfügbar sind** , und klicken Sie dann auf **BranchCache aktivieren**.  
  
8.  Klicken Sie zweimal auf **OK** .  
  

