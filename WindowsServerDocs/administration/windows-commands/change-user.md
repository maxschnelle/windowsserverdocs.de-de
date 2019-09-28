---
title: change user
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6202f024-8cf5-411e-89b1-ee37ff46499d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 771e39182c17b9a6710e49eff2f5302e539bdbb5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379570"
---
# <a name="change-user"></a>change user

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Installationsmodus für den Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> change user {/execute | /install | /query}
> ```
> ## <a name="parameters"></a>Parameter
> 
> | Parameter |                                                                                                 Beschreibung                                                                                                  |
> |-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | /execute  |                                                                Ermöglicht die Zuordnung von INI-Dateien zum Basisverzeichnis. Dies ist die Standardeinstellung.                                                                 |
> | /install  | Deaktiviert die Zuordnung der INI-Datei zum Basisverzeichnis. Alle INI-Dateien werden gelesen und in das System Verzeichnis geschrieben. Wenn Sie Anwendungen auf einem Remote Desktop-Sitzungs Host Server installieren, müssen Sie die INI-Datei Zuordnung deaktivieren. |
> |  /Query "aus   |                                                                             Zeigt die aktuelle Einstellung für die INI-Datei Zuordnung an.                                                                              |
> |    /?     |                                                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                     |
> 
> ## <a name="remarks"></a>Hinweise
> - Verwenden Sie **Benutzer ändern/install** , bevor Sie eine Anwendung installieren, um INI-Dateien für die Anwendung im System Verzeichnis zu erstellen. Diese Dateien werden als Quelle verwendet, wenn benutzerspezifische ini-Dateien erstellt werden. Verwenden Sie nach der Installation der Anwendung **Change user/execute** , um die Datei Zuordnung der Standard-INI-Datei wiederherzustellen.
> - Wenn Sie die Anwendung zum ersten Mal ausführen, wird das Basisverzeichnis nach den zugehörigen ini-Dateien durchsucht. Wenn die INI-Dateien nicht im Basisverzeichnis gefunden werden, aber im System Verzeichnis gefunden werden, werden Remotedesktopdienste die INI-Dateien in das Basisverzeichnis kopiert, um sicherzustellen, dass jeder Benutzer über eine eindeutige Kopie der INI-Dateien der Anwendung verfügt. Alle neuen ini-Dateien werden im Basisverzeichnis erstellt.
> - Jeder Benutzer muss über eine eindeutige Kopie der INI-Dateien für eine Anwendung verfügen. Dadurch wird verhindert, dass Instanzen, in denen unterschiedliche Benutzer möglicherweise nicht kompatible Anwendungs Konfigurationen aufweisen (z. b. verschiedene Standard Verzeichnisse oder Bildschirmauflösungen).
> - Wenn sich das System im Installationsmodus befindet (d. h. **Benutzer/install ändern**), treten mehrere Dinge auf. Alle Registrierungseinträge, die erstellt werden, werden unter **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Terminal server\install**in den Unterschlüssel **\Software** oder den Unterschlüssel **\Machine** schattiert. Zu **HKEY_CURrenT_USER** hinzugefügte Unterschlüssel werden unter dem Unterschlüssel **\Software** kopiert, und die zu **HKEY_LOCAL_MACHINE** hinzugefügten Unterschlüssel werden unter dem Unterschlüssel **\Machine** kopiert. Wenn die Anwendung das Windows-Verzeichnis mithilfe von Systemaufrufen abfragt (z. b. GetWindowsDirectory), gibt der RD-Sitzungs Host Server das Verzeichnis systemroot zurück. Wenn eine INI-Datei Einträge mithilfe von Systemaufrufen (z. b. "Write-PrivateProfileString") hinzugefügt werden, werden Sie den INI-Dateien im Verzeichnis "SystemRoot" hinzugefügt.
> - Wenn das System in den Ausführungs Modus zurückkehrt (d. h. **Benutzer/Execute ändern**) und die Anwendung versucht, einen Registrierungs Eintrag unter **HKEY_CURrenT_USER** zu lesen, der nicht vorhanden ist, überprüft Remotedesktopdienste, ob eine Kopie des Schlüssels vorhanden ist. der Unterschlüssel **\terminal server\install** . Wenn dies der Fall ist, werden die Unterschlüssel an den entsprechenden Speicherort unter **HKEY_CURrenT_USER**kopiert. Wenn die Anwendung versucht, aus einer nicht vorhandenen ini-Datei zu lesen, sucht Remotedesktopdienste nach dieser INI-Datei im Stammverzeichnis des Systems. Wenn sich die INI-Datei im Stammverzeichnis des Systems befindet, wird Sie in das Unterverzeichnis "\Windows" des Basisverzeichnisses des Benutzers kopiert. Wenn die Anwendung das Windows-Verzeichnis abfragt, gibt der RD-Sitzungs Host Server das Unterverzeichnis "\Windows" des Basisverzeichnisses des Benutzers zurück.
> - Wenn Sie sich anmelden, wird Remotedesktopdienste überprüft, ob die System. ini-Dateien neuer als die INI-Dateien auf dem Computer sind. Wenn die System Version neuer ist, wird die INI-Datei entweder ersetzt oder mit der neueren Version zusammengeführt. Dies hängt davon ab, ob das INISYNC-Bit 0x40 für diese INI-Datei festgelegt ist. Ihre vorherige Version der INI-Datei wurde in "inifile. ctx" umbenannt. Wenn die System Registrierungs Werte unter dem Unterschlüssel **\terminal server\install** neuer als Ihre Version unter **HKEY_CURrenT_USER**sind, wird Ihre Version der Unterschlüssel gelöscht und durch die neuen untergeordneten Schlüssel von **\terminal server\install**ersetzt.
>   ## <a name="BKMK_examples"></a>Beispiele
> - Geben Sie Folgendes ein, um die INI-Datei Zuordnung im Basisverzeichnis zu deaktivieren:
>   ```
>   change user /install
>   ```
> - Geben Sie Folgendes ein, um die INI-Datei Zuordnung im Basisverzeichnis zu aktivieren:
>   ```
>   change user /execute
>   ```
> - Geben Sie Folgendes ein, um die aktuelle Einstellung für die INI-Datei Zuordnung anzuzeigen:
>   ```
>   change user /query
>   ```
>   #### <a name="additional-references"></a>Weitere Verweise
>   [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
>   -[Änderung](change.md)@no__t-[3 &#40;Remotedesktopdienste Befehls&#41; Referenz für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
