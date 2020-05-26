---
title: Ksetup Delta Host-Karte
description: Referenz Thema für den Ksetup-Befehl "chosttorealmmap", mit dem eine SPN-Zuordnung (Service Principal Name, Dienst Prinzipal Name) zwischen dem angegebenen Host und dem Bereich entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17fc30e76247c570c653d5ec38501a2199435c7f
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817860"
---
# <a name="ksetup-delhosttorealmmap"></a>Ksetup Delta Host-Karte

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Befehl "addhosttorealmmap"](ksetup-addhosttorealmmap.md)
