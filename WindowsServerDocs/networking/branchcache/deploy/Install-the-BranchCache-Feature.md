---
title: Installieren der BranchCache-Funktion
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a69848536b56521da9b5ef07689aba7f8690e888
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-branchcache-feature"></a>Installieren der BranchCache-Funktion

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Mithilfe dieses Verfahrens können Sie die BranchCache-Funktion installieren und starten Sie den BranchCache-Dienst auf einem Computer unter Windows Server&reg; 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
Bevor Sie dieses Verfahren ausführen, empfiehlt es sich, dass Sie installieren und konfigurieren die BITS-basierte Anwendung oder der Webserver.  
  
> [!NOTE]  
> Zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, führen Sie Windows PowerShell als Administrator, geben Sie die folgenden Befehle an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>Zum Installieren und aktivieren das BranchCache-feature  
  
1.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  In **Installationstyp auswählen**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  In **Zielserver auswählen**, stellen Sie sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
4.  In **Serverrollen auswählen**, klicken Sie auf **Weiter**.  
  
5.  In **Features auswählen**, klicken Sie auf **BranchCache**, und klicken Sie dann auf **Weiter**.  
  
6.  In **Installationsauswahl bestätigen**, klicken Sie auf **installieren**. In **Installationsstatus**, die BranchCache-Feature-Installation wird fortgesetzt. Wenn die Installation abgeschlossen ist, klicken Sie auf **schließen**.  
  
Nachdem Sie die BranchCache-Funktion installieren, der BranchCache-Dienst – auch als bezeichnet die PeerDistSvc - aktiviert ist, und der Starttyp automatisch.  
  


