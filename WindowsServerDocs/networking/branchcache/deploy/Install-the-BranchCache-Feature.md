---
title: Installieren der BranchCache-Funktion
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5ee438ef57d3355cf19713d8574591aeea6ae06f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406434"
---
# <a name="install-the-branchcache-feature"></a>Installieren der BranchCache-Funktion

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mit diesem Verfahren können Sie die BranchCache-Funktion installieren und den BranchCache-Dienst auf einem Computer unter Windows Server&reg; 2016, Windows Server 2012 R2 oder Windows Server 2012 starten.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
Bevor Sie dieses Verfahren ausführen, empfiehlt es sich, die Bits-basierte Anwendung oder den Webserver zu installieren und zu konfigurieren.  
  
> [!NOTE]  
> Um dieses Verfahren mithilfe von Windows PowerShell auszuführen, führen Sie Windows PowerShell als Administrator aus, geben Sie die folgenden Befehle an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>So installieren Sie die BranchCache-Funktion  
  
1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  Vergewissern Sie sich, dass unter **Installationstyp auswählen**die Option **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **weiter**.  
  
3.  Stellen **Sie in Zielserver auswählen**sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **weiter**.  
  
4.  Klicken Sie in **Serverrollen auswählen**auf **Weiter**.  
  
5.  Klicken Sie unter **Features auswählen**auf **BranchCache**, und klicken Sie dann auf **weiter**.  
  
6.  Klicken Sie unter **Installationsauswahl bestätigen** auf **Installieren**. Bei der Installation wird die Installation der BranchCache-Funktion **fort**gesetzt. Wenn die Installation abgeschlossen ist, klicken Sie auf **Schließen**.  
  
Nachdem Sie das BranchCache-Feature installiert haben, wird der BranchCache-Dienst (auch als PeerDistSvc bezeichnet) aktiviert, und der Starttyp ist automatisch.  
  


