---
title: dcgpofix
description: Referenz Artikel zum Dcgpofix-Befehl, mit dem die Standard-Gruppenrichtlinie Objekte (GPOs) für eine Domäne neu erstellt werden.
ms.topic: reference
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3ee90daa4e0bc6100c28f06c892694e015976f8a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628942"
---
# <a name="dcgpofix"></a>dcgpofix

Erstellt die Standard-Gruppenrichtlinie Objekte (GPOs) für eine Domäne neu. Um zum Gruppenrichtlinien-Verwaltungskonsole (GPMC) zu gelangen, müssen Sie Gruppenrichtlinie Management als Feature über Server-Manager installieren.

>[!IMPORTANT]
> Als bewährte Vorgehensweise sollten Sie das Gruppenrichtlinien Objekt Standard Domänen Richtlinie nur so konfigurieren, dass die Standardeinstellungen für **Konto Richtlinien** , Kenn Wort Richtlinie, Konto Sperr Richtlinie und Kerberos-Richtlinie verwaltet werden. Außerdem sollten Sie das Gruppenrichtlinien Objekt Standard Domänen Controller-Richtlinie nur so konfigurieren, dass Benutzerrechte und Überwachungs Richtlinien festgelegt werden.

## <a name="syntax"></a>Syntax

```
dcgpofix [/ignoreschema] [/target: {domain | dc | both}] [/?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /ignoreschema | Ignoriert die Version des Active Directory Schemas, wenn Sie diesen Befehl ausführen. Andernfalls funktioniert der Befehl nur für dieselbe Schema Version wie die Windows-Version, in der der Befehl ausgeliefert wurde. |
| `/target {domain | dc | both` | Gibt an, ob die Standard Domänen Richtlinie, die Standard Domänen Controller-Richtlinie oder beide Richtlinien Typen als Ziel festgelegt werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Standardeinstellungen für **Konto Richtlinien** , die Kenn Wort Richtlinie, die Konto Sperr Richtlinie und die Kerberos-Richtlinie zu verwalten, während die Active Directory Schema Version ignoriert wird:

```
dcgpofix /ignoreschema /target:domain
```

Geben Sie Folgendes ein, um das Gruppenrichtlinien Objekt Standard Domänen Controller nur zum Festlegen von Benutzerrechten und Überwachungs Richtlinien zu konfigurieren, während die Active Directory Schema Version ignoriert wird:

```
dcgpofix /ignoreschema /target:dc
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)