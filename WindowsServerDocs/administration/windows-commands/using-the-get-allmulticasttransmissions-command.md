---
title: Verwenden des Befehls Get-allmulticasttransmissions
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 644684ffb356ef07120bc391e3d3da2daf768eaf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363343"
---
# <a name="using-the-get-allmulticasttransmissions-command"></a>Verwenden des Befehls Get-allmulticasttransmissions

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
## <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                                                                                   Erläuterung                                                                                                                                                                                                                                                                    |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |                                                                                                                                                                                 Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                  |
|         [/Show]         | **Windows Server 2008**<br /><br />/Show: Clients: zeigt Informationen zu Client Computern an, die mit den Multicast Übertragungen verbunden sind.<br /><br />**Windows Server 2008 R2**<br /><br />Show: {Boot &#124; install &#124; all}-der Typ des zurück zugebende Bilds.                                Beim **Start** werden nur Start Abbild Übertragungen zurückgegeben.                                  **Install** gibt nur Installations Abbild Übertragungen zurück. **Alle** gibt beide Bild Typen zurück. |
|                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|    /Details: Clients     |                                                                                                                                                                                              Wird nur für Windows Server 2008 R2 unterstützt. Falls vorhanden, werden Clients angezeigt, die mit der Übertragung verbunden sind.                                                                                                                                                                                               |
| [/ExcludedeletePending] |                                                                                                                                                                                                                                              Schließt alle deaktivierten Übertragungen aus der Liste aus.                                                                                                                                                                                                                                               |

## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu allen Übertragungen anzuzeigen:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Show:All` geben Sie Folgendes ein, um Informationen über alle Übertragungen außer deaktivierte Übertragungen anzuzeigen:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`
  #### <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [mithilfe des Befehls Get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
   mithilfe des Befehls[New-MulticastTransmission](using-the-new-multicasttransmission-command.md)
   mit[dem Befehl Remove-](using-the-remove-multicasttransmission-command.md)MulticastTransmission 
  [ Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
