---
title: bitsadmin create
description: Referenz Artikel für den Befehl bizadmin Create, mit dem ein Übertragungs Auftrag mit dem angegebenen anzeigen Amen erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3e0f8fb7d8396a238cabcbeb375f61cbe526c3f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928344"
---
# <a name="bitsadmin-create"></a>bitsadmin create

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Übertragungs Auftrag mit dem angegebenen anzeigen Amen.

> [!NOTE]
> Die **/Upload**   Parametertypen "/Upload" und **/Upload-Reply** werden von Bits 1,2 und früher nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /create [type] displayname
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ------- | -------- |
| type | Es gibt drei Arten von Aufträgen:<ul><li>**Downloaden.** Überträgt Daten von einem Server in eine lokale Datei.</li><li>**Uploads.** Überträgt Daten aus einer lokalen Datei auf einen-Server.</li><li>**/Upload-Reply.** Überträgt Daten aus einer lokalen Datei auf einen Server und empfängt eine Antwortdatei vom Server.</li></ul>Dieser Parameter ist standardmäßig **/Download** , wenn er nicht angegeben ist. |
| displayname | Der dem neu erstellten Auftrag zugewiesene Anzeige Name. |

## <a name="examples"></a>Beispiele

So erstellen Sie einen Download Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Resume"](bitsadmin-resume.md)

- [Bider admin-Befehl](bitsadmin.md)
