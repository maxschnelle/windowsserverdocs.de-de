---
title: mmc
description: Referenz Artikel für den MMC-Befehl, mit dem Sie eine bestimmte MMC-Konsole öffnen, MMC im Autoren Modus öffnen oder angeben können, um die 32-Bit-oder 64-Bit-Version von MMC zu öffnen.
ms.topic: article
ms.assetid: 7bfa4030-ce42-40fb-922f-2f5145a80872
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f118259bde62d6a9cc193c7451489aebd709d884
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886421"
---
# <a name="mmc"></a>mmc

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe der MMC-Befehlszeilenoptionen können Sie eine bestimmte **MMC** -Konsole öffnen, **MMC** im Autoren Modus öffnen oder angeben, dass die 32-Bit-oder 64-Bit-Version von **MMC** geöffnet ist.

## <a name="syntax"></a>Syntax

```
mmc <path>\<filename>.msc [/a] [/64] [/32]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<path>\<filename>.msc` | startet die **MMC** und öffnet eine gespeicherte Konsole. Sie müssen den gesamten Pfad und den Dateinamen für die gespeicherte Konsolen Datei angeben. Wenn Sie keine Konsolen Datei angeben, öffnet **MMC** eine neue Konsole. |
| /a | Öffnet eine gespeicherte Konsole im Autoren Modus.  Wird zum vornehmen von Änderungen an gespeicherten Konsolen verwendet. |
| /64 | Öffnet die 64-Bit-Version von **MMC** (MMC64). Verwenden Sie diese Option nur, wenn Sie ein 64-Bit-Betriebssystem von Microsoft ausführen und ein 64-Bit-Snap-in verwenden möchten. |
| /32 | Öffnet die 32-Bit-Version von **MMC** (MMC32). Wenn Sie ein Microsoft 64-Bit-Betriebssystem ausführen, können Sie 32-Bit-Snap-Ins ausführen, indem Sie MMC mit dieser Befehlszeilenoption öffnen, wenn Sie über 32-Bit-Snap-Ins verfügen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen

- Sie können Umgebungsvariablen verwenden, um Befehlszeilen oder Verknüpfungen zu erstellen, die nicht vom expliziten Speicherort der Konsolen Dateien abhängen. Wenn sich z. b. der Pfad zu einer Konsolen Datei im Ordner "System" befindet (z **. b. "MMC c:\winnt\system32\ console_name. msc**"), können Sie die erweiterbare Daten Zeichenfolge " **% systemroot%** " verwenden, um den Speicherort anzugeben (**MMC% systemroot% \ System32 \ console_name. msc**). Dies kann hilfreich sein, wenn Sie Aufgaben an Personen in Ihrer Organisation delegieren, die auf verschiedenen Computern arbeiten.

- Wenn Konsolen mithilfe der **/a** -Option geöffnet werden, werden Sie unabhängig vom Standardmodus im Autoren Modus geöffnet. Dadurch wird die Standardmoduseinstellung für Dateien nicht dauerhaft geändert. Wenn Sie diese Option weglassen, öffnet MMC Konsolen Dateien entsprechend ihren Standardeinstellungen für den Modus.

- Nachdem Sie **MMC** oder eine Konsolen Datei im Autoren Modus geöffnet haben, können Sie eine beliebige vorhandene Konsole öffnen, indem Sie im **Konsolen** Menü auf **Öffnen** klicken.

- Sie können die Befehlszeile verwenden, um Verknüpfungen zum Öffnen von **MMC** und gespeicherten Konsolen zu erstellen. Ein Befehlszeilen Befehl funktioniert mit dem Befehl **Ausführen** im **Startmenü** , in einem Eingabe Aufforderungs Fenster, in Verknüpfungen oder in einer beliebigen Batchdatei oder einem beliebigen Programm, das bzw. das den Befehl aufruft.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
