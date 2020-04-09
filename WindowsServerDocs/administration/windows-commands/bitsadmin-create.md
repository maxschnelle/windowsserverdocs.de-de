---
title: bitsadmin create
description: Windows-Befehls Thema für **bizadmin Create**, mit dem ein Übertragungs Auftrag mit dem angegebenen anzeigen Amen erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a922d9f15aff0a9bd064a7e987920adf3a9107d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850813"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Übertragungs Auftrag mit dem angegebenen anzeigen Amen. Download Aufträge übertragen von Daten von einem Server in eine lokale Datei. Hochladen von Aufträgen übertragen von Daten aus einer lokalen Datei auf einen-Server. Mit Upload-Antwort-Aufträgen werden Daten aus einer lokalen Datei auf einen Server übertragen, und es wird eine Antwortdatei vom Server empfangen.

Verwenden Sie den Schalter [bitadmin Resume](bitsadmin-resume.md) , um den Auftrag in der Übertragungs Warteschlange zu aktivieren.

## <a name="syntax"></a>Syntax

```
bitsadmin /create [type] displayname
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| Typ | -  **/Download** überträgt Daten von einem Server in eine lokale Datei.<p>-  **"/Upload"** überträgt Daten aus einer lokalen Datei auf einen-Server.<p>-  **/Upload-Reply** überträgt Daten aus einer lokalen Datei auf einen Server und empfängt eine Antwortdatei vom Server.<p>Dieser Parameter ist standardmäßig **/Download** , wenn er nicht in der Befehlszeile angegeben wird. Außerdem sind die Typen **"/Upload"**  und **/Upload-Reply** in Bits 1,2 und früher nicht verfügbar. |
| displayname | Der dem neu erstellten Auftrag zugewiesene Anzeige Name. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Erstellt einen Download Auftrag mit dem Namen *mydownloadjob*.

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
