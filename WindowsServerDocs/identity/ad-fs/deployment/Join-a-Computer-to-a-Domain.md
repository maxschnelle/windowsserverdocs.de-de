---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: Hinzufügen eines Computers zu einer Domäne
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 174f585f3e156fc8e068b9300fc90a20a67869cf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855353"
---
# <a name="join-a-computer-to-a-domain"></a>Hinzufügen eines Computers zu einer Domäne

Damit Active Directory-Verbunddienste (AD FS) \(AD FS\) funktioniert, muss jeder Computer, der als Verbund Server fungiert, einer Domäne hinzugefügt werden. Verbund Server Proxys können einer Domäne hinzugefügt werden, dies ist jedoch nicht zwingend erforderlich.  
  
Sie müssen einen Webserver nicht zu einer Domäne hinzufügen, wenn der Webserver nur Ansprüche\-fähigen Anwendungen unterstützt.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-join-a-computer-to-a-domain"></a>So fügen Sie einen Computer einer Domäne hinzu  
  
1.  Geben Sie auf der **Start** Seite **Systemsteuerung**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Navigieren Sie zu **System und Sicherheit**, und klicken Sie dann auf **System**.  
  
3.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** auf **Einstellungen ändern**.  
  
4.  Klicken Sie auf der Registerkarte **Computername** auf **Ändern**.  
  
5.  Klicken Sie unter **Mitglied von**auf **Domäne**, geben Sie den Namen der Domäne ein, der dieser Computer beitreten soll, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **OK**, und starten Sie dann den Computer erneut.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

