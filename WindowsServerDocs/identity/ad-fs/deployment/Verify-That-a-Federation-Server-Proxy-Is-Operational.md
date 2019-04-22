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
ms.openlocfilehash: 4900d8621b94a514a07bba55b2f7f3df5dd36353
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814621"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>Überprüfen der Betriebsbereitschaft eines Verbundserverproxys

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
[Prüfliste: Das Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

