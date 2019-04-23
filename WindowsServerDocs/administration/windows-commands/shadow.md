---
title: shadow
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 125b2971d5d4783ea0b974c45b988cbd1c58a2bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877111"
---
# <a name="shadow"></a>shadow

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ermöglicht Ihnen, die eine aktive Sitzung eines anderen Benutzers auf einem Remotedesktop-Sitzungshost (rd Session Host)-Server Remote zu steuern.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\<SessionName>|Gibt den Namen der Sitzung, die Sie Remote steuern möchten.|
|\<SessionID>|Gibt die ID der Sitzung, die Sie Remote steuern möchten. Verwendung **Abfrage** um die Liste von Sitzungen und die Sitzungs-IDs anzuzeigen.|
|/server:\<ServerName>|Gibt an, den RD-Sitzungshost-Server, die mit der Sitzung, die Sie Remote steuern möchten. Standardmäßig wird der aktuelle RD-Sitzung: Host4-Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen, die ausgeführt wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie können anzeigen oder die Sitzung aktiv steuern. Wenn Sie eine benutzersitzung aktiv steuern möchten, werden Sie können mit Tastatureingaben und Aktionen der Sitzung.
-   Können Sie Ihre eigenen Sitzungen (mit Ausnahme von der aktuellen Sitzung) immer Remote steuern, aber Sie benötigen Full Control-Berechtigung oder die Berechtigung für Remotesteuerung beschränkten Zugriff auf eine andere Sitzung Remote zu steuern.
-   Sie können die Remotesteuerung auch initiieren, mit der Remotedesktopdienste-Manager.
-   Vor Beginn der Überwachung, informiert der Server den Benutzer, die die Sitzung Remote gesteuert werden, es sei denn, diese Warnung deaktiviert ist. Die Sitzung möglicherweise ein paar Sekunden fixiert werden, während er darauf wartet, dass eine Antwort des Benutzers angezeigt. Verwenden Sie zum Konfigurieren der Remotesteuerung für Benutzer und Sitzungen das Remote Desktop Services-Konfigurationstool oder das Remote Desktop Services-Erweiterungen für lokale Benutzer und Gruppen und active Directory-Benutzer und Computer aus.
-   Die Sitzung muss unterstützen die Bildschirmauflösung, die verwendet werden, in der Sitzung, die Sie Remote Steuern des oder der Vorgang fehlschlägt.
-   Die konsolensitzung kann weder Remote Steuern einer anderen Sitzung, noch können sie Remote gesteuert werden von einer anderen Sitzung.
-   Wenn Sie die Remotesteuerung (shadowing) beenden möchten, drücken Sie STRG + * (mit \* auf der Zehnertastatur).

## <a name="BKMK_examples"></a>Beispiele für
-   Geben Sie zum Spiegeln von Sitzung 93:
    ```
    shadow 93
    ```
-   Geben Sie Folgendes ein, um die Sitzung ACCTG01:
    ```
    shadow ACCTG01
    ```

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
