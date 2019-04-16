---
title: "Wiederherstellung des AD-Gesamtstruktur - einen vollständigen Server sichern"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adfs
ms.openlocfilehash: 51b53e7348ae00ed2fc63711b9c3297279ebe033
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>Zurücksetzen des Kennworts Vertrauensstellung auf einer Seite der Vertrauensstellung  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Wenn die Wiederherstellung der Gesamtstruktur mit einer sicherheitsverletzung verknüpft ist, gehen Sie zum Zurücksetzen des Kennworts auf einer Seite der Vertrauensstellung vertrauen. Dazu zählen auch implizite Vertrauensstellungen zwischen untergeordneten und übergeordneten Domänen als auch explizite Vertrauensstellungen zwischen dieser Domäne (die vertrauende Domäne) und einer anderen Domäne (der vertrauenswürdigen Domäne).  
  
 Zurücksetzen des Kennworts auf nur die vertrauende Domäne Seite der Vertrauensstellung, auch bekannt als eingehende Vertrauensstellung (die Seite, in denen diese Domäne gehört). Verwenden Sie dann das gleiche Kennwort in der vertrauenswürdigen Domäne Seite der Vertrauensstellung, auch bekannt als die ausgehende Vertrauensstellung. Beim Wiederherstellen des ersten Domänencontrollers in jeder anderen Domäne (vertrauenswürdig), wird das Kennwort für die ausgehende Vertrauensstellung zurückgesetzt.  
  
 Beim Zurücksetzen des Kennworts Vertrauensstellung wird sichergestellt, dass der Domänencontroller nicht mit potenziell fehlerhaften Domänencontroller außerhalb der Domäne repliziert. Durch Festlegen der beim Wiederherstellen des ersten Domänencontrollers in jeder Domäne dasselbe Vertrauensstellungskennwort, stellen Sie sicher, dass dieser Domänencontroller mit den wiederhergestellten Domänencontroller repliziert. Domänencontroller in der Domäne, die wiederhergestellt werden, durch die Installation von AD DS repliziert diese neue Kennwörter automatisch während der Installation.  
  
## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>Zurücksetzen des Kennworts Vertrauensstellung auf einer Seite der Vertrauensstellung  
  
1.  Geben Sie den folgenden Befehl an einer Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    netdom experthelp trust  
    ```  
  
2.  Verwenden Sie die Syntax, die mit diesem Befehl zum mit dem NetDom-Tool zum Zurücksetzen des Kennworts Vertrauensstellung bereitstellt.  
  
     Angenommen, es gibt zwei Domänen in der Gesamtstruktur – übergeordneten und untergeordneten – und Sie werden mit diesem Befehl auf dem wiederhergestellten Domänencontroller in der übergeordneten Domäne ausgeführt wird, verwenden Sie die folgende Befehlssyntax:  
  
    ```  
    netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
    ```  
  
     Wenn Sie diesen Befehl in der untergeordneten Domäne ausführen, verwenden Sie die folgende Befehlssyntax:  
  
    ```  
    netdom trust child domain name /domain:parent domain name /resetOneSide /password:password /userO:administrator /passwordO:*  
    ```  
  
    > [!NOTE]
    >  **PasswordT** sollten der gleiche Wert auf beiden Seiten der Vertrauensstellung sein. Führen Sie diesen Befehl nur einmal (im Gegensatz zu den **Netdom Resetpwd** Befehl), da es das Kennwort automatisch zweimal zurückgesetzt.  
  
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
