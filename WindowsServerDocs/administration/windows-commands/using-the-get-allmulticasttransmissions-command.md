---
title: Mithilfe des Befehls Get-AllMulticastTransmissions
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b05f8802a288d80960cf79356675cb9adce9c260
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440532"
---
# <a name="using-the-get-allmulticasttransmissions-command"></a>Mithilfe des Befehls Get-AllMulticastTransmissions

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen zu allen Multicastübertragungen auf einem Server an.
## <a name="syntax"></a>Syntax
für WindowsServer 2008:
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
| [/Server:<Server name>] |                                                                                                                                                                                 Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.                                                                                                                                                                                  |
|         [/Show]         | **Windows Server 2008**<br /><br />/Show:Clients - zeigt Informationen über Clientcomputer, die mit der Multicastübertragungen verbunden sind.<br /><br />**Windows Server 2008 R2**<br /><br />Anzeigen: {Boot &#124; installieren &#124; alle}: der Typ des zurückzugebenden Bilds.                                **Start** gibt nur Image Übertragungen zu starten.                                  **Installieren Sie** gibt nur Image Übertragungen installieren. **Alle** gibt beides image Typen. |
|                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|    /details:clients     |                                                                                                                                                                                              Nur unterstützt für Windows Server 2008 R2. Falls vorhanden, werden Clients, die mit der Übertragung verbunden sind, angezeigt.                                                                                                                                                                                               |
| [/ExcludedeletePending] |                                                                                                                                                                                                                                              Schließt alle deaktivierten Übertragungen aus der Liste aus.                                                                                                                                                                                                                                               |

## <a name="BKMK_examples"></a>Beispiele für
Um Informationen über alle Übertragungen anzuzeigen, geben Sie Folgendes ein:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Show:All` Um Informationen über alle Übertragungen mit Ausnahme von deaktivierten Übertragungen anzuzeigen, geben Sie Folgendes ein:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`
  #### <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [mit dem Befehl Get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
  [mit dem Befehl new-MulticastTransmission](using-the-new-multicasttransmission-command.md) 
   [Mit dem Befehl Remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md)
  [Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
