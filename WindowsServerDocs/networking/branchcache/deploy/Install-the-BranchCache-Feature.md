---
title: Installieren der BranchCache-Funktion
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8b4aecd9e9355a6c2d5ac485ac77c76428fe295f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872191"
---
# <a name="install-the-branchcache-feature"></a>Installieren der BranchCache-Funktion

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, die BranchCache-Funktion installieren und starten Sie den BranchCache-Dienst auf einem Computer unter Windows Server&reg; 2016, Windows Server 2012 R2 und Windows Server 2012.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
Bevor Sie dieses Verfahren durchführen, empfiehlt es sich, dass Sie installieren und der BITS-basierte Anwendung oder eine Web-Server konfigurieren.  
  
> [!NOTE]  
> Geben Sie an der Windows PowerShell-Eingabeaufforderung die folgenden Befehle zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, Windows PowerShell als Administrator ausführen, und drücken Sie dann die EINGABETASTE.  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>So installieren Sie die BranchCache-Funktion  
  
1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Des Assistenten zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  In **Installationstyp**, sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  In **Zielserver auswählen**, stellen Sie sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie in **Serverrollen auswählen**auf **Weiter**.  
  
5.  In **Funktionen auswählen**, klicken Sie auf **BranchCache**, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie unter **Installationsauswahl bestätigen** auf **Installieren**. In **Installationsstatus**, die BranchCache-Feature-Installation fortgesetzt wird. Wenn die Installation abgeschlossen ist, klicken Sie auf **schließen**.  
  
Nachdem Sie das BranchCache-Feature installieren, der BranchCache-Dienst - und die PeerDistSvc – so genannte aktiviert ist, und der Starttyp ist automatisch.  
  


