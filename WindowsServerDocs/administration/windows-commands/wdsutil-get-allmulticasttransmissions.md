---
title: WDSUTIL Get-allmulticastübertragungen
description: Referenz Artikel zu WDSUTIL Get-allmulticasttransmissions, der Informationen zu allen Multicast Übertragungen auf einem Server anzeigt.
ms.topic: reference
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 273581e02784f5a8678be09aaf94a4e380940ea1
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730311"
---
# <a name="wdsutil-get-allmulticasttransmissions"></a>WDSUTIL Get-allmulticastübertragungen

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

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL Get-MulticastTransmission-Befehl](wdsutil-get-multicasttransmission.md)
- [WDSUTIL New-MulticastTransmission-Befehl](wdsutil-new-multicasttransmission.md)
- [WDSUTIL Remove-MulticastTransmission-Befehl](wdsutil-remove-multicasttransmission.md)
- [WDSUTIL Start-MulticastTransmission-Befehl](wdsutil-start-multicasttransmission.md)
