---
title: 'Ksetup: mapuser'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: daa1b8d2c6d0ce2801191b953a533a63bcd8f4ab
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724616"
---
# <a name="ksetupmapuser"></a>Ksetup: mapuser



Ordnet den Namen eines Kerberos-Prinzipals einem Konto zu.

## <a name="syntax"></a>Syntax

```
ksetup /mapuser <Principal> <Account>
```

#### <a name="parameters"></a>Parameter

|  Parameter   |                                                   BESCHREIBUNG                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| \<Prinzipal> |              Der voll qualifizierte Domänen Name eines beliebigen Prinzipals. Beispiel: mike@corp.CONTOSO.COM.              |
|  \<Konto>  | Alle Konto-oder Sicherheitsgruppen Namen, die auf diesem Computer vorhanden sind, z. b. Gast, Domänen Benutzer oder Administrator. |

## <a name="remarks"></a>Bemerkungen

Ein Konto kann speziell identifiziert werden, z. b. Domänen Gäste. Oder Sie können das Platzhalter Zeichen (*) verwenden, um alle Konten einzubeziehen.

Wenn ein Kontoname weggelassen wird, wird die Zuordnung für den angegebenen Prinzipal gelöscht.

Der Computer authentifiziert nur die Prinzipale des angegebenen Bereichs, wenn Sie gültige Kerberos-Tickets vorweisen.

Verwenden Sie **Ksetup** ohne Parameter oder Argumente, um die aktuellen zugeordneten Einstellungen und den Standardbereich anzuzeigen.

Wenn Änderungen an der externen Schlüsselverteilungscenter (KDC) und der Bereichs Konfiguration vorgenommen werden, ist ein Neustart des Computers erforderlich, auf dem die Einstellung geändert wurde.

## <a name="examples"></a>Beispiele

Ordnen Sie das Konto von Mike Danseglio innerhalb des Kerberos-Bereichs "" mit dem Gast Konto auf diesem Computer zu, und gewähren Sie ihm alle Berechtigungen eines Mitglieds des integrierten Gastkontos, ohne sich bei diesem Computer authentifizieren zu müssen:
```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```
Entfernen Sie die Zuordnung des Mike Danseglio-Kontos zum Gastkonto auf diesem Computer, um zu verhindern, dass er sich bei diesem Computer mit seinen Anmelde Informationen von "Configuration Manager" authentifiziert:
```
ksetup /mapuser mike@corp.CONTOSO.COM 
```
Ordnen Sie das Konto Mike Danseglio innerhalb des Bereichs "sberos" von "" für ein beliebiges vorhandenes Konto auf diesem Computer zu. (wenn nur die Standardbenutzer-und Gastkonten auf diesem Computer aktiv sind, werden die Berechtigungen von Mike auf diese festgelegt):
```
ksetup /mapuser mike@corp.CONTOSO.COM *
```
Ordnen Sie alle Konten innerhalb des Bereichs "" von "" von "" im Bereich "" von "" auf diesem Computer einem vorhandenen Konto mit demselben Namen zu:
```
ksetup /mapuser * *
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)