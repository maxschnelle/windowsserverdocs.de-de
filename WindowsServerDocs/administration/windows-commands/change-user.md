---
title: change user
description: Referenz Thema für den Befehl "Benutzer ändern", mit dem der Installationsmodus für den Remotedesktop-Sitzungshost Server geändert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6202f024-8cf5-411e-89b1-ee37ff46499d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de96280f42f1e3002c4379390367856dcdcb885a
ms.sourcegitcommit: 568b924d32421256f64abfee171304f1daf320d2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "85070185"
---
# <a name="change-user"></a>change user

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Installationsmodus für den Remotedesktop-Sitzungshost-Server.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
change user {/execute | /install | /query}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /execute | Ermöglicht die Zuordnung von INI-Dateien zum Basisverzeichnis. Dies ist die Standardeinstellung. |
| /install | Deaktiviert die Zuordnung der INI-Datei zum Basisverzeichnis. Alle INI-Dateien werden gelesen und in das System Verzeichnis geschrieben. Sie müssen die INI-Datei Zuordnung deaktivieren, wenn Sie Anwendungen auf einem Remotedesktop-Sitzungshost Server installieren. |
| /Query "aus | Zeigt die aktuelle Einstellung für die INI-Datei Zuordnung an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Verwenden Sie **Benutzer ändern/install** , bevor Sie eine Anwendung installieren, um INI-Dateien für die Anwendung im System Verzeichnis zu erstellen. Diese Dateien werden als Quelle verwendet, wenn benutzerspezifische ini-Dateien erstellt werden. Verwenden Sie nach der Installation der Anwendung **Change user/execute** , um die Datei Zuordnung der Standard-INI-Datei wiederherzustellen.

- Wenn Sie die APP zum ersten Mal ausführen, wird das Basisverzeichnis nach den zugehörigen ini-Dateien durchsucht. Wenn die INI-Dateien nicht im Basisverzeichnis gefunden werden, aber im System Verzeichnis gefunden werden, werden Remotedesktopdienste die INI-Dateien in das Basisverzeichnis kopiert, um sicherzustellen, dass jeder Benutzer über eine eindeutige Kopie der INI-Datei der Anwendung verfügt. Alle neuen ini-Dateien werden im Basisverzeichnis erstellt.

- Jeder Benutzer muss über eine eindeutige Kopie der INI-Dateien für eine Anwendung verfügen. Dadurch wird verhindert, dass Instanzen, in denen unterschiedliche Benutzer möglicherweise nicht kompatible Anwendungs Konfigurationen aufweisen (z. b. verschiedene Standard Verzeichnisse oder Bildschirmauflösungen).

- Wenn das System **Change user/install**ausgeführt wird, treten mehrere Dinge auf. Alle Registrierungseinträge, die erstellt werden, werden unter **HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows NT\CurrentVersion\Terminal server\install**im Unterschlüssel **\Software** oder Unterschlüssel **\Machine** schattiert. Unterschlüssel, die **HKEY_CURRENT_USER** hinzugefügt werden, werden unter dem Unterschlüssel **\Software** kopiert, und die zu **HKEY_LOCAL_MACHINE** hinzugefügten Unterschlüssel werden unter dem Unterschlüssel **\Machine** kopiert. Wenn die Anwendung das Windows-Verzeichnis mithilfe von Systemaufrufen abfragt (z. b. GetWindowsDirectory), gibt der RD-Sitzungs Host Server das Verzeichnis systemroot zurück. Wenn eine INI-Datei Einträge mithilfe von Systemaufrufen (z. b. "Write-PrivateProfileString") hinzugefügt werden, werden Sie den INI-Dateien im Verzeichnis "SystemRoot" hinzugefügt.

- Wenn das System zurückkehrt, um die **Benutzer/Execute zu ändern**, und die Anwendung versucht, einen Registrierungs Eintrag unter **HKEY_CURRENT_USER** zu lesen, der nicht vorhanden ist, prüft Remotedesktopdienste, ob eine Kopie des Schlüssels unter dem Unterschlüssel **\terminal server\install** vorhanden ist. Wenn dies der Fall ist, werden die Unterschlüssel an den entsprechenden Speicherort unter **HKEY_CURRENT_USER**kopiert. Wenn die Anwendung versucht, aus einer nicht vorhandenen ini-Datei zu lesen, sucht Remotedesktopdienste nach dieser INI-Datei im Stammverzeichnis des Systems. Wenn sich die INI-Datei im Stammverzeichnis des Systems befindet, wird Sie in das Unterverzeichnis "\Windows" des Basisverzeichnisses des Benutzers kopiert. Wenn die Anwendung das Windows-Verzeichnis abfragt, gibt der RD-Sitzungs Host Server das Unterverzeichnis "\Windows" des Basisverzeichnisses des Benutzers zurück.

- Wenn Sie sich anmelden, wird Remotedesktopdienste überprüft, ob die System. ini-Dateien neuer als die INI-Dateien auf dem Computer sind. Wenn die System Version neuer ist, wird die INI-Datei entweder ersetzt oder mit der neueren Version zusammengeführt. Dies hängt davon ab, ob das INISYNC-Bit 0x40 für diese INI-Datei festgelegt ist. Ihre vorherige Version der INI-Datei wurde in "inifile. ctx" umbenannt. Wenn die System Registrierungs Werte unter dem Unterschlüssel **\terminal server\install** neuer als Ihre Version unter **HKEY_CURRENT_USER**sind, wird Ihre Version der Unterschlüssel gelöscht und durch die neuen untergeordneten Schlüssel von **\terminal server\install**ersetzt.

## <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die INI-Datei Zuordnung im Basisverzeichnis zu deaktivieren:

  ```
  change user /install
  ```

- Geben Sie Folgendes ein, um die INI-Datei Zuordnung im Basisverzeichnis zu aktivieren:

  ```
  change user /execute
  ```

- Geben Sie Folgendes ein, um die aktuelle Einstellung für die INI-Datei Zuordnung anzuzeigen:

  ```
  change user /query
  ```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "ändern"](change.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
