---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: "Überprüfen Sie, ob a Federation Serverproxy betriebsbereit ist"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4900d8621b94a514a07bba55b2f7f3df5dd36353
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>Überprüfen Sie, ob a Federation Serverproxy betriebsbereit ist

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Das folgende Verfahren können überprüfen, ob der Verbundserverproxy mit dem Verbunddienst in Active Directory Federation Services \(AD FS\) kommunizieren kann. Sie dieses Verfahren ausführen, nach dem Ausführen der **AD FS-Konfigurationsassistenten für den Verbundserverproxy** so konfigurieren Sie die Computer in der Verbundserverproxy-Rolle ausführen. Weitere Informationen zum Ausführen dieses Assistenten finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).  
  
> [!IMPORTANT]  
> Das Ergebnis dieses Tests besteht im erfolgreichen Generieren eines bestimmten Ereignisses in der Ereignisanzeige auf dem Verbundserverproxy-Computer.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>Um sicherzustellen, dass ein Verbundserverproxys betriebsbereit ist  
  
1.  Melden Sie sich bei des Verbundserverproxys als Administrator an.  
  
2.  Auf der **starten** geben**Ereignisanzeige**, und drücken Sie dann die EINGABETASTE.  
  
3.  Klicken Sie im Detailbereich doppelten Mausklick **Anwendungs- und Dienstprotokolle**, doppelten Mausklick **Ereignisse für AD FS**, und klicken Sie dann auf **Admin**.  
  
4.  In der **Ereignis-ID** Spalte, suchen Sie nach der Ereignis-ID 198.  
  
    Wenn der Verbundserverproxy richtig konfiguriert ist, sehen Sie ein neues Ereignis im Anwendungsprotokoll der Ereignisanzeige mit der Ereignis-ID 198. Dieses Ereignis wird überprüft, ob der Verbundserverproxy-Dienst erfolgreich gestartet wurde und nun online ist.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

