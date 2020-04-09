---
title: flattemp
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 059a0960-1fd9-4382-87fe-a85d5dccdaea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a291c102d70ff9166a7bb0261e506792a49dc18
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844573"
---
# <a name="flattemp"></a>flattemp

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert oder deaktiviert flattemporäre Ordner.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
flattemp {/query | /enable | /disable}
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Query "aus|Fragt die aktuelle-Einstellung ab.|
|/enable|Aktiviert flattemporäre Ordner. Benutzer geben den temporären Ordner frei, es sei denn, der temporäre Ordner befindet sich im Basisordner des Benutzers.|
|/Disable|Deaktiviert flache temporäre Ordner. Jeder temporäre Ordner eines Benutzers befindet sich in einem separaten Ordner (festgelegt durch die Sitzungs-ID des Benutzers).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Der Befehl " **flattemp** " ist nur verfügbar, wenn Sie den Terminal Server-Rollen Dienst auf einem Computer installiert haben, auf dem Windows Server 2008 oder der Rollen Dienst "Remote Desktop-Sitzungs Host" auf einem Computer mit Windows Server 2008 R2 ausgeführt wird.
-   Sie müssen über Administrator Anmelde Informationen verfügen, um **flattemp**ausführen zu können.
-   Nachdem jeder Benutzer einen eindeutigen temporären Ordner besitzt, verwenden Sie **flattemp/enable** , um flache temporäre Ordner zu aktivieren.
-   Die Standardmethode zum Erstellen temporärer Ordner für mehrere Benutzer (in der Regel durch die Umgebungsvariablen TEMP und tmp) besteht darin, Unterordner im Ordner **\temp** zu erstellen, indem Sie die LogonId als Unterordner Namen verwenden. Wenn beispielsweise die Temp-Umgebungsvariable auf c:\temp zeigt, lautet der temporäre Ordner, der der Benutzer Anmelde-ID 4 zugewiesen ist, c:\Temp\4. Mithilfe von **flattemp**können Sie direkt auf den Ordner "\temp" zeigen und verhindern, dass Unterordner gebildet werden. Dies ist hilfreich, wenn Sie möchten, dass die temporären Benutzerordner in Basis Ordnern enthalten sind, egal ob auf einem lokalen Laufwerk des Remote Desktop-Sitzungs Host Servers oder auf einem freigegebenen Netzwerklaufwerk. Sie sollten den Befehl **flattemp/enable** nur verwenden, wenn jeder Benutzer über einen separaten temporären Ordner verfügt.
-   Möglicherweise treten Anwendungsfehler auf, wenn sich der temporäre Ordner des Benutzers auf einem Netzlaufwerk befindet. Dieser Fehler tritt auf, wenn das freigegebene Netzwerklaufwerk im Netzwerk vorübergehend nicht mehr verfügbar ist. Da die temporären Dateien der Anwendung entweder nicht zugänglich sind oder nicht synchronisiert sind, antwortet sie so, als ob der Datenträger angehalten wurde. Es wird nicht empfohlen, den temporären Ordner auf ein Netzwerklaufwerk zu verschieben. Der Standardwert besteht darin, temporäre Ordner auf der lokalen Festplatte beizubehalten. Wenn bei bestimmten Anwendungen unerwartetes Verhalten oder Datenträger Beschädigungs Fehler auftreten, stabilisieren Sie das Netzwerk, oder verschieben Sie die temporären Ordner zurück auf die lokale Festplatte.
-   Wenn Sie die Verwendung separater temporärer Ordner pro Sitzung deaktivieren, werden die **flattemp** -Einstellungen ignoriert. Diese Option wird im Remotedesktopdienste-Konfigurationstool festgelegt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
-   Geben Sie Folgendes ein, um die aktuelle Einstellung für flattemporär Ordner anzuzeigen:
    ```
    flattemp /query
    ```
-   Geben Sie Folgendes ein, um flache temporäre Ordner zu aktivieren:
    ```
    flattemp /enable
    ```
-   Um flache temporäre Ordner zu deaktivieren, geben Sie Folgendes ein:
    ```
    flattemp /disable
    ```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
