---
title: mmc
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bfa4030-ce42-40fb-922f-2f5145a80872
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 403f7569eaa2380d26cda805c40b1a623743952c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842011"
---
# <a name="mmc"></a>mmc

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Verwenden die Mmc-Befehlszeilenoptionen, können Sie eine bestimmte öffnen **Mmc** -Konsole öffnen **Mmc** im Autorenmodus oder angeben, dass die 32-Bit oder 64-Bit-Version des **Mmc** wird geöffnet.
## <a name="syntax"></a>Syntax
```
mmc <path>\<filename>.msc [/a] [/64] [/32]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<path>\\<filename>.msc|Startet **Mmc** und öffnet eine gespeicherte Konsole. Sie müssen den vollständigen Pfad und Namen für die Datei gespeicherte Konsole angeben. Wenn Sie keine Datei für eine Konsolenanwendung angeben **Mmc** öffnet eine neue Konsole.|
|/a|Öffnet eine gespeicherte Konsole im Autorenmodus an.  Verwendet, um gespeicherte Konsolen zu ändern.|
|/64|Öffnet die 64-Bit-Version des **Mmc** (mmc64). Verwenden Sie diese Option nur, wenn Sie ein Microsoft-64-Bit-Betriebssystem ausgeführt werden und ein 64-Bit-Snap-in verwendet werden soll.|
|/32|Öffnet die 32-Bit-Version des **Mmc** (mmc32). Bei einem Microsoft-64-Bit-Betriebssystem ausgeführt wird, können Sie die 32-Bit-Snap-ins mit Mmc öffnen, klicken Sie mit dieser Befehlszeilenoption ausführen, wenn Sie nur 32-Bit-Snap-ins verfügen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
-   Mithilfe der <path> **\\** <filename> **.msc** Befehlszeilenoption Sie Umgebungsvariablen verwenden können, erstellen über die Befehlszeilen oder Verknüpfungen, die nicht von den expliziten abhängen Speicherort der Dateien der Konsole. Z. B. der Pfad zur Datei für eine Konsolenanwendung ist im Ordner "System" (z. B. **Mmc c:\winnt\system32\console_name.msc**), können Sie die erweiterbare Zeichenfolge **%SystemRoot%** den Speicherort angeben (**mmc%systemroot%\system32\console_name.msc**). Dies kann nützlich sein, wenn Sie Aufgaben delegieren, um Personen in Ihrer Organisation, die auf verschiedenen Computern arbeiten.
-   Mithilfe der **/a** Befehlszeilenoption bei Konsolen mit dieser Option geöffnet sind, werden sie im Autorenmodus, unabhängig von ihrer Standardmodus geöffnet. Dadurch wird die Einstellung der Modus für Dateien dauerhaft nicht geändert; Wenn Sie diese Option auslassen, die Mmc Konsolendateien gemäß ihrer Einstellungen für die Standard-Modus geöffnet.
-   Nach dem Öffnen **Mmc** oder eine Konsolendatei im Autorenmodus, können Sie alle vorhandenen Konsole öffnen, indem Sie auf **öffnen** auf der **Konsole** Menü.
-   Sie können die Befehlszeile verwenden, zum Erstellen von Verknüpfungen zum Öffnen **Mmc** und Konsolen gespeichert. Befehlszeile arbeitet mit der **ausführen** Befehl die **starten** Menü in jedes Eingabeaufforderungsfenster, in Verknüpfungen oder in jedem Batchdatei oder ein Programm, das den Befehl aufruft.
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)

