---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: "Hinzufügen eines Computers zu einer Domäne"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 641a1541143206d06973a6a0f11c689390abea21
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="join-a-computer-to-a-domain"></a>Hinzufügen eines Computers zu einer Domäne

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Für Active Directory Federation Services \(AD FS\) funktioniert muss jeder Computer, der als Verbundserver Funktionen zu einer Domäne angehören. Verbundserverproxys können in einer Domäne hinzugefügt werden, aber dies ist nicht erforderlich.  
  
Sie müssen keinen Webserver zu einer Domäne beitreten, wenn es sich bei der Webserver nur Claims\-fähigen Anwendungen gehostet wird.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-join-a-computer-to-a-domain"></a>Zum Hinzufügen eines Computers zu einer Domäne  
  
1.  Auf der **starten** geben**Systemsteuerung**, und drücken Sie dann die EINGABETASTE.  
  
2.  Navigieren Sie zu **System und Sicherheit**, und klicken Sie dann auf **System**.  
  
3.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**, klicken Sie auf **Einstellungsänderungen**.  
  
4.  Auf der **Computername** auf **ändern**.  
  
5.  Klicken Sie unter **Mitglied**, klicken Sie auf **Domäne**, geben Sie den Namen der Domäne, die diesem Computer beitreten soll, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **OK**, und klicken Sie dann den Computer neu starten.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

