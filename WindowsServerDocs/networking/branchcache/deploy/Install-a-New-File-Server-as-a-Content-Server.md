---
title: Installieren eines neuen Dateiservers als Inhaltsserver
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e3a4dbe5339685b385b0157756379e9e545f1964
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812021"
---
# <a name="install-a-new-file-server-as-a-content-server"></a>Installieren eines neuen Dateiservers als Inhaltsserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, um die Serverrolle "Dateidienste" zu installieren und die **BranchCache für Netzwerkdateien** -Rollendienst auf einem Computer unter Windows Server 2016.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
> [!NOTE]  
> Geben Sie an der Windows PowerShell-Eingabeaufforderung die folgenden Befehle zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, Windows PowerShell als Administrator ausführen, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> `Restart-Computer`  
>   
> Um den Rollendienst für die Datendeduplizierung zu installieren, geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>So installieren Sie die Serverrolle „Dateidienste“ und den Rollendienst „BranchCache für Netzwerkdateien“  
  
1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie unter **Vorbemerkungen** auf **Weiter**.  
  
2.  In **Installationstyp**, sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  In **Zielserver auswählen**, stellen Sie sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
4.  In **Serverrollen auswählen**im **Rollen**, beachten Sie, dass die **und Dateispeicherdiensten** Rolle bereits installiert ist, klicken Sie auf den Pfeil links neben dem Rollennamen, erweitern die Auswahl von Rollendiensten, und klicken Sie dann auf den Pfeil auf der linken Seite des **Datei- und iSCSI-Dienste**.  
  
5.  Wählen Sie die Kontrollkästchen für **Dateiserver** und **BranchCache für Netzwerkdateien**.  
  
    > [!TIP]  
    > Es wird empfohlen, dass Sie auch das Kontrollkästchen für auswählen **Datendeduplizierung**.
  
    Klicken Sie auf **Weiter**.  
  
6.  In **Funktionen auswählen**, klicken Sie auf **Weiter**.  
  
7.  In **Installationsauswahl bestätigen**, überprüfen Sie Ihre Auswahl, und klicken Sie dann auf **installieren**. Die **Installationsstatus** Bereich wird während der Installation angezeigt. Wenn die Installation abgeschlossen ist, klicken Sie auf **schließen**.
