---
title: dcgpofix
description: Referenz Thema für Dcgpofix, das die Standard-Gruppenrichtlinie Objekte (GPOs) für eine Domäne neu erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b30190f06e5e38031c8d205d8ccee9c573a8d84
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716786"
---
# <a name="dcgpofix"></a>dcgpofix

Erstellt die Standard-Gruppenrichtlinie Objekte (GPOs) für eine Domäne neu.

## <a name="syntax"></a>Syntax

```
DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]
```

#### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                 BESCHREIBUNG                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /ignoreschema  | Ignoriert die Version der Active Directory® Schema-MC.</br>Wenn Sie diesen Befehl ausführen. Andernfalls funktioniert der Befehl nur für dieselbe Schema Version wie die Windows-Version, in der der Befehl ausgeliefert wurde. |
| /Target {Domäne |                                                                                                     DC                                                                                                      |
|       /?        |                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                     |

## <a name="remarks"></a>Bemerkungen

-   Der **Dcgpofix** -Befehl ist in Windows Server 2008 R2 und Windows Server 2008 mit Ausnahme von Server Core-Installationen verfügbar.
-   Obwohl die Gruppenrichtlinien-Verwaltungskonsole (GPMC) mit Windows Server 2008 R2 und Windows Server 2008 verteilt ist, müssen Sie Gruppenrichtlinie Management als Feature über Server-Manager installieren.

## <a name="examples"></a>Beispiele

Stellen Sie das Gruppenrichtlinien Objekt der Standard Domänen Richtlinie in seinem ursprünglichen Zustand wieder her. Alle Änderungen, die Sie an diesem GPO vorgenommen haben, gehen verloren. Als bewährte Vorgehensweise sollten Sie das Gruppenrichtlinien Objekt Standard Domänen Richtlinie nur so konfigurieren, dass die Standardeinstellungen für Konto Richtlinien, Kenn Wort Richtlinie, Konto Sperr Richtlinie und Kerberos-Richtlinie verwaltet werden. In diesem Beispiel ignorieren Sie die Version des Active Directory Schemas, sodass der **Dcgpofix** -Befehl nicht auf das gleiche Schema wie die Windows-Version beschränkt ist, in der der Befehl ausgeliefert wurde.
```
dcgpofix /ignoreschema /target:Domain
```
Stellen Sie das Gruppenrichtlinien Objekt Standard Domänen Controller in seinem ursprünglichen Zustand wieder her. Alle Änderungen, die Sie an diesem GPO vorgenommen haben, gehen verloren. Als bewährte Vorgehensweise sollten Sie das Gruppenrichtlinien Objekt Standard Domänen Controller nur so konfigurieren, dass Benutzerrechte und Überwachungs Richtlinien festgelegt werden. In diesem Beispiel ignorieren Sie die Version des Active Directory Schemas, sodass der **Dcgpofix** -Befehl nicht auf das gleiche Schema wie die Windows-Version beschränkt ist, in der der Befehl ausgeliefert wurde.
```
dcgpofix /ignoreschema /target:DC
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [TechCenter zu Gruppenrichtlinien](https://go.microsoft.com/fwlink/?LinkID=145531)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)