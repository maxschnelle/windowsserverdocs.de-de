---
title: 'AD-Gesamtstruktur Wiederherstellung: Zurücksetzen eines Vertrauens Kennworts'
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.openlocfilehash: d3a0c694e2108ca623f1ba224d2a265314d7800e
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941480"
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>Zurücksetzen eines Vertrauensstellungs Kennworts auf einer Seite der Vertrauensstellung

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Wenn die Wiederherstellung der Gesamtstruktur mit einer Sicherheitsverletzung verbunden ist, verwenden Sie das folgende Verfahren, um ein Vertrauensstellungs Kennwort auf einer Seite der Vertrauensstellung zurückzusetzen. Dies schließt implizite Vertrauens Stellungen zwischen untergeordneten und übergeordneten Domänen sowie explizite Vertrauens Stellungen zwischen dieser Domäne (der vertrauenden Domäne) und einer anderen Domäne (der vertrauenswürdigen Domäne) ein.

 Setzen Sie das Kennwort nur auf der vertrauenden Domänen Seite der Vertrauensstellung zurück, auch bekannt als eingehende Vertrauensstellung (die Seite, zu der diese Domäne gehört). Verwenden Sie dann das gleiche Kennwort auf der vertrauenswürdigen Domänen Seite der Vertrauensstellung, auch bekannt als ausgehende Vertrauensstellung. Setzen Sie das Kennwort der ausgehenden Vertrauensstellung zurück, wenn Sie den ersten Domänen Controller in den anderen (vertrauenswürdigen) Domänen wiederherstellen.

 Durch das Zurücksetzen des Vertrauensstellungs Kennworts wird sichergestellt, dass der Domänen Controller nicht mit potenziell ungültigen DCS außerhalb der Domäne Durch Festlegen desselben Vertrauens Kennworts beim Wiederherstellen des ersten Domänen Controllers in den einzelnen Domänen müssen Sie sicherstellen, dass dieser Domänen Controller mit jedem der wiederhergestellten DCS repliziert wird. Nachfolgende DCS in der Domäne, die durch die Installation von AD DS wieder hergestellt werden, werden diese neuen Kenn Wörter während des Installationsvorgangs automatisch replizieren.

## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>So setzen Sie ein Vertrauensstellungs Kennwort auf einer Seite der Vertrauensstellung zurück

1. Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   ```
   netdom experthelp trust
   ```

2. Verwenden Sie die Syntax, die dieser Befehl bereitstellt, um das Vertrauensstellungs Kennwort mit dem Netdom-Tool zurückzusetzen.
   Wenn z. b. zwei Domänen in der Gesamtstruktur – übergeordnet und untergeordnet – vorhanden sind und Sie diesen Befehl auf dem wiederhergestellten Domänen Controller in der übergeordneten Domäne ausführen, verwenden Sie die folgende Befehlssyntax:

   ```
   netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*
   ```

   Wenn Sie diesen Befehl in der untergeordneten Domäne ausführen, verwenden Sie die folgende Befehlssyntax:

   ```
   netdom trust child domain name /domain:parent domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*
   ```

   > [!NOTE]
   > **Passwordt** muss auf beiden Seiten der Vertrauensstellung denselben Wert aufweisen. Führen Sie diesen Befehl nur einmal aus (im Gegensatz zum Befehl **netdom resetpwd** ), da das Kennwort automatisch zweimal zurückgesetzt wird.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
