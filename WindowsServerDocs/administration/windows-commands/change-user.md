---
title: change user
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6d32c27e4b4c91b553efe3b55ab38181f51ed4d2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817491"
---
# <a name="change-user"></a>change user

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Installationsmodus für den Server Remote Desktop Session Host (rd Session Host).
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.
## <a name="syntax"></a>Syntax
```
change user {/execute | /install | /query}
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ Ausführen|Ermöglicht die Zuordnung von INI-Datei in das Stammverzeichnis. Dies ist die Standardeinstellung.|
|/ Install|Deaktiviert die Zuordnung der INI-Dateien in das Stammverzeichnis. Alle INI-Dateien gelesen und geschrieben werden, für das Systemverzeichnis. Bei der Installation von Anwendungen auf einen Remotedesktop-Sitzungshostserver, müssen Sie die Zuordnung der INI-Dateien deaktivieren.|
|/query|Zeigt die aktuelle Einstellung für die Zuordnung der INI-Dateien.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
-   Verwendung **Change User/install** vor der Installation einer Anwendung auf die INI-Dateien für die Anwendung im Verzeichnis Systems zu erstellen. Diese Dateien werden als Quelle verwendet, wenn benutzerspezifische INI-Dateien erstellt werden. Verwenden Sie nach der Installation der Anwendung **Benutzer ändern / execute** , um die Zuordnung der INI-Dateien wiederherzustellen.
-   Beim ersten, die Sie beim Ausführen der Anwendung sucht er das Basisverzeichnis für die INI-Dateien. Wenn die INI-Dateien sind im home-Verzeichnis nicht gefunden, aber sich im Systemverzeichnis befinden, kopiert Remote Desktop Services die INI-Dateien in das Stammverzeichnis, um sicherzustellen, dass jeder Benutzer eine eindeutige Kopie der INI-Dateien der Anwendung. Alle neuen INI-Dateien werden im Basisverzeichnis erstellt.
-   Jeder Benutzer muss eine eindeutige Kopie der INI-Dateien für eine Anwendung verfügen. Dies verhindert, dass Instanzen, in denen verschiedene Konfigurationen inkompatible Anwendung, (z. B. verschiedene dem Standard entsprechenden Verzeichnissen oder bildschirmauflösungen) von Benutzern eventuell.
-   Wenn das System ist in den Installationsmodus wechseln (d. h. **Change User/install**), verschiedene Dinge passieren. Alle Registrierungseinträge, die erstellt werden, sind unter schattiert **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentversion\Terminal Server\Install**, entweder in der **\SOFTWARE** Unterschlüssel oder die **\MACHINE** Unterschlüssel. Unterschlüssel hinzugefügt **HKEY_CURrenT_USER** werden unter kopiert die **\SOFTWARE** Unterschlüssel, und der Unterschlüssel hinzugefügt **HKEY_LOCAL_MACHINE** werden kopiert, unter der **\ Computer** Unterschlüssel. Wenn die Anwendung das Windows-Verzeichnis abfragt, mithilfe von Systemaufrufen, z. B. GetWindowsdirectory gibt der Remotedesktop-Sitzungshostserver des Verzeichnisses Systemroot zurück. Wenn INI-Dateieinträge hinzugefügt werden, mithilfe von Systemaufrufen, wie WritePrivateProfileString, werden sie in der INI-Dateien im Verzeichnis Systemroot hinzugefügt.
-   Das System in den Ausführungsmodus zurück (d. h. **ändern Sie die Benutzer aus, und führen Sie**), und die Anwendung versucht, einen Registrierungseintrag unter Lesen **HKEY_CURrenT_USER** , die nicht vorhanden, Remote Desktop Services überprüft, ob eine Kopie des Schlüssels unter vorhanden ist. die **\Terminal Server\Install** Unterschlüssel. Wenn dies der Fall ist, werden die Unterschlüssel an die gewünschte Position unter kopiert **HKEY_CURrenT_USER**. Wenn die Anwendung versucht, die aus einer INI-Datei zu lesen, die nicht vorhanden ist, durchsucht Remote Desktop Services für die Initialisierungsdatei unter dem Systemstamm. Ist die INI-Datei im Stammverzeichnis Systems, wird es in das Unterverzeichnis "\Windows" der home-Verzeichnis des Benutzers kopiert. Wenn die Anwendung über das Windows-Verzeichnis abfragt, gibt der Remotedesktop-Sitzungshostserver Unterverzeichnis "\Windows" des home-Verzeichnis des Benutzers zurück.
-   Wenn Sie sich anmelden, überprüft Remote Desktop Services, ob die System-INI-Dateien neuer als die INI-Dateien auf Ihrem Computer. Wenn die Systemversion neuer ist, ist die INI-Datei entweder ersetzt oder zusammengeführt wird, mit der neueren Version. Dies hängt davon, ob die INISYNC, 0 x 40-bit, ist für diese Initialisierungsdatei. Die vorherige Version der INI-Datei ist Inifile.ctx umbenannt. Wenn die Registrierung des Systems unter Werten der **\Terminal Server\Install** Unterschlüssel aktuellere Ihre Version unter **HKEY_CURrenT_USER**, Ihre Version der Unterschlüssel gelöscht und durch die neue Unterschlüssel ersetzt von **\Terminal Server\Install**.
## <a name="BKMK_examples"></a>Beispiele für
-   Um die Zuordnung der INI-Dateien im Basisverzeichnis deaktivieren möchten, geben Sie Folgendes ein:
    ```
    change user /install
    ```
-   Um-dateizuordnung die INI-Datei im Basisverzeichnis zu aktivieren, geben Sie Folgendes ein:
    ```
    change user /execute
    ```
-   Um die aktuelle Einstellung für die Zuordnung der INI-Dateien anzuzeigen, geben Sie Folgendes ein:
    ```
    change user /query
    ```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[ändern](change.md)
[Remote Desktop Services &#40;"Terminal Services"&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
