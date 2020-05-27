---
title: Ksetup mapuser
description: Referenz Thema für den Ksetup mapuser-Befehl, der den Namen eines Kerberos-Prinzipals einem Konto zuordnet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ac2f3e30b3057ceea4376d7ffe8286875d5301d
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817670"
---
# <a name="ksetup-mapuser"></a>Ksetup mapuser

Ordnet den Namen eines Kerberos-Prinzipals einem Konto zu.

## <a name="syntax"></a>Syntax

```
ksetup /mapuser <principal> <account>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<principal>` | Gibt den voll qualifizierten Domänen Namen eines Prinzipal Benutzers an. Beispiel: mike@corp.CONTOSO.COM. Wenn Sie keinen Konto Parameter angeben, wird die Zuordnung für den angegebenen Prinzipal gelöscht. |
| `<account>` | Gibt einen beliebigen Konto-oder Sicherheitsgruppen Namen an, der auf diesem Computer vorhanden ist, z. b. **Gast**, **Domänen Benutzer**oder **Administrator**. Wenn dieser Parameter ausgelassen wird, wird die Zuordnung für den angegebenen Prinzipal gelöscht. |

#### <a name="remarks"></a>Hinweise

- Ein Konto kann speziell identifiziert werden, z. b. **Domänen Gäste**, oder Sie können ein Platzhalter Zeichen (*) verwenden, um alle Konten einzubeziehen.

- Der Computer authentifiziert nur die Prinzipale des angegebenen Bereichs, wenn Sie gültige Kerberos-Tickets vorweisen.

- Wenn Änderungen an der externen Schlüsselverteilungscenter (KDC) und der Bereichs Konfiguration vorgenommen werden, ist ein Neustart des Computers erforderlich, auf dem die Einstellung geändert wurde.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuellen zugeordneten Einstellungen und den Standardbereich anzuzeigen:

```
ksetup
```

Wenn Sie das Konto von Mike Danseglio innerhalb des Kerberos-Bereichs "Configuration Manager" dem Gast Konto auf diesem Computer zuordnen möchten, um ihm alle Berechtigungen eines Mitglieds des integrierten Gastkontos zu erteilen, ohne sich bei diesem Computer authentifizieren zu müssen, geben Sie Folgendes ein:

```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```

Wenn Sie die Zuordnung von Mike Danseglio-Konto zum Gastkonto auf diesem Computer entfernen möchten, um zu verhindern, dass er sich mit seinen Anmelde Informationen von "Configuration Manager" bei diesem Computer authentifiziert, geben Sie Folgendes ein:

```
ksetup /mapuser mike@corp.CONTOSO.COM
```

Geben Sie Folgendes ein, um das Konto von Mike Danseglios im Bereich "sberos" von "" für ein vorhandenes Konto auf diesem Computer zuzuordnen:

```
ksetup /mapuser mike@corp.CONTOSO.COM *
```

> [!NOTE]
> Wenn nur die Standard Benutzer-und Gastkonten auf diesem Computer aktiv sind, werden die Berechtigungen von Mike auf diese festgelegt.

Geben Sie Folgendes ein, um alle Konten innerhalb des Bereichs "" von "" in "" von "" im Bereich "" von "" im Bereich "" von ""

```
ksetup /mapuser * *
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)
