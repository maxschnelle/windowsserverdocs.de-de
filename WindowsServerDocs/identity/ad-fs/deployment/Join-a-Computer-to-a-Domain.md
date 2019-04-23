---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: Hinzufügen eines Computers zu einer Domäne
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 811f5296143637974cf82e59d57665f8a96f1c8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884111"
---
# <a name="join-a-computer-to-a-domain"></a>Hinzufügen eines Computers zu einer Domäne

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Für Active Directory-Verbunddienste \(AD FS\) funktioniert, jeden Computer, der während ein Verbundservers zu einer Domäne verknüpft werden muss. Verbundserverproxys können mit einer Domäne verknüpft werden, aber dies ist nicht erforderlich.  
  
Sie müssen keinen Webserver mit einer Domäne zu verknüpfen, wenn der Webserver Ansprüche hostet\-nur Anwendungen zu unterstützen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-join-a-computer-to-a-domain"></a>Zum Hinzufügen eines Computers zu einer Domäne  
  
1.  Auf der **starten** geben **Systemsteuerung**, und drücken Sie dann die EINGABETASTE.  
  
2.  Navigieren Sie zu **System und Sicherheit**, und klicken Sie dann auf **System**.  
  
3.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**auf **Einstellungen ändern**.  
  
4.  Klicken Sie auf der Registerkarte **Computername** auf **Ändern**.  
  
5.  Klicken Sie unter **Mitglied**, klicken Sie auf **Domäne**, geben Sie den Namen der Domäne, die Sie möchten diese Computer verknüpfen, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **OK**, und starten Sie dann den Computer erneut.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Das Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Das Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

