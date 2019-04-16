---
title: Installieren eines neuen Dateiservers als Inhaltsserver
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 53937cfc139efc6df5facfa872e63609229a548c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-a-new-file-server-as-a-content-server"></a>Installieren eines neuen Dateiservers als Inhaltsserver

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Verwenden Sie dieses Verfahren, um die Serverrolle Dateidienste installieren und die **BranchCache für Netzwerkdateien** auf einem Computer unter Windows Server 2016-Rollendienst.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, führen Sie Windows PowerShell als Administrator, geben Sie die folgenden Befehle an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> `Restart-Computer`  
>   
> Geben Sie den folgenden Befehl zum Installieren des Rollendiensts "Datendeduplizierung", und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>So installieren Sie Dateidienste und der Rollendienst BranchCache für Netzwerk-Dateien  
  
1.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet. In **vor dem Beginn**, klicken Sie auf **Weiter**.  
  
2.  In **Installationstyp auswählen**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  In **Zielserver auswählen**, stellen Sie sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
4.  In **Serverrollen auswählen**im **Rollen**, beachten Sie, dass die **Datei-und Speicherdienste** Rolle bereits installiert. Klicken Sie auf den Pfeil links neben den Rollennamen an, um die Auswahl der Rollendienste zu erweitern, und klicken Sie dann auf den Pfeil neben **Datei- und iSCSI-Dienste**.  
  
5.  Wählen Sie die Kontrollkästchen für **Dateiserver** und **BranchCache für Netzwerkdateien**.  
  
    > [!TIP]  
    > Es wird empfohlen, dass Sie auch das Kontrollkästchen für auswählen **Datendeduplizierung**.
  
    Klicken Sie auf **Weiter**.  
  
6.  In **Features auswählen**, klicken Sie auf **Weiter**.  
  
7.  In **Installationsauswahl bestätigen**, überprüfen Sie Ihre Auswahl, und klicken Sie dann auf **installieren**. Die **Installationsstatus** Bereich wird während der Installation angezeigt. Wenn die Installation abgeschlossen ist, klicken Sie auf **schließen**.
