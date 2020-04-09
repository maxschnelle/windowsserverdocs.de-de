---
title: Get-allmulticastübertragungen
description: Windows-Befehls Thema für Get-allmulticasttransmissions, das Informationen zu allen Multicast Übertragungen auf einem Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c81db5a5d5ebb9bcc5e2d00165d5c944c687fd97
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831329"
---
# <a name="get-allmulticasttransmissions"></a>Get-allmulticastübertragungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu allen Multicast Übertragungen auf einem Server an.

## <a name="syntax"></a>Syntax
für Windows Server 2008:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:Clients] [/ExcludedeletePending]
```
für Windows Server 2008 R2:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:{Boot | Install | All}] [/details:Clients]  [/ExcludedeletePending]
```
### <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                                                                                   Erklärung                                                                                                                                                                                                                                                                    |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |                                                                                                                                                                                 Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                  |
|         [/Show]         | **Windows Server 2008**<p>/Show: Clients: zeigt Informationen zu Client Computern an, die mit den Multicast Übertragungen verbunden sind.<p>**Windows Server 2008 R2**<p>Show: {Boot &#124; install &#124; all}-der Typ des zurück zugebende Bilds.                                Beim **Start** werden nur Start Abbild Übertragungen zurückgegeben.                                  **Install** gibt nur Installations Abbild Übertragungen zurück. **Alle** gibt beide Bild Typen zurück. |
|                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|    /Details: Clients     |                                                                                                                                                                                              Wird nur für Windows Server 2008 R2 unterstützt. Falls vorhanden, werden Clients angezeigt, die mit der Übertragung verbunden sind.                                                                                                                                                                                               |
| [/ExcludedeletePending] |                                                                                                                                                                                                                                              Schließt alle deaktivierten Übertragungen aus der Liste aus.                                                                                                                                                                                                                                               |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu allen Übertragungen anzuzeigen:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2 `wdsutil /Get-AllMulticastTransmissions /Show:All`: zum Anzeigen von Informationen zu allen Übertragungen außer deaktivierten Übertragungen geben Sie Folgendes ein:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`
  ## <a name="additional-references"></a>Weitere Verweise
  - Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [mithilfe des Befehls Get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
  [mithilfe des Befehls New-MulticastTransmission](using-the-new-multicasttransmission-command.md)
  [mit dem Befehl Remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md)
  [Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
