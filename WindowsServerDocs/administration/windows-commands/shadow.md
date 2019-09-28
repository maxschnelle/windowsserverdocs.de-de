---
title: shadow
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f81d9717-6883-4e14-9508-4b2a87e48ea7 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb2fad4b0a553e736755f2dc56e5d88297a1fef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383962"
---
# <a name="shadow"></a>shadow

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht die Remote Steuerung einer aktiven Sitzung eines anderen Benutzers auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\<sessionname >|Gibt den Namen der Sitzung an, die Sie remote steuern möchten.|
|\<sessionid >|Gibt die ID der Sitzung an, die Sie remote steuern möchten. Verwenden Sie den **Abfrage Benutzer** , um die Liste der Sitzungen und ihre Sitzungs-IDs anzuzeigen.|
|/Server: \<servername >|Gibt den Remote Desktop-Sitzungs Host Server mit der Sitzung an, die Sie remote steuern möchten. Standardmäßig wird der aktuelle RD-Sitzung Host4-Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie können die Sitzung entweder anzeigen oder aktiv steuern. Wenn Sie die Sitzung eines Benutzers aktiv steuern möchten, können Sie Tastatur-und Mausaktionen für die Sitzung eingeben.
-   Sie können Ihre eigenen Sitzungen (außer der aktuellen Sitzung) jederzeit Remote steuern. Sie müssen jedoch über die Berechtigung "Vollzugriff" oder "Remote Steuerung" verfügen, um eine andere Sitzung Remote zu steuern.
-   Sie können die Remote Steuerung auch mithilfe von Remotedesktopdienste-Manager initiieren.
-   Vor Beginn der Überwachung warnt der Server den Benutzer, dass die Sitzung remote gesteuert wird, es sei denn, diese Warnung ist deaktiviert. Die Sitzung scheint einige Sekunden lang eingefroren zu sein, während Sie auf eine Antwort des Benutzers wartet. Verwenden Sie zum Konfigurieren der Remote Steuerung für Benutzer und Sitzungen das Remotedesktopdienste-Konfigurationstool oder die Remotedesktopdienste Erweiterungen für lokale Benutzer und Gruppen sowie für Active Directory-Benutzer und-Computer.
-   Ihre Sitzung muss in der Lage sein, die Videoauflösung zu unterstützen, die in der Sitzung verwendet wird, für die Sie eine Remote Steuerung durchführt.
-   Die Konsolen Sitzung kann keine Remote Steuerung einer anderen Sitzung durchführt, und Sie kann nicht von einer anderen Sitzung remote gesteuert werden.
-   Wenn Sie die Remote Steuerung beenden möchten (Shadowing), drücken Sie STRG + \* (nur mit \* von der numerischen Tastatur).

## <a name="BKMK_examples"></a>Beispiele
-   Zum Schatten der Sitzung 93 geben Sie Folgendes ein:
    ```
    shadow 93
    ```
-   Geben Sie Folgendes ein, um die Sitzungs ACCTG01 zu schattieren
    ```
    shadow ACCTG01
    ```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Remotedesktopdienste &#40;Befehlsreferenz&#41; für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
