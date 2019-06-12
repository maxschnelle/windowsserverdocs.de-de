---
title: ksetup:mapuser
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5bc68fe9e8f4cbb9869cb74e4eb20a3400eb56ad
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437963"
---
# <a name="ksetupmapuser"></a>ksetup:mapuser



Ordnet den Namen einer Kerberos-Prinzipal mit einem Konto an. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /mapuser <Principal> <Account>
```

### <a name="parameters"></a>Parameter

|  Parameter   |                                                   Beschreibung                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| \<Principal> |              Die vollqualifizierten Domänennamen der Prinzipal; z. B. mike@corp.CONTOSO.COM.              |
|  \<Konto >  | Oder die Sicherheitsgruppe Namen einer Gruppe, der auf diesem Computer, z. B. Gäste, Domänen-Benutzer oder Administrator vorhanden ist. |

## <a name="remarks"></a>Hinweise

Ein Konto kann z. B. Domänen-Gäste speziell identifiziert werden. Oder Sie können das Platzhalterzeichen (*) alle Konten enthalten.

Wenn ein Kontoname weggelassen wird, wird die Zuordnung für den angegebenen Prinzipal gelöscht.

Der Computer wird nur die Prinzipale des angegebenen Bereichs authentifiziert, wenn sie gültige Kerberos-Tickets stellen.

Verwendung **Ksetup** ohne Parameter oder Argumente finden Sie unter dem aktuellen zugeordnet, Einstellungen und den Standardbereich.

Wenn Änderungen an den externen Schlüsselverteilungscenter (KDC) und der Bereich-Konfiguration vorgenommen werden, muss ein Neustart des Computers ein, in denen die Einstellung geändert wurde.

## <a name="BKMK_Examples"></a>Beispiele für

Ordnen Sie Mike Danseglios-Konto in den Kerberos-Bereich CONTOSO das Gastkonto auf dem Computer, gewähren ihm sämtliche Berechtigungen der ein Mitglied der integrierten Gastkonto ohne zu diesem Computer zu authentifizieren:
```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```
Entfernen Sie die Zuordnung von Mike Danseglios-Konto, um das Gastkonto auf diesem Computer aus, um zu verhindern, dass ihm Authentifizierung dieses Computers mit seinen Anmeldeinformationen von CONTOSO:
```
ksetup /mapuser mike@corp.CONTOSO.COM 
```
Zuordnen von Mike Danseglios-Konto in der CONTOSO-Kerberos-Bereich auf ein beliebiges vorhandenes Konto auf diesem Computer. (wenn nur die Standardbenutzer und Gastkonten auf diesem Computer aktiv sind, werden Danseglioss Berechtigungen, die festgelegt werden):
```
ksetup /mapuser mike@corp.CONTOSO.COM *
```
Ordnen Sie alle Konten in der CONTOSO-Kerberos-Bereich, auf ein beliebiges vorhandenes Konto mit dem gleichen Namen auf diesem Computer:
```
ksetup /mapuser * *
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)