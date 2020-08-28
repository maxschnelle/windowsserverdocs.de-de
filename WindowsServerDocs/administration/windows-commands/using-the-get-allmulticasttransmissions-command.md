---
title: Get-allmulticastübertragungen
description: Referenz Artikel zu Get-allmulticasttransmissions, der Informationen zu allen Multicast Übertragungen auf einem Server anzeigt.
ms.topic: reference
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0c7c4e77c2ad23fab864839cde03ed4f4806c80
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035958"
---
# <a name="get-allmulticasttransmissions"></a>Get-allmulticastübertragungen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
|         [/Show]         | **Windows Server 2008**<p>/Show: Clients: zeigt Informationen zu Client Computern an, die mit den Multicast Übertragungen verbunden sind.<p>**Windows Server 2008 R2**<p>Anzeigen: {Boot &#124; install &#124; all}-der Typ des Abbilds, das zurückgegeben werden soll.                                Beim **Start** werden nur Start Abbild Übertragungen zurückgegeben.                                  **Install** gibt nur Installations Abbild Übertragungen zurück. **Alle** gibt beide Bild Typen zurück. |
|                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|    /Details: Clients     |                                                                                                                                                                                              Wird nur für Windows Server 2008 R2 unterstützt. Falls vorhanden, werden Clients angezeigt, die mit der Übertragung verbunden sind.                                                                                                                                                                                               |
| [/ExcludedeletePending] |                                                                                                                                                                                                                                              Schließt alle deaktivierten Übertragungen aus der Liste aus.                                                                                                                                                                                                                                               |

## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu allen Übertragungen anzuzeigen:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Show:All` Geben Sie Folgendes ein, um Informationen zu allen Übertragungen außer deaktivierten Übertragungen anzuzeigen:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
   [Verwenden des Befehls](using-the-get-multicasttransmission-command.md) 
   Get-MulticastTransmission [Verwenden des New-MulticastTransmission-Befehls](using-the-new-multicasttransmission-command.md) 
   [Verwenden des Remove-MulticastTransmission-Befehls](using-the-remove-multicasttransmission-command.md) 
   [Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
