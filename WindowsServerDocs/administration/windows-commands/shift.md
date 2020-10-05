---
title: Schiebeoperatoren
description: Referenz Artikel für den Shift-Befehl, der die Position von Batch-Parametern in einer Batchdatei ändert.
ms.topic: reference
ms.assetid: b56574e8-570a-4cc9-bbac-1b94fbf6a47a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4553826aa7c3def335ae1d9ec9594ee9d878fc63
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718337"
---
# <a name="shift"></a>Schiebeoperatoren

Ändert die Position von Batch Parametern in einer Batchdatei.

## <a name="syntax"></a>Syntax

```
shift [/n <N>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /n `<N>` | Gibt an, dass die Verschiebung beim *n*-ten Argument gestartet werden soll, wobei *N* ein beliebiger Wert zwischen *0* und *8*ist. Erfordert Befehls Erweiterungen, die standardmäßig aktiviert sind. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen

- Der **Shift** -Befehl ändert die Werte der Batch Parameter **%0** bis **%9** durch Kopieren jedes Parameters in den vorherigen – der Wert von **%1** wird in **%0**kopiert, der Wert von **%2** wird in **%1**kopiert usw. Dies ist hilfreich beim Schreiben einer Batchdatei, die denselben Vorgang für eine beliebige Anzahl von Parametern ausführt.

- Wenn Befehls Erweiterungen aktiviert sind, unterstützt der Befehl **Shift** die Befehlszeilenoption **/n** . Die **/n** -Option gibt an, dass die Verschiebung beim n-ten Argument gestartet werden soll, wobei **n** ein beliebiger Wert zwischen 0 und 8 ist. Beispielsweise würde **Shift/2** " **%3** " in **"%2**", " **%4** " in " **%3**" usw. verschieben und " **%0** " und " **%1** " nicht beeinträchtigt. Befehls Erweiterungen werden standardmäßig aktiviert.

- Mit dem Befehl **Shift** können Sie eine Batchdatei erstellen, die mehr als 10 Batch Parameter annehmen kann. Wenn Sie mehr als 10 Parameter in der Befehlszeile angeben, werden diejenigen, die nach dem zehnten (**%9**) angezeigt werden, nacheinander in **%9**verschoben.

- Der **Shift** -Befehl hat keine Auswirkung auf den **%\*** Batch-Parameter.

- Es ist kein rückwärts **Verschiebungs** Befehl vorhanden. Nachdem Sie den Befehl **Shift** implementiert haben, können Sie den Batch Parameter (**%0**), der vor der Verschiebung vorhanden war, nicht wiederherstellen.

## <a name="examples"></a>Beispiele

Wenn Sie eine Batchdatei namens " *Mycopy.bat*" verwenden möchten, um eine Liste der Dateien in ein bestimmtes Verzeichnis zu kopieren, geben Sie Folgendes ein:

```
@echo off
rem MYCOPY.BAT copies any number of files
rem to a directory.
rem The command uses the following syntax:
rem mycopy dir file1 file2 ...
set todir=%1
:getfile
shift
if %1== goto end
copy %1 %todir%
goto getfile
:end
set todir=
echo All done
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
