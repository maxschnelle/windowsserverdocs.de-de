---
title: scwcmd view
description: Referenz Artikel für den Befehl scwcmd view, der eine XML-Datei mithilfe einer angegebenen XSL-Transformation rendert.
ms.topic: reference
ms.assetid: 7995959a-d93e-4865-a6a0-2ab18c2bb47f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e411bf06015684e7dedb94d109f5e4294f46af84
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388930"
---
# <a name="scwcmd-view"></a>scwcmd view

> Gilt für: Windows Server 2012 R2 und Windows Server 2012

Rendert eine XML-Datei mithilfe einer angegebenen XSL-Transformation. Dieser Befehl kann nützlich sein, um SCW (Security Configuration Wizard). XML-Dateien unter Verwendung verschiedener Ansichten anzuzeigen.

## <a name="syntax"></a>Syntax

```
scwcmd view /x:<Xmlfile.xml> [/s:<Xslfile.xsl>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /x`<Xmlfile.xml>` | Gibt die XML-Datei an, die angezeigt werden soll. Dieser Parameter muss angegeben werden. |
| /s`<Xslfile.xsl>` | Gibt die XSL-Transformation an, die als Teil des Renderingprozesses auf die XML-Datei angewendet werden soll. Dieser Parameter ist für SCW. XML-Dateien optional. Wenn der **View** -Befehl verwendet wird, um eine SCW. XML-Datei zu rendieren, wird automatisch versucht, die richtige Standard Transformation für die angegebene XML-Datei zu laden. Wenn eine XSL-Transformation angegeben ist, muss die Transformation unter der Annahme geschrieben werden, dass sich die XML-Datei im gleichen Verzeichnis wie die XSL-Transformation befindet. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="example"></a>Beispiel

Wenn Sie *Policyfile.xml* mithilfe der Transformation *policyview. xsl* anzeigen möchten, geben Sie Folgendes ein:

```
scwcmd view /x:C:\policies\Policyfile.xml /s:C:\viewers\Policyview.xsl
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [scwcmd-Analyse Befehl](scwcmd-analyze.md)

- [scwcmd-Befehl "configure"](scwcmd-configure.md)

- [scwcmd-register Befehl](scwcmd-register.md)

- [scwcmd-rollback-Befehl](scwcmd-rollback.md)

- [Befehl "Scwcmd Transform"](scwcmd-transform.md)