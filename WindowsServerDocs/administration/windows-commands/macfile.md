---
title: macfile
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd7646ada96cb02ae434d4ba846da7a9c4dca51b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437474"
---
# <a name="macfile"></a>macfile

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Dateiserver verwaltet für Macintosh-Server, Volumes, Verzeichnisse und Dateien. Sie können administrative Aufgaben automatisieren, indem eine Reihe von Befehlen in Batchdateien und manuell zu starten oder zu vorbestimmten Zeiten. 
-   [So ändern Sie Verzeichnisse auf Macintosh Datenträgern](#BKMK_Moddirs)
-   [Verknüpfen von Daten von einem Macintosh-Datei und Ressource forks](#BKMK_Joinforks)
-   [Ändern Sie die Nachricht für die Anmeldung, und begrenzen von Sitzungen](#BKMK_LogonLimit)
-   [Zum Hinzufügen, ändern oder Entfernen von Macintosh-Datenträgern](#BKMK_addvol)

## <a name="BKMK_Moddirs"></a>So ändern Sie Verzeichnisse auf Macintosh Datenträgern

### <a name="syntax"></a>Syntax
```
macfile directory[/server:\\<computerName>] /path:<directory> [/owner:<OwnerName>] [/group:<GroupName>] [/permissions:<Permissions>]
```

### <a name="parameters"></a>Parameter
-   / Server:\\\\<computerName> Gibt den Server, auf dem ein Verzeichnis geändert. Wenn nicht angegeben, wird der Vorgang auf dem lokalen Computer ausgeführt.
-   / Path:<directory> Erforderlich. Gibt den Pfad zum Verzeichnis, das Sie ändern möchten. Das Verzeichnis muss vorhanden sein. **Macfile Directory** erstellt keine Verzeichnisse.
-   / Owner:<OwnerName> ändert den Besitzer des Verzeichnisses. Wenn nicht angegeben ist, bleibt der Besitzer unverändert.
-   /Group:<GroupName> Gibt an, oder ändert die primäre Macintosh-Gruppe, die mit dem Verzeichnis verknüpft ist. Wenn nicht angegeben, wird die primäre Gruppe nicht geändert.
-   /Permissions:<Permissions> Berechtigungen auf das Verzeichnis für den Besitzer, primäre Gruppe und World (alle) festgelegt. Eine Anzahl 11-stelligen dient zum Festlegen von Berechtigungen. Erteilt die Berechtigung der Zahl 1 und 0 wird eine Berechtigung (z. B. 11111011000). Wenn nicht angegeben ist, bleiben die Berechtigungen nicht geändert.
    Die Position der Ziffer bestimmt die Berechtigung festgelegt ist, wie in der folgenden Tabelle beschrieben.

    |Position|Berechtigungssätze für|
    |------|------------|
    |Erster|OwnerSeeFiles|
    |Zweimal|OwnerSeeFolders|
    |Dritter|OwnerMakechanges|
    |Vierter|GroupSeeFiles|
    |Fünfte|GroupSeeFolders|
    |Sechste|GroupMakechanges|
    |siebte|WorldSeeFiles|
    |Achte|WorldSeeFolders|
    |Neunte|WorldMakechanges|
    |Zehnte|Das Verzeichnis kann nicht umbenannt, verschoben oder gelöscht werden.|
    |Elfte|Die Änderungen gelten für das aktuelle Verzeichnis und alle Unterverzeichnisse.|

-   /?
    Zeigt die Hilfe an der Eingabeaufforderung an.

### <a name="remarks"></a>Hinweise
- enthält die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. **"** <em>Computer Name</em> **"** ).
- Verwendung **MacFile** auf ein vorhandenes Verzeichnis auf einem Macintosh zugängliches Volume für Macintosh-Benutzer verfügbar machen. Die **MacFile** Befehl werden keine Verzeichnisse erstellt. Verwenden der Eingabeaufforderung den Befehl-Manager für Dateiserver oder **Macintosh neuer Ordner** Befehl ein Verzeichnis auf einem Macintosh zugängliches Volume erstellen, bevor Sie verwenden die **Macfile Directory** Befehl.
  ### <a name="BKMK_Examples"></a>Beispiele für
  Im folgende Beispiel ändert die Berechtigungen der Unterverzeichnis Mai Vertriebs-, auf dem Macintosh zugängliches Volume Statistiken, auf das Laufwerk E: des lokalen Servers. Das Beispiel weist Dateien finden Sie unter, siehe Ordner und stellen Änderungen Berechtigungen an den Besitzer und finden Sie unter Dateien und Ordnern finden Sie unter Berechtigungen für alle anderen Benutzer beim verhindern, dass des Verzeichnis, das umbenannt wird, verschoben oder gelöscht.
  ```
  macfile directory /path:"e:\statistics\may sales" /permissions:11111011000
  ```

## <a name="BKMK_Joinforks"></a>Verknüpfen von Daten von einem Macintosh-Datei und Ressource forks

### <a name="syntax"></a>Syntax
```
macfile forkize[/server:\\<computerName>] [/creator:<CreatorName>] [/type:<typeName>]  [/datafork:<Filepath>] [/resourcefork:<Filepath>] /targetfile:<Filepath>
```

### <a name="parameters"></a>Parameter

|         Parameter          |                                                                                                           Beschreibung                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| / Server:\\\\<computerName> |                                                            Gibt den Server für den join der Dateien. Wenn nicht angegeben, wird der Vorgang auf dem lokalen Computer ausgeführt.                                                            |
|   / Creator:<CreatorName>   |                                      Gibt den Ersteller der Datei. Der Macintosh Finder der **/Creator** Befehlszeilenoption, um die Anwendung zu ermitteln, die die Datei erstellt.                                       |
|      / Type:<typeName>      |                                 Gibt den Typ der Datei an. Der Macintosh Finder der **/type** Befehlszeilenoption für den Dateityp innerhalb der Anwendung zu bestimmen, die die Datei erstellt.                                 |
|    /datafork:<Filepath>    |                                                                   Gibt den Speicherort der Daten-Verzweigung, die verknüpft werden. Sie können einen Remotepfad angeben.                                                                   |
|  /resourcefork:<Filepath>  |                                                                 Gibt den Speicherort der Ressource-Verzweigung, die verknüpft werden. Sie können einen Remotepfad angeben.                                                                 |
|   /targetfile:<Filepath>   | Erforderlich. Gibt den Speicherort der Datei, die durch das Verknüpfen einer Fork Daten und eine Verzweigung für die Ressource erstellt wird, oder der Speicherort der Datei, deren Typ oder des Entwicklers, die Sie ändern möchten. Die Datei muss auf dem angegebenen Server sein. |
|             /?             |                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                               |

### <a name="remarks"></a>Hinweise
- enthält die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. **"** <em>Computer Name</em> **"** ).

### <a name="examples"></a>Beispiele
Um die Datei Baumapp auf dem Macintosh zugängliches Volume D:\Release, verwenden das Ressourcenteil C:\Cross\Mac\Appcode, erstellen und diese neue Datei mit dem Macintosh-Clients angezeigt werden, wie eine Anwendung zu erstellen (Macintosh-Anwendungen verwenden Sie den Typ APPL) mit der Ersteller (Signatur ) legen Sie auf Magnolie, Typ:
```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\treeapp
```
So ändern Sie den Dateiersteller in Microsoft Word 5.1, für die Datei WOrd.txt in das Verzeichnis D:\Word Documents\Group-Dateien, auf dem Server \\\SERverA, Typ:
```
macfile forkize /server:\\servera /creator:MSWD /type:TEXT /targetfile:"d:\Word documents\Group files\Word.txt"
```

## <a name="BKMK_LogonLimit"></a>Ändern Sie die Nachricht für die Anmeldung, und begrenzen von Sitzungen
### <a name="syntax"></a>Syntax
```
macfile server [/server:\\<computerName>] [/maxsessions:{Number | unlimited}] [/loginmessage:<Message>]
```

### <a name="parameters"></a>Parameter

|               Parameter                |                                                                                                                                                                           Beschreibung                                                                                                                                                                            |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       / Server:\\\\<computerName>       |                                                                                                                        Gibt den Server für die Parameter ändern. Wenn nicht angegeben, wird der Vorgang auf dem lokalen Computer ausgeführt.                                                                                                                         |
| /maxsessions:{Number &#124; unlimited} |                                                                                         Gibt die maximale Anzahl von Benutzern, die gleichzeitig verwenden die Datei und Druckserver für Macintosh kann. Wenn nicht angegeben, die **Maxsessions** Einstellung für der Server unverändert bleibt.                                                                                         |
|        loginmessage:<Message>         | Änderungen finden Sie unter den Macintosh-Benutzer, bei der Anmeldung auf dem Dateiserver für Macintosh-Server. Die maximale Anzahl von Zeichen für die Nachricht für die Anmeldung ist 199. Wenn nicht angegeben, die **Loginmessage** Nachrichteneigenschaften für der Server unverändert bleibt. Um einer vorhandenen Meldung für die Anmeldung zu entfernen, enthalten die **loginmessage** Parameter, aber lassen die *Nachricht* Variable ist leer. |
|                   /?                   |                                                                                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                               |

### <a name="remarks"></a>Hinweise
- enthält die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. **"** <em>Computer Name</em> **"** ).

### <a name="examples"></a>Beispiele
Ändern die Anzahl von Dateien und Druckserver für Macintosh-Sitzungen, die zulässig sind auf dem lokalen Server aus der aktuellen Einstellung der fünf Sitzungen und zum Hinzufügen der Anmeldung Nachricht "Abmelden vom Server für Macintosh Wenn Sie fertig sind.", Typ:
```
macfile server /maxsessions:5 /loginmessage:"Log off from Server for Macintosh when you are finished."
```

## <a name="BKMK_addvol"></a>Zum Hinzufügen, ändern oder Entfernen von Macintosh-Datenträgern
### <a name="syntax"></a>Syntax
```
macfile volume {/add|/set} [/server:\\<computerName>] /name:<volumeName>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<Password>] [/maxusers:{<Number>>|unlimited}]
macfile volume /remove[/server:\\<computerName>] /name:<volumeName>
```

### <a name="parameters"></a>Parameter

|              Parameter               |                                                                                                                                                                       Beschreibung                                                                                                                                                                        |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          {/add &#124; /set}          |                                                                                                                      Erforderlich, wenn Sie zum Hinzufügen oder Ändern von einem Macintosh zugängliches Volume. Hinzufügen oder ändern das angegebene Volume.                                                                                                                       |
|      / Server:\\\\<computerName>      |                                                                                                             Gibt den Server für das Hinzufügen, ändern oder Entfernen eines Volumes. Wenn nicht angegeben, wird der Vorgang auf dem lokalen Computer ausgeführt.                                                                                                              |
|          / Name:<volumeName>          |                                                                                                                                          Erforderlich. Gibt an, die Volumename hinzugefügt, geändert oder entfernt werden.                                                                                                                                           |
|          / Path:<directory>           |                                                                                                                Erforderlich, und nur gültig, wenn Sie ein Volume hinzufügen möchten. Gibt den Pfad zum Stammverzeichnis des Volumes hinzugefügt werden.                                                                                                                 |
|    /readonly:{true &#124; false}     | Gibt an, ob Benutzer die Dateien im Volume ändern können. Geben Sie "true", um anzugeben, dass Benutzer Dateien auf dem Volume nicht ändern können. Geben Sie "false", um anzugeben, dass Benutzer Dateien im Volume ändern können. Wenn nicht angegeben, wenn Sie ein Volume hinzufügen, sind Änderungen an Dateien zulässig. Wenn nicht angegeben, wenn Sie ein Volume zu ändern der **Readonly** Einstellung für das Volume bleibt unverändert. |
|  /guestsallowed:{true &#124; false}  |      Gibt an, ob Benutzern, die sich als Gäste auf das Volume verwenden können. Geben Sie "true", um anzugeben, dass Gäste auf das Volume verwenden können. Geben Sie "false", um anzugeben, dass das Volume nicht Gäste verwenden können. Wenn nicht angegeben, wenn Sie ein Volume hinzufügen, können Gäste auf das Volume verwenden. Wenn nicht angegeben beim Ändern eines Volumes, die **Guestsallowed** Einstellung für das Volume bleibt unverändert.       |
|         / Password:<Password>         |                                                                               Gibt ein Kennwort, die auf dem Volume benötigt werden. Wenn nicht angegeben, wenn Sie ein Volume hinzufügen, wird kein Kennwort erstellt. Wenn nicht angegeben, wenn Sie ein Volume zu ändern, wird das Kennwort nicht geändert.                                                                               |
| /maxusers:{<Number>>&#124;unlimited} |                                                 Gibt die maximale Anzahl von Benutzern, die gleichzeitig auf die Dateien auf dem Volume verwenden können. Wenn nicht angegeben, wenn Sie ein Volume hinzufügen, kann eine unbegrenzte Anzahl von Benutzern auf das Volume verwenden. Wenn nicht angegeben beim Ändern eines Volumes, die **Maxusers** Wert bleibt unverändert.                                                 |
|               /remove                |                                                                                                                                Erforderlich, wenn Sie einen Macintosh-Volumes entfernen möchten. Entfernt das angegebene Volume an.                                                                                                                                |
|                  /?                  |                                                                                                                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                           |

### <a name="remarks"></a>Hinweise
- enthält die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. **"** <em>Computer Name</em> **"** ).

### <a name="examples"></a>Beispiele
Geben Sie zum Erstellen eines Volumes, die uns Marketing Statistiken auf dem lokalen Server, mit dem Statistiken-Verzeichnis auf dem Laufwerk E aufgerufen und angegeben, dass das Volume von Gästen nicht zugegriffen werden kann:
```
macfile volume /add /name:"US Marketing Statistics" /guestsallowed:false /path:e:\Stats
```
Ändern die Lautstärke oben erstellten nur-Lese und ein Kennwort erforderlich, und legen Sie die maximale Benutzeranzahl in fünf, Typ:
```
macfile volume /set /name:"US Marketing Statistics" /readonly:true /password:saturn /maxusers:5
```
Um ein Volume Landschaftsgestaltung, auf dem Server hinzuzufügen \\\Magnolia, mithilfe von Strukturen Directory Laufwerk E:, und um anzugeben, dass das Volume von Gästen, Typ zugegriffen werden kann:
```
macfile volume /add /server:\\Magnolia /name:"Landscape Design" /path:e:\trees
```
Um das Volume, das Namen Sales Reports auf dem lokalen Server zu entfernen, geben Sie Folgendes ein:
```
macfile volume /remove /name:"Sales Reports"
```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
