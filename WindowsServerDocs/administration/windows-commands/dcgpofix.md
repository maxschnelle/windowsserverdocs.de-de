---
title: dcgpofix
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 179d540371870075906bbcbf8ff912e1b883915d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433932"
---
# <a name="dcgpofix"></a>dcgpofix



Die standardmäßige Gruppenrichtlinienobjekte (GPOs) für eine Domäne wird erstellt. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]
```

### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                 Beschreibung                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /ignoreschema  | Die Version des Active Schema Mc ignoriert</br>Wenn Sie diesen Befehl ausführen. Andernfalls funktioniert der Befehl nur auf die gleiche Schemaversion wie die Windows-Version, in der der Befehl ausgeliefert wurde. |
| / target {domain |                                                                                                     DC                                                                                                      |
|       /?        |                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                     |

## <a name="remarks"></a>Hinweise

-   Die **Dcgpofix** Befehl ist verfügbar in Windows Server 2008 R2 und Windows Server 2008, außer auf Server Core-Installationen.
-   Auch wenn die Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC) mit Windows Server 2008 R2 und Windows Server 2008 verteilt wird, müssen Sie die Gruppenrichtlinien-Verwaltungskonsole als Feature über Server-Manager installieren.

## <a name="BKMK_Examples"></a>Beispiele für

Stellen Sie das Gruppenrichtlinienobjekt auf den ursprünglichen Zustand wieder her. Alle Änderungen gehen verloren, die Sie mit diesem Gruppenrichtlinienobjekt vorgenommen haben. Als bewährte Methode sollten Sie die Standarddomänenrichtlinie nur, um die Standardeinstellungen für Kontorichtlinien, Kennwortrichtlinien, Kontosperrungsrichtlinie und Kerberos-Richtlinie verwalten konfigurieren. In diesem Beispiel, die Sie ignorieren der Version des Active Directory-Schema, damit die **Dcgpofix** Befehl gibt keine Beschränkung auf dasselbe Schema wie die Windows-Version, in dem Sie der Befehl ausgeliefert wurde.
```
dcgpofix /ignoreschema /target:Domain
```
Stellen Sie die Standard-Domänencontrollerrichtlinie auf den ursprünglichen Zustand wieder her. Alle Änderungen gehen verloren, die Sie mit diesem Gruppenrichtlinienobjekt vorgenommen haben. Als bewährte Methode sollten Sie konfigurieren die Standarddomänencontroller-Richtlinie-Gruppenrichtlinienobjekt nur zum Festlegen von Benutzerrechten und Überwachungsrichtlinien. In diesem Beispiel, die Sie ignorieren der Version des Active Directory-Schema, damit die **Dcgpofix** Befehl gibt keine Beschränkung auf dasselbe Schema wie die Windows-Version, in dem Sie der Befehl ausgeliefert wurde.
```
dcgpofix /ignoreschema /target:DC
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Gruppenrichtlinien-TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)