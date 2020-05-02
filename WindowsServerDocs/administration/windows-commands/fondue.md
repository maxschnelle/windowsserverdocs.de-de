---
title: Fondue
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc4467f6-ddbb-4d6d-b51e-5a50a957b8c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2e3b64ff05ab9a539b7734f37b7515c6f9ef123
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725591"
---
# <a name="fondue"></a>Fondue

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert optionale Windows-Features, indem erforderliche Dateien aus Windows Update oder einer anderen durch Gruppenrichtlinie angegebenen Quelle heruntergeladen werden. Die Manifest-Datei für das Feature muss bereits in Ihrem Windows-Abbild installiert sein. 
## <a name="syntax"></a>Syntax
```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootRequest}]
```
#### <a name="parameters"></a>Parameter

|              Parameter              |                                                                                                                                                                     BESCHREIBUNG                                                                                                                                                                     |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /Enable-Feature: <*feature_name*>   |                                                                               Gibt den Namen des optionalen Windows-Features an, das Sie aktivieren möchten. Sie können nur eine Funktion pro Befehlszeile aktivieren. Verwenden Sie zum Aktivieren mehrerer Features "Fondue. exe" für jede Funktion.                                                                                |
|    /CALLER-Name: <*program_name*>    |                                                                                 Gibt den Programm-oder Prozessnamen an, wenn "Fondue. exe" von einem Skript oder einer Batchdatei aus aufgerufen wird. Sie können diese Option verwenden, um den Programmnamen dem sqm-Bericht hinzuzufügen, wenn ein Fehler vorliegt.                                                                                 |
| /Hide-UX: {all &#124; rebootrequest} | Mit **all** können Sie alle Nachrichten für den Benutzer ausblenden, einschließlich Fortschritts-und Berechtigungsanforderungen für den Zugriff auf Windows Update. Wenn die Berechtigung erforderlich ist, schlägt der Vorgang fehl.<p>Verwenden Sie **rebootrequest** , um nur Benutzer Meldungen auszublenden, die die Berechtigung zum Neustarten des Computers anfordern. Verwenden Sie diese Option, wenn Sie über ein Skript zum Steuern von Neustart Anforderungen verfügen. |

## <a name="examples"></a>Beispiele
Um Microsoft .NET Framework 3,5 zu aktivieren, geben Sie Folgendes ein:
```
fondue.exe /enable-feature:NETFX3
```
Wenn Sie Microsoft .NET Framework 3,5 aktivieren möchten, fügen Sie dem sqm-Bericht den Programmnamen hinzu, und zeigen Sie dem Benutzer keine Meldungen an, geben Sie Folgendes ein:
```
fondue.exe /enable-feature:NETFX3 /caller-name:Admin.bat /hide-ux:all
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
  ## <a name="see-also"></a>Weitere Informationen
  [Microsoft .NET Framework 3,5 Bereitstellungs Überlegungen](https://go.microsoft.com/fwlink/?LinkId=248869)
