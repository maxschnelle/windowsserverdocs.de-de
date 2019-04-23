---
title: Konfigurieren eines vorhandenen Dateiservers als Inhaltsserver
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: bdac7d2a-25b4-4f61-bed1-b290700c18f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d031e8aa853849c322692552ca9107838cebb5e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866911"
---
# <a name="configure-an-existing-file-server-as-a-content-server"></a>Konfigurieren eines vorhandenen Dateiservers als Inhaltsserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, installieren die **BranchCache für Netzwerkdateien** Rollendienst der Dateidienste-Serverrolle auf einem Computer unter Windows Server 2016.  
  
> [!IMPORTANT]  
> Führen Sie dieses Verfahren nicht weiter aus, wenn die Serverrolle Dateidienste noch nicht installiert wurde. Stattdessen finden Sie unter [Installieren eines neuen Dateiservers als Inhaltsserver](../../branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
> [!NOTE]  
> Geben Sie an der Windows PowerShell-Eingabeaufforderung die folgenden Befehle zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, Windows PowerShell als Administrator ausführen, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> Um den Rollendienst für die Datendeduplizierung zu installieren, geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-the-branchcache-for-network-files-role-service"></a>So installieren Sie den BranchCache für Netzwerkdateien-Rollendienst  
  
1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Des Assistenten zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  In **Installationstyp**, sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  In **Zielserver auswählen**, stellen Sie sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
4.  In **Serverrollen auswählen**im **Rollen**, beachten Sie, dass die **und Dateispeicherdiensten** Rolle bereits installiert ist, klicken Sie auf den Pfeil links neben dem Rollennamen, erweitern die Auswahl von Rollendiensten, und klicken Sie dann auf den Pfeil auf der linken Seite des **Datei- und iSCSI-Dienste**.  
  
5.  Wählen Sie das Kontrollkästchen für **BranchCache für Netzwerkdateien**.  
  
    > [!TIP]  
    > Wenn Sie nicht bereits geschehen, wird empfohlen, dass Sie auch das Kontrollkästchen für auswählen **Datendeduplizierung**.  
  
    Klicken Sie auf **Weiter**.  
  
6.  In **Funktionen auswählen**, klicken Sie auf **Weiter**.  
  
7.  In **Installationsauswahl bestätigen**, überprüfen Sie Ihre Auswahl, und klicken Sie dann auf **installieren**. Die **Installationsstatus** Bereich wird während der Installation angezeigt. Wenn die Installation abgeschlossen ist, klicken Sie auf **schließen**.  
  


