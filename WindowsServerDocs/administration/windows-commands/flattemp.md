---
title: flattemp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 059a0960-1fd9-4382-87fe-a85d5dccdaea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3fc14a6fe1a355f7c20c130fba3fb1f17e49b6f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872931"
---
# <a name="flattemp"></a>flattemp

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Aktiviert oder deaktiviert die temporären Ordner.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
flattemp {/query | /enable | /disable}
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/query|Fragt die aktuelle Einstellung an.|
|/ Enable /|Ermöglicht die temporären Ordner. Benutzer werden den temporären Ordner freigeben, es sei denn, der der temporäre Ordner in den Basisordner des Benutzers s befindet.|
|/ Disable|Deaktiviert die temporären Ordner. Jeder Benutzer temporären Ordner befinden in einem separaten Ordner (bestimmt durch den Benutzer s Sitzungs-ID).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **Flattemp** Befehl ist nur verfügbar, wenn Sie die Terminalserver-Rollendienst auf einem Computer unter Windows Server 2008 oder den RD-Sitzungshost-Rollendienst auf einem Computer unter Windows Server 2008 R2 installiert haben.
-   Sie benötigen Administratoranmeldeinformationen, um die Ausführung **Flattemp**.
-   Nachdem jeder Benutzer einen eindeutigen temporären Ordner verfügt, verwenden Sie **Flattemp/Enable /** temporären Ordner zu aktivieren.
-   Die Standardmethode zum Erstellen von temporären Ordner für mehrere Benutzer (in der Regel verweist die Umgebungsvariablen TEMP und TMP) ist die Erstellung von Unterordnern im der **\Temp** Ordner mithilfe der LogonID als Name des Unterordners. Wenn die Umgebungsvariable TEMP auf C:\Temp verweist, ist der temporäre Ordner, die der Benutzer LogonID 4 zugewiesen beispielsweise C:\Temp\4. Mithilfe von **Flattemp**, können Sie direkt zum Ordner \Temp zeigen und verhindern, dass die Unterordner bilden. Dies ist nützlich, wenn Sie möchten, dass die temporären Ordner der Benutzer im Basisordner, egal ob auf einem Remotedesktop-Sitzungshost Server lokalen Laufwerk oder auf einem freigegebenen Netzlaufwerk enthalten sein soll. Verwenden Sie die **Flattemp/Enable /** Befehl nur, wenn jeder Benutzer einen separaten temporären Ordner hat.
-   Anwendungsfehler können auftreten, wenn die temporären Ordner des Benutzers auf einem Netzlaufwerk wird. Dies tritt auf, wird das Netzwerk freigegebenen Laufwerk im Netzwerk vorübergehend nicht zugegriffen werden kann. Da die temporären Dateien der Anwendung nicht zugegriffen werden kann oder nicht mehr synchronisiert sind, wird als ob der Datenträger nicht mehr reagiert. Verschieben den temporären Ordner auf einem Netzlaufwerk wird nicht empfohlen. Der Standardwert ist zu temporären Ordner auf der lokalen Festplatte. Wenn unerwartete Verhalten oder die datenträgerbeschädigung: Fehler bei bestimmten Anwendungen auftreten, Stabilisieren Sie Ihr Netzwerk zu, oder verschieben Sie die temporären Ordner zurück, in der lokalen Festplatte.
-   Wenn Sie zu deaktivieren, verwenden separate temporären Ordner, der pro Sitzung **Flattemp** Einstellungen werden ignoriert. Diese Option wird in das Remote Desktop Services-Konfigurationstool festgelegt.

## <a name="BKMK_examples"></a>Beispiele für
-   Um die aktuelle Einstellung für den temporären Ordner anzuzeigen, geben Sie Folgendes ein:
    ```
    flattemp /query
    ```
-   Um die temporären Ordner zu aktivieren, geben Sie Folgendes ein:
    ```
    flattemp /enable
    ```
-   Um die temporären Ordner zu deaktivieren, geben Sie Folgendes ein:
    ```
    flattemp /disable
    ```

## <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)

[Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
