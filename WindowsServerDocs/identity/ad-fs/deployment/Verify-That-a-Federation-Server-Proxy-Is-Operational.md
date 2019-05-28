---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: Überprüfen der Betriebsbereitschaft eines Verbundserverproxys
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 26b0ae4f331607d83c6b94a2655ddc9eded8a356
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191867"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>Überprüfen der Betriebsbereitschaft eines Verbundserverproxys


Sie können das folgende Verfahren stellen Sie sicher, dass der Verbundserverproxy mit dem Verbunddienst in Active Directory-Verbunddienste kommunizieren kann \(AD FS\). Sie führen dieses Verfahren, nach dem Ausführen der **Konfigurations-Assistenten von AD FS Federation Server Proxy** so konfigurieren Sie die Computer in der Verbundserverproxy-Rolle ausgeführt. Weitere Informationen zum Ausführen dieses Assistenten finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).  
  
> [!IMPORTANT]  
> Das Ergebnis dieses Tests besteht im erfolgreichen Generieren eines bestimmten Ereignisses in der Ereignisanzeige auf dem Verbundserverproxy-Computer.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>Um sicherzustellen, dass es sich bei ein Verbundserverproxy funktionsfähig ist.  
  
1.  Melden Sie sich an den Verbundserverproxy als Administrator an.  
  
2.  Auf der **starten** geben**Ereignisanzeige**, und drücken Sie dann die EINGABETASTE.  
  
3.  Doppelklicken Sie im Detailbereich,\-klicken Sie auf **Anwendungs- und Dienstprotokolle**, double\-klicken Sie auf **AD FS-Ereignisse**, und klicken Sie dann auf **Admin**.  
  
4.  Suchen Sie in der Spalte **Ereignis-ID** nach der Ereignis-ID 198.  
  
    Wenn der Verbundserverproxy ordnungsgemäß konfiguriert ist, sehen Sie ein neues Ereignis im Anwendungsprotokoll der Ereignisanzeige mit der Ereignis-ID 198 angezeigt. Dieses Ereignis bestätigt, dass der Verbundserverproxy-Dienst erfolgreich gestartet wurde und nun online ist.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

