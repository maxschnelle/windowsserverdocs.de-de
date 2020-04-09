---
title: shadow
description: Windows-Befehle Thema für Schatten, mit dem Sie eine aktive Sitzung eines anderen Benutzers auf einem Remotedesktop-Sitzungshost Server remote steuern können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f81d9717-6883-4e14-9508-4b2a87e48ea7 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 90c3202d810257cc94c73b88c5c1627901f54af0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834333"
---
# <a name="shadow"></a>shadow

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht die Remote Steuerung einer aktiven Sitzung eines anderen Benutzers auf einem Remotedesktop-Sitzungshost Server.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\<Sessionname >|Gibt den Namen der Sitzung an, die Sie remote steuern möchten.|
|\<SessionID >|Gibt die ID der Sitzung an, die Sie remote steuern möchten. Verwenden Sie den **Abfrage Benutzer** , um die Liste der Sitzungen und ihre Sitzungs-IDs anzuzeigen.|
|/Server:\<Servername >|Gibt den Remote Desktop-Sitzungs Host Server mit der Sitzung an, die Sie remote steuern möchten. Standardmäßig wird der aktuelle RD-Sitzung Host4-Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie können die Sitzung entweder anzeigen oder aktiv steuern. Wenn Sie die Sitzung eines Benutzers aktiv steuern möchten, können Sie Tastatur-und Mausaktionen für die Sitzung eingeben.
-   Sie können Ihre eigenen Sitzungen (außer der aktuellen Sitzung) jederzeit Remote steuern. Sie müssen jedoch über die Berechtigung "Vollzugriff" oder "Remote Steuerung" verfügen, um eine andere Sitzung Remote zu steuern.
-   Sie können die Remote Steuerung auch mithilfe von Remotedesktopdienste-Manager initiieren.
-   Vor Beginn der Überwachung warnt der Server den Benutzer, dass die Sitzung remote gesteuert wird, es sei denn, diese Warnung ist deaktiviert. Die Sitzung scheint einige Sekunden lang eingefroren zu sein, während Sie auf eine Antwort des Benutzers wartet. Verwenden Sie zum Konfigurieren der Remote Steuerung für Benutzer und Sitzungen das Remotedesktopdienste-Konfigurationstool oder die Remotedesktopdienste Erweiterungen für lokale Benutzer und Gruppen sowie für Active Directory-Benutzer und-Computer.
-   Ihre Sitzung muss in der Lage sein, die Videoauflösung zu unterstützen, die in der Sitzung verwendet wird, für die Sie eine Remote Steuerung durchführt.
-   Die Konsolen Sitzung kann keine Remote Steuerung einer anderen Sitzung durchführt, und Sie kann nicht von einer anderen Sitzung remote gesteuert werden.
-   Wenn Sie die Remote Steuerung beenden möchten (Shadowing), drücken Sie STRG +\* (indem Sie nur \* von der numerischen Tastatur verwenden).

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
-   Zum Schatten der Sitzung 93 geben Sie Folgendes ein:
    ```
    shadow 93
    ```
-   Geben Sie Folgendes ein, um die Sitzungs ACCTG01 zu schattieren
    ```
    shadow ACCTG01
    ```

## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Remotedesktopdienste Befehlsreferenz (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
