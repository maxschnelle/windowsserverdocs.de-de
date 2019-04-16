---
title: Konfigurieren eines vorhandenen Dateiservers als Inhaltsserver
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: bdac7d2a-25b4-4f61-bed1-b290700c18f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: da4c38b6209dc10704aee8c79344ee2da98da272
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-an-existing-file-server-as-a-content-server"></a>Konfigurieren eines vorhandenen Dateiservers als Inhaltsserver

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Verwenden Sie dieses Verfahren zum Installieren der **BranchCache für Netzwerkdateien** Rollendienst der Dateidienste-Serverrolle auf einem Computer unter Windows Server 2016.  
  
> [!IMPORTANT]  
> Wenn die Serverrolle Dateidienste noch nicht installiert ist, führen Sie dieses Verfahren nicht. Wechseln Sie stattdessen [Installieren eines neuen Dateiservers als Inhaltsserver](../../branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md).  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, führen Sie Windows PowerShell als Administrator, geben Sie die folgenden Befehle an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> Geben Sie den folgenden Befehl zum Installieren des Rollendiensts "Datendeduplizierung", und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-the-branchcache-for-network-files-role-service"></a>So installieren Sie den Rollendienst BranchCache für Netzwerkdateien  
  
1.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  In **Installationstyp auswählen**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  In **Zielserver auswählen**, stellen Sie sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
4.  In **Serverrollen auswählen**im **Rollen**, beachten Sie, dass die **Datei-und Speicherdienste** Rolle bereits installiert. Klicken Sie auf den Pfeil links neben den Rollennamen an, um die Auswahl der Rollendienste zu erweitern, und klicken Sie dann auf den Pfeil neben **Datei- und iSCSI-Dienste**.  
  
5.  Wählen Sie das Kontrollkästchen für **BranchCache für Netzwerkdateien**.  
  
    > [!TIP]  
    > Wenn Sie nicht bereits geschehen, wird empfohlen, dass Sie auch das Kontrollkästchen für auswählen **Datendeduplizierung**.  
  
    Klicken Sie auf **Weiter**.  
  
6.  In **Features auswählen**, klicken Sie auf **Weiter**.  
  
7.  In **Installationsauswahl bestätigen**, überprüfen Sie Ihre Auswahl, und klicken Sie dann auf **installieren**. Die **Installationsstatus** Bereich wird während der Installation angezeigt. Wenn die Installation abgeschlossen ist, klicken Sie auf **schließen**.  
  


