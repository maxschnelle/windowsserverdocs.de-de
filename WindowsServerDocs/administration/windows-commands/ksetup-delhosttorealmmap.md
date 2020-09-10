---
title: ksetup delhosttorealmmap
description: Referenz Artikel für den Befehl "Ksetup Delta Host Map", der eine Dienst Prinzipal Namen-Zuordnung (Service Principal Name, SPN) zwischen dem angegebenen Host und dem Bereich entfernt.
ms.topic: reference
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 321d468169005d5b183e3b3d4149872a731b8cfa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639698"
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
