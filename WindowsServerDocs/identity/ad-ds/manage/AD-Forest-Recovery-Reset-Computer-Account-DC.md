---
title: 'AD-Gesamtstruktur-Wiederherstellung: Zurücksetzen des Computerkontos auf dem DC'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adds
ms.openlocfilehash: 388b460196888d4ca0cd12218972197afb6d49c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852761"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD-Gesamtstruktur-Wiederherstellung: Zurücksetzen des Computerkontos auf dem DC

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Verwenden Sie das folgende Verfahren, um das Kennwort des Computerkontos des DC zurückzusetzen. 
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>Zurücksetzen des Kennworts für das Computerkonto des Domänencontrollers  

1. Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   ```
   netdom help resetpwd  
   ```
  
2. Verwenden Sie die Syntax, dass dieser Befehl stellt für die Verwendung von des Netdom-Befehlszeilentools, das Kennwort des Computerkontos, z. B. zurückzusetzen:  

   ```
   netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
   ```  
  
    Wo *Domänencontrollername* ist der lokale Domänencontroller, die Sie wiederherstellen. 
  
   > [!NOTE]
   > Sie sollten diesen Befehl zweimal ausführen.
  
## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
