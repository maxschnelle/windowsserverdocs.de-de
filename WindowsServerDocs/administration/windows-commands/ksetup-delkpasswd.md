---
title: 'Ksetup: Delta Pass WD'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2de1546b112041f7035a711852140e9bb34babe3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724650"
---
# <a name="ksetupdelkpasswd"></a>Ksetup: Delta Pass WD

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

entfernt einen Kerberos-Kenn Wort Server (kpasswd) für einen Bereich.
## <a name="syntax"></a>Syntax
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
#### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                   BESCHREIBUNG                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. Bereich angezeigt, wenn **Ksetup** ausgeführt wird.                                |
| <KpasswdName> | Der KDC-Name, der als Kerberos-Kenn Wort Server verwendet werden soll, wird als voll qualifizierter Domänen Name ohne Beachtung der Groß-/Kleinschreibung angegeben, z. b. mitkdc.contoso.com Wenn der KDC-Name weggelassen wird, kann DNS verwendet werden, um nach KDCs zu suchen. |

## <a name="remarks"></a>Bemerkungen
Führen Sie den Befehl **Ksetup** aus, um den KDC-Namen zu überprüfen. Wenn **kpasswd =** nicht in der Ausgabe angezeigt wird, wurde die Zuordnung nicht konfiguriert. Wenn festgelegt, werden mehrere Zuordnungen aufgelistet.
## <a name="examples"></a>Beispiele
Überprüfen Sie den Bereich Corp. CONTOSO.com verwendet den nicht-Windows-KDC-Server mitkdc.contoso.com als Kenn Wort Server:
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
Um zu überprüfen, ob der Befehl wie beabsichtigt funktioniert, führen Sie **Ksetup** auf dem Windows-Computer aus, um den Bereich Corp. CONTOSO.com ist keinem Kerberos-Kenn Wort Server (KDC-Name) zugeordnet.
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [ksetup](ksetup.md)
-   [Ksetup: Delta Pass WD](ksetup-delkpasswd.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
