---
title: Verwenden des Befehls Get-Server
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c7e0ee4529858b16cdc63ea1d6d358a190b8b1a9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392118"
---
# <a name="using-the-get-server-command"></a>Verwenden des Befehls Get-Server

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen vom angegebenen Windows-Bereitstellungsdiensteserver ab.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {config &#124; Images &#124; all}|Gibt den Typ der zurück zugebende Informationen an.<br /><br />-   **config** gibt Konfigurationsinformationen zurück.<br />-   -**Bilder** gibt Informationen zu Bildgruppen, Start Abbildern und Installations Abbildern zurück.<br />bei -    werden**alle** Konfigurationsinformationen und Bild Informationen zurückgegeben.|
|/Detailed|Sie können diese Option mit **/Show: Images** oder **/Show: all** verwenden, um anzugeben, dass alle Bild Metadaten aus jedem Bild zurückgegeben werden sollen. Wenn die **/detailed** -Option nicht verwendet wird, besteht das Standardverhalten darin, den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zum Server anzuzeigen:
```
wdsutil /Get-Server /Show:Config
```
Geben Sie Folgendes ein, um ausführliche Informationen zum Server anzuzeigen:
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem](using-the-disable-server-command.md)Befehl "Enable-Server" 
 mit dem Befehl "[Enable-Server](using-the-enable-server-command.md)" 
 mithilfe des Befehls "[Initialize-Server](using-the-initialize-server-command.md)" 
[Unterbefehl "Set-Server](subcommand-set-server.md)
[ " Unterbefehl: Start-Server](subcommand-start-server.md)1[Unterbefehl: beenden-Server](subcommand-stop-server.md)3[die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
