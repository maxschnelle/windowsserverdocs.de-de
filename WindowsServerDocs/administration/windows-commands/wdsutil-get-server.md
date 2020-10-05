---
title: WDSUTIL Get-Server
description: Referenz Artikel zu "WDSUTIL Get-Server", der Informationen vom angegebenen Windows-Bereitstellungsdiensteserver abruft.
ms.topic: reference
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e855724833a90c64dfb3692ccd82fad67a572873
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730227"
---
# <a name="wdsutil-get-server"></a>WDSUTIL Get-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen vom angegebenen Windows-Bereitstellungsdiensteserver ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {config &#124; Images &#124; alle}|Gibt den Typ der zurück zugebende Informationen an.<p>-   **Config** gibt Konfigurationsinformationen zurück.<br />-   **Images** gibt Informationen zu Bildgruppen, Start Abbildern und Installations Abbildern zurück.<br />-   **Alle** gibt Konfigurationsinformationen und Bild Informationen zurück.|
|/Detailed|Sie können diese Option mit **/Show: Images** oder **/Show: all** verwenden, um anzugeben, dass alle Bild Metadaten aus jedem Bild zurückgegeben werden sollen. Wenn die **/detailed** -Option nicht verwendet wird, besteht das Standardverhalten darin, den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zum Server anzuzeigen:
```
wdsutil /Get-Server /Show:Config
```
Geben Sie Folgendes ein, um ausführliche Informationen zum Server anzuzeigen:
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl zum Deaktivieren des Servers](wdsutil-disable-server.md)
- [Befehl "WDSUTIL Enable-Server"](wdsutil-enable-server.md)
- [Befehl "WDSUTIL Initialize-Server"](wdsutil-initialize-server.md)
- [WDSUTIL Set-Server-Befehl](wdsutil-set-server.md)
- [WDSUTIL Start-Server-Befehl](wdsutil-start-server.md)
- [WDSUTIL-Befehl zum Abbrechen von Servern](wdsutil-stop-server.md)
- [WDSUTIL-Befehl "Uninitialize-Server"](wdsutil-uninitialize-server.md)
