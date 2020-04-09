---
title: Get-Server
description: Windows-Befehls Thema für Get-Server, das Informationen vom angegebenen Windows-Bereitstellungsdiensteserver abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65903dc89730eb9d1da23be31ecc1909daece9c4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830843"
---
# <a name="get-server"></a>Get-Server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen vom angegebenen Windows-Bereitstellungsdiensteserver ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {config &#124; Images &#124; all}|Gibt den Typ der zurück zugebende Informationen an.<p>-   **config** gibt Konfigurationsinformationen zurück.<br />-   **Images** gibt Informationen zu Abbild Gruppen, Start Abbildern und Installations Abbildern zurück.<br />-   **alle** Konfigurationsinformationen und Bild Informationen zurück.|
|/Detailed|Sie können diese Option mit **/Show: Images** oder **/Show: all** verwenden, um anzugeben, dass alle Bild Metadaten aus jedem Bild zurückgegeben werden sollen. Wenn die **/detailed** -Option nicht verwendet wird, besteht das Standardverhalten darin, den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um Informationen zum Server anzuzeigen:
```
wdsutil /Get-Server /Show:Config
```
Geben Sie Folgendes ein, um ausführliche Informationen zum Server anzuzeigen:
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Weitere Verweise
- [Der Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des](using-the-disable-server-command.md) Befehls "Enable-Server"
mithilfe des Befehls " [Enable-Server](using-the-enable-server-command.md) "
[mit dem Befehl "Initialize-Server](using-the-initialize-server-command.md) "
[Unterbefehl: Set-Server](subcommand-set-server.md)
[Unterbefehl: Start-Server](subcommand-start-server.md)
[Unterbefehl: beenden-Server](subcommand-stop-server.md)
[die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
