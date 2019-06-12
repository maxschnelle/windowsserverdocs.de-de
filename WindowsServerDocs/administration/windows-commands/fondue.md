---
title: fondue
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: bcbbbf80f25f77d1feb83f358401e4d14da3d354
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439218"
---
# <a name="fondue"></a>fondue

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Können optionale Features von Windows durch Herunterladen der erforderlichen Dateien aus Windows Update oder einer anderen Quelle, die von der Gruppenrichtlinie angegeben. Die Manifestdatei für die Funktion muss bereits in Ihrem Windows-Image installiert sein. 
## <a name="syntax"></a>Syntax
```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootRequest}]
```
### <a name="parameters"></a>Parameter

|              Parameter              |                                                                                                                                                                     Beschreibung                                                                                                                                                                     |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  / Enable-Feature: <*Featurename*>   |                                                                               Gibt den Namen des optionalen Windows-Features, die Sie aktivieren möchten. Sie können nur eine Funktion pro über die Befehlszeile aktivieren. Verwenden Sie fondue.exe für jede Funktion, um mehrere Funktionen zu aktivieren.                                                                                |
|    /caller-Name: <*Program_name*>    |                                                                                 Gibt den Namen Programm oder Prozess aus, wenn Sie aus einem Skript oder Batch fondue.exe aufrufen. Sie können diese Option verwenden, um den Namen des Programms für die SQM-Bericht hinzufügen, wenn ein Fehler auftritt.                                                                                 |
| /hide-ux:{all &#124; rebootRequest} | Verwendung **alle** So blenden Sie alle Nachrichten, die dem Benutzer, einschließlich Status und die Berechtigung zugriffsanforderungen für Windows Update aus. Wenn die Berechtigung erforderlich ist, schlägt der Vorgang fehl.<br /><br />Verwendung **RebootRequest** benutzermeldungen in der die Berechtigung zum Neustart des Computers nur ausblenden. Verwenden Sie diese Option, wenn Sie ein Skript verfügen, Steuerelemente Anforderungen einen Neustart. |

## <a name="BKMK_Examples"></a>Beispiele für
Um Microsoft .NET Framework 3.5 zu aktivieren, geben Sie Folgendes ein:
```
fondue.exe /enable-feature:NETFX3
```
Um Microsoft .NET Framework 3.5 zu aktivieren, fügen Sie den Namen des Programms für die SQM-Bericht, und Meldungen an den Benutzer, der Typ nicht angezeigt:
```
fondue.exe /enable-feature:NETFX3 /caller-name:Admin.bat /hide-ux:all
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
  ## <a name="see-also"></a>Siehe auch
  [Überlegungen zur Bereitstellung von Microsoft .NET Framework 3.5](https://go.microsoft.com/fwlink/?LinkId=248869)
