---
title: 'AD-Gesamtstruktur Wiederherstellung: Zurücksetzen des Computer Kontos auf dem Domänen Controller'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adds
ms.openlocfilehash: 320d02f789b8dda771b648b0aa9a58f545f3358b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368868"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD-Gesamtstruktur Wiederherstellung: Zurücksetzen des Computer Kontos auf dem Domänen Controller

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Gehen Sie folgendermaßen vor, um das Computer Konto Kennwort des DC zurückzusetzen. 
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>So setzen Sie das Computer Konto Kennwort des Domänen Controllers zurück  

1. Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   ```
   netdom help resetpwd  
   ```
  
2. Verwenden Sie die Syntax, die dieser Befehl für die Verwendung des Netdom-Befehlszeilen Tools bereitstellt, um das Computer Konto Kennwort zurückzusetzen, z. b.:  

   ```
   netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
   ```  
  
    Dabei ist der *Domänen Controller Name der lokale Domänen Controller* , den Sie wiederherstellen. 
  
   > [!NOTE]
   > Sie sollten diesen Befehl zweimal ausführen.
  
## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
