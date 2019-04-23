---
title: Mithilfe der Get-Server-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: da8bf0fc6e31bd8d0079933f1d7c529c4fe96f42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870981"
---
# <a name="using-the-get-server-command"></a>Mithilfe der Get-Server-Befehl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft Informationen aus dem angegebenen Windows-Bereitstellungsdienste-Server ab.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|/ Anzeigen: {Config &#124; Images &#124; alle}|Gibt den Typ der zurückzugebenden Informationen.<br /><br />-   **Config** gibt Konfigurationsinformationen zurück.<br />-   **Images** gibt Informationen zu Abbildgruppen, Startabbildern und Installationsabbildern zurück.<br />-   **Alle** Konfigurationsinformationen und Informationen zurückgegeben.|
|[/detailed]|Sie können diese Option mit **/Show:Images** oder **/Show:All** um anzugeben, dass alle Metadaten zu Bildern von jedes Bild zurückgegeben werden sollen. Wenn die **/ detailed** Option nicht verwendet wird, ist das Standardverhalten der Image-Name, Beschreibung und Dateinamen zurück.|
## <a name="BKMK_examples"></a>Beispiele für
Um Informationen zum Server anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /Get-Server /Show:Config
```
Um ausführliche Informationen zum Server anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-Server-Befehl](using-the-disable-server-command.md)
[mit dem Enable-Server-Befehl](using-the-enable-server-command.md)
[mithilfe der Initialize-Server-Befehl](using-the-initialize-server-command.md)
[Unterbefehl: Set-Server](subcommand-set-server.md)
[Unterbefehl: Start-Server](subcommand-start-server.md) 
 [ Unterbefehl: Stop-Server](subcommand-stop-server.md)
[die Uninitialize-Server-Option](the-uninitialize-server-option.md)
