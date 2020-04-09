---
title: makecab
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46efbae1d59a85071622df51fc018d0bf73dc504
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840263"
---
# <a name="makecab"></a>makecab

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verpacken vorhandener Dateien in eine CAB-Datei.
## <a name="syntax"></a>Syntax
```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```
#### <a name="parameters"></a>Parameter

|      Parameter       |                                                                        Beschreibung                                                                        |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|       <source>       |                                                                     Die zu komprimierende Datei.                                                                     |
|    <destination>     | Dateiname, der komprimierte Dateien zugewiesen werden soll. Wenn der Name ausgelassen wird, wird das letzte Zeichen des Quell Dateinamens durch einen Unterstrich (_) ersetzt und als Ziel verwendet. |
| /f < directives_file > |                                                   Eine Datei mit **makecab** -Direktiven (kann wiederholt werden).                                                   |
|    /d var =<value>    |                                                          Definiert die Variable mit dem angegebenen Wert.                                                           |
|       /l <dir>       |                                               Speicherort für das Ziel (Standard ist Aktuelles Verzeichnis).                                               |
|       /v [<n>]        |                                                    Ausführlichkeits Grad für das Debuggen festlegen (0 = keine,..., 3 = vollständig).                                                     |
|          /?          |                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                            |

## <a name="remarks"></a>Hinweise
-   Weitere Informationen zu directive_file finden Sie im Microsoft-CAB- [Format](https://go.microsoft.com/fwlink/?LinkId=226852) auf MSDN.

## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

