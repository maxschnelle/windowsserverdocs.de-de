---
title: mmc
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bfa4030-ce42-40fb-922f-2f5145a80872
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d143336db3369b3b319391967db879126d2fb29
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839443"
---
# <a name="mmc"></a>mmc

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe der MMC-Befehlszeilenoptionen können Sie eine bestimmte **MMC** -Konsole öffnen, **MMC** im Autoren Modus öffnen oder angeben, dass die 32-Bit-oder 64-Bit-Version von **MMC** geöffnet ist.
## <a name="syntax"></a>Syntax
```
mmc <path>\<filename>.msc [/a] [/64] [/32]
```
#### <a name="parameters"></a>Parameter

|       Parameter        |                                                                                                 Beschreibung                                                                                                 |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <path>\\<filename>. msc |        startet die **MMC** und öffnet eine gespeicherte Konsole. Sie müssen den gesamten Pfad und den Dateinamen für die gespeicherte Konsolen Datei angeben. Wenn Sie keine Konsolen Datei angeben, öffnet **MMC** eine neue Konsole.         |
|           /a           |                                                               Öffnet eine gespeicherte Konsole im Autoren Modus.  Wird zum vornehmen von Änderungen an gespeicherten Konsolen verwendet.                                                                |
|          /64           |                         Öffnet die 64-Bit-Version von **MMC** (MMC64). Verwenden Sie diese Option nur, wenn Sie ein 64-Bit-Betriebssystem von Microsoft ausführen und ein 64-Bit-Snap-in verwenden möchten.                          |
|          /32           | Öffnet die 32-Bit-Version von **MMC** (MMC32). Wenn Sie ein Microsoft 64-Bit-Betriebssystem ausführen, können Sie 32-Bit-Snap-Ins ausführen, indem Sie MMC mit dieser Befehlszeilenoption öffnen, wenn Sie über 32-Bit-Snap-Ins verfügen. |
|           /?           |                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                     |

## <a name="remarks"></a>Hinweise
- Mithilfe der Befehlszeilenoption "<path> **\\** <filename> **. msc** " können Sie-Umgebungsvariablen verwenden, um Befehlszeilen oder Verknüpfungen zu erstellen, die nicht vom expliziten Speicherort der Konsolen Dateien abhängen. Wenn sich z. b. der Pfad zu einer Konsolen Datei im Ordner "System" befindet (z **. b. "MMC c:\winnt\system32\ console_name. msc**"), können Sie die erweiterbare Daten Zeichenfolge " **% systemroot%** " verwenden, um den Speicherort anzugeben (**MMC% systemroot% \ System32 \ console_name. msc**). Dies kann hilfreich sein, wenn Sie Aufgaben an Personen in Ihrer Organisation delegieren, die auf verschiedenen Computern arbeiten.
- Wenn Sie die Befehlszeilenoption **/a** verwenden, wenn Konsolen mit dieser Option geöffnet werden, werden Sie unabhängig von ihrem Standardmodus im Autoren Modus geöffnet. Dadurch wird die Standardmoduseinstellung für Dateien nicht dauerhaft geändert. Wenn Sie diese Option weglassen, öffnet MMC Konsolen Dateien entsprechend ihren Standardeinstellungen für den Modus.
- Nachdem Sie **MMC** oder eine Konsolen Datei im Autoren Modus geöffnet haben, können Sie eine beliebige vorhandene Konsole öffnen, indem Sie im **Konsolen** Menü auf **Öffnen** klicken.
- Sie können die Befehlszeile verwenden, um Verknüpfungen zum Öffnen von **MMC** und gespeicherten Konsolen zu erstellen. Ein Befehlszeilen Befehl funktioniert mit dem Befehl **Ausführen** im **Startmenü** , in einem Eingabe Aufforderungs Fenster, in Verknüpfungen oder in einer beliebigen Batchdatei oder einem beliebigen Programm, das bzw. das den Befehl aufruft.
  ## <a name="additional-references"></a>Weitere Verweise
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

