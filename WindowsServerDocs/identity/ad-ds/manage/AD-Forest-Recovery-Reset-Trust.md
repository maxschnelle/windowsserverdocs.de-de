---
title: 'AD-Gesamtstruktur-Wiederherstellung: einen vollständigen Server sichern'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 455c930a90cd443cf1fe62f436abca88384f79c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865561"
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>Zurücksetzen eines Kennworts vertrauen auf einer Seite der Vertrauensstellung  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Wenn die Wiederherstellung der Gesamtstruktur zu einer sicherheitsverletzung bezieht, verwenden Sie das folgende Verfahren, um eine Vertrauensstellung zur kennwortzurücksetzung auf einer Seite der Vertrauensstellung. Dies schließt die implizite Vertrauensstellungen zwischen untergeordneten und übergeordneten Domänen als auch explizite Vertrauensstellungen zwischen dieser Domäne (der vertrauenden Domäne) und einer anderen Domäne (der vertrauenswürdigen Domäne). 
  
 Zurücksetzen des Kennworts für die nur die vertrauende domänenseite der Vertrauensstellung, auch bekannt als die eingehende Vertrauensstellung (die Seite, in denen diese Domäne angehört). Verwenden Sie dann das gleiche Kennwort auf der vertrauenswürdigen Domäne-Seite der Vertrauensstellung, auch bekannt als die ausgehende Vertrauensstellung an. Zurücksetzen des Kennworts für die ausgehende Vertrauensstellung an, bei der Wiederherstellung des ersten Domänencontrollers in jedem der anderen Domänen (vertrauenswürdigen). 
  
 Das Zurücksetzen des Kennworts für die Vertrauensstellung stellt sicher, dass der Domänencontroller nicht mit potenziell schlechten DCs außerhalb seiner Domäne repliziert wird. Wenn Sie beim Wiederherstellen des ersten Domänencontrollers in jeder Domäne dasselbe Vertrauensstellungskennwort festlegen, stellen Sie sicher, dass dieser Domänencontroller mit jedem der wiederhergestellten Domänencontroller repliziert werden. Nachfolgende DCs in der Domäne, die wiederhergestellt werden, durch die Installation von AD DS werden diese neuen Kennwörter automatisch während des Installationsvorgangs repliziert. 
  
## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>Um eine Vertrauensstellung zur kennwortzurücksetzung auf einer Seite der Vertrauensstellung  
  
1. Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   ```  
   netdom experthelp trust  
   ```  
  
2. Verwenden Sie die Syntax, dass dieser Befehl bietet für mit dem NetDom-Tool zum Zurücksetzen des Kennworts für die Vertrauensstellung.
   Angenommen, es gibt zwei Domänen in der Gesamtstruktur – über- und untergeordneten – und Sie diesen Befehl auf dem wiederhergestellten DC in der übergeordneten Domäne ausgeführt werden, verwenden Sie die folgende Befehlssyntax:  

   ```  
   netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   Wenn Sie diesen Befehl in der untergeordneten Domäne ausführen, verwenden Sie die folgende Befehlssyntax:  

   ```  
   netdom trust child domain name /domain:parent domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   > [!NOTE]
   > **PasswordT** muss der gleiche Wert auf beiden Seiten der Vertrauensstellung. Führen Sie diesen Befehl nur einmal (im Gegensatz zu den **Netdom Resetpwd** Befehl) da es das Kennwort automatisch zweimal zurückgesetzt. 
  
## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
