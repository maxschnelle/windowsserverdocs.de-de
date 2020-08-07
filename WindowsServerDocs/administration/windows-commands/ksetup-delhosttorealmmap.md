---
title: ksetup delhosttorealmmap
description: Referenz Artikel für den Befehl "Ksetup Delta Host Map", der eine Dienst Prinzipal Namen-Zuordnung (Service Principal Name, SPN) zwischen dem angegebenen Host und dem Bereich entfernt.
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 953a8d33a65bb9c5aafd4d549f762772bc059ba4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888000"
---
# <a name="ksetup-delhosttorealmmap"></a>ksetup delhosttorealmmap

Entfernt die Zuordnung eines Dienst Prinzipal namens (SPN) zwischen dem angegebenen Host und dem Bereich. Dieser Befehl entfernt auch die Zuordnung zwischen einem Host und dem Bereich (oder mehreren Hosts zum Bereich).

Die Zuordnung wird in der Registrierung unter gespeichert `HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm` . Nachdem Sie diesen Befehl ausgeführt haben, sollten Sie sicherstellen, dass die Zuordnung in der Registrierung angezeigt wird.

## <a name="syntax"></a>Syntax

```
ksetup /delhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<hostname>` | Gibt den voll qualifizierten Domänen Namen des Computers an. |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Konfiguration des Bereichs "Configuration Manager" zu ändern und die Zuordnung des Host Computers IPops897 in den Bereich zu löschen:

```
ksetup /delhosttorealmmap IPops897 CONTOSO
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Befehl "addhosttorealmmap"](ksetup-addhosttorealmmap.md)
