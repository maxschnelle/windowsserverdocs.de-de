---
title: "Wiederherstellung des AD-Gesamtstruktur - Zurücksetzen des Computerkontos auf dem Domänencontroller"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adfs
ms.openlocfilehash: 588510a27f56abb4497b2f80fa0281a858a7e8eb
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>Wiederherstellung des AD-Gesamtstruktur - Zurücksetzen des Computerkontos auf dem Domänencontroller 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Verwenden Sie das folgende Verfahren, um das Kennwort des Computerkontos des Domänencontrollers zurückzusetzen.  
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>Zurücksetzen des Kennworts für das Computerkonto des Domänencontrollers  
  
1.  Geben Sie den folgenden Befehl an einer Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    netdom help resetpwd  
    ```  
  
2.  Verwenden Sie die Syntax, dass dieser Befehl enthält das Netdom-Befehlszeilentool zum Zurücksetzen des Kennworts für den Computer, z.B.:  
  
    ```  
    netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
    ```  
  
     Wo *Name des Domänencontrollers* ist der lokale Domänencontroller, die Sie wiederherstellen.  
  
    > [!NOTE]
    >  Sie sollten diesen Befehl zweimal ausführen.  
  
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
