---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: Hinzufügen eines Computers zu einer Domäne
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 9f6d657397cb07d081a229135e3e6c97c7191164
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408349"
---
# <a name="join-a-computer-to-a-domain"></a>Hinzufügen eines Computers zu einer Domäne

Damit Active Directory-Verbunddienste (AD FS) \(AD FS\) funktioniert, muss jeder Computer, der als Verbund Server fungiert, einer Domäne hinzugefügt werden. Verbund Server Proxys können einer Domäne hinzugefügt werden, dies ist jedoch nicht zwingend erforderlich.  
  
Sie müssen einen Webserver nicht zu einer Domäne hinzufügen, wenn der Webserver nur Ansprüche\-fähigen Anwendungen unterstützt.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-join-a-computer-to-a-domain"></a>So fügen Sie einen Computer einer Domäne hinzu  
  
1.  Geben Sie auf der **Start** Seite **Systemsteuerung**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Navigieren Sie zu **System und Sicherheit**, und klicken Sie dann auf **System**.  
  
3.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**auf **Einstellungen ändern**.  
  
4.  Klicken Sie auf der Registerkarte **Computername** auf **Ändern**.  
  
5.  Klicken Sie unter **Mitglied von**auf **Domäne**, geben Sie den Namen der Domäne ein, der dieser Computer beitreten soll, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **OK**, und starten Sie dann den Computer erneut.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

