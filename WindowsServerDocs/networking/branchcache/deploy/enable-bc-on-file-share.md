---
title: Aktivieren von BranchCache auf einer Dateifreigabe (Optional)
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-bc
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33ed40ef91d9389bb7940dcf928cba43f0c9dbd2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>Aktivieren von BranchCache auf einer Dateifreigabe (Optional)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie um BranchCache auf einer Dateifreigabe aktivieren.  
  
> [!IMPORTANT]  
> Sie müssen sich nicht um dieses Verfahren auszuführen, wenn Sie die hashveröffentlichungseinstellung, mit dem Wert konfigurieren **hashveröffentlichung für alle freigegebenen Ordner zulassen**.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>So aktivieren Sie BranchCache auf einer Dateifreigabe  
  
1.  Öffnen Sie Windows PowerShell, geben **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  In der MMC auf die **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.  
  
3.  In **hinzufügen oder Entfernen von Snap-Ins**im **Verfügbare Snap-Ins**, doppelklicken Sie auf **freigegebene Ordner**. Der Assistent zum freigegebenen Ordner, die mit dem lokalen Computer-Objekt ausgewählt wird geöffnet. Konfigurieren Sie die Ansicht, in der Sie arbeiten möchten, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Doppelklicken Sie auf **freigegebene Ordner (lokal)**, und klicken Sie dann auf **Freigaben**.  
  
5.  Klicken Sie im Detailbereich mit der rechten Maustaste einer Freigabe, und klicken Sie dann auf **Eigenschaften**. Der Freigabe **Eigenschaften** Dialogfeld wird geöffnet.  
  
6.  In der **Eigenschaften** Dialogfeld auf die **allgemeine** auf **Offline-Einstellungen**. Die **Offline-Einstellungen** Dialogfeld wird geöffnet.  
  
7.  Stellen Sie sicher, dass **nur die Dateien und Programme, die Benutzer angeben, offline verfügbar** ausgewählt ist, und klicken Sie dann auf **BranchCache aktivieren**.  
  
8.  Klicken Sie auf **OK** zweimal.  
  

