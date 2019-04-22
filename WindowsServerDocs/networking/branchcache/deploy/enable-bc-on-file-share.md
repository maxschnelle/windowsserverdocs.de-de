---
title: Aktivieren von BranchCache auf einer Dateifreigabe (optional)
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
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
ms.openlocfilehash: 36d8379378529a94874c82e0aa90a6440f0281b2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822231"
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>Aktivieren von BranchCache auf einer Dateifreigabe (optional)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, zum Aktivieren von BranchCache auf einer Dateifreigabe.  
  
> [!IMPORTANT]  
> Sie müssen sich nicht um dieses Verfahren auszuführen, wenn Sie die hashveröffentlichungseinstellung, mit dem Wert konfigurieren **hashveröffentlichung für alle freigegebenen Ordner zulassen**.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>Zum Aktivieren von BranchCache auf einer Dateifreigabe  
  
1.  Öffnen Sie Windows PowerShell, geben Sie **mmc**ein, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  In **hinzufügen oder Entfernen von-Snap-ins**im **Verfügbare Snap-Ins**, doppelklicken Sie auf **gemeinsam genutzten Ordnern**. Der freigegebene Ordner-Assistent wird geöffnet, mit dem lokalen Computer-Objekt, das ausgewählt. Konfigurieren Sie die Ansicht, die Sie bevorzugen, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Doppelklicken Sie auf **gemeinsam genutzten Ordnern (lokal)**, und klicken Sie dann auf **Freigaben**.  
  
5.  Klicken Sie im Detailbereich mit der rechten Maustaste in einer Freigabe, und klicken Sie dann auf **Eigenschaften**. Der Freigabe **Eigenschaften** Dialogfeld wird geöffnet.  
  
6.  In der **Eigenschaften** Dialogfeld auf die **allgemeine** auf **Offlineeinstellungen**. Die **Offlineeinstellungen** Dialogfeld wird geöffnet.  
  
7.  Sicherstellen, dass **nur die Dateien und Programme, die Benutzer angeben, offline verfügbar** ausgewählt ist, und klicken Sie dann auf **BranchCache aktivieren**.  
  
8.  Klicken Sie zweimal auf **OK** .  
  

