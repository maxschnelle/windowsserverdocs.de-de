---
title: fondue
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc4467f6-ddbb-4d6d-b51e-5a50a957b8c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d75d2d9fb57f8888cfc5bf50e2f7796aefc66102
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377087"
---
# <a name="fondue"></a>fondue

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert optionale Windows-Features, indem erforderliche Dateien aus Windows Update oder einer anderen durch Gruppenrichtlinie angegebenen Quelle heruntergeladen werden. Die Manifest-Datei für das Feature muss bereits in Ihrem Windows-Abbild installiert sein. 
## <a name="syntax"></a>Syntax
```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootRequest}]
```
### <a name="parameters"></a>Parameter

|              Parameter              |                                                                                                                                                                     Beschreibung                                                                                                                                                                     |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /Enable-Feature: <*feature_name*>   |                                                                               Gibt den Namen des optionalen Windows-Features an, das Sie aktivieren möchten. Sie können nur eine Funktion pro Befehlszeile aktivieren. Verwenden Sie zum Aktivieren mehrerer Features "Fondue. exe" für jede Funktion.                                                                                |
|    /CALLER-Name: <*program_name*>    |                                                                                 Gibt den Programm-oder Prozessnamen an, wenn "Fondue. exe" von einem Skript oder einer Batchdatei aus aufgerufen wird. Sie können diese Option verwenden, um den Programmnamen dem sqm-Bericht hinzuzufügen, wenn ein Fehler vorliegt.                                                                                 |
| /Hide-UX: {All &#124; rebootrequest} | Mit **all** können Sie alle Nachrichten für den Benutzer ausblenden, einschließlich Fortschritts-und Berechtigungsanforderungen für den Zugriff auf Windows Update. Wenn die Berechtigung erforderlich ist, schlägt der Vorgang fehl.<br /><br />Verwenden Sie **rebootrequest** , um nur Benutzer Meldungen auszublenden, die die Berechtigung zum Neustarten des Computers anfordern. Verwenden Sie diese Option, wenn Sie über ein Skript zum Steuern von Neustart Anforderungen verfügen. |

## <a name="BKMK_Examples"></a>Beispiele
Um Microsoft .NET Framework 3,5 zu aktivieren, geben Sie Folgendes ein:
```
fondue.exe /enable-feature:NETFX3
```
Wenn Sie Microsoft .NET Framework 3,5 aktivieren möchten, fügen Sie dem sqm-Bericht den Programmnamen hinzu, und zeigen Sie dem Benutzer keine Meldungen an, geben Sie Folgendes ein:
```
fondue.exe /enable-feature:NETFX3 /caller-name:Admin.bat /hide-ux:all
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
  ## <a name="see-also"></a>Siehe auch
  [Microsoft .NET Framework 3,5 Bereitstellungs Überlegungen](https://go.microsoft.com/fwlink/?LinkId=248869)
