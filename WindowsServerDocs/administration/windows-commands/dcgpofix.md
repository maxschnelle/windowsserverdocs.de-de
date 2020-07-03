---
title: dcgpofix
description: Referenz Artikel zum Dcgpofix-Befehl, mit dem die Standard-Gruppenrichtlinie Objekte (GPOs) für eine Domäne neu erstellt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf9e3c37c054c34d602e472a2c5f83e9a8b284b9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928803"
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

| Parameter | Beschreibung |
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