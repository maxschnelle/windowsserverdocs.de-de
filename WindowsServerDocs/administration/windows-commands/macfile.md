---
title: macfile
description: Referenz Artikel für den MacFile-Befehl, der den Datei Server für Macintosh-Server, Volumes, Verzeichnisse und Dateien verwaltet.
ms.topic: reference
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 06095d99c6cfbdc51fd28f51f9bc06f08d959edf
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023694"
---
# <a name="macfile"></a>macfile

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwaltet den Datei Server für Macintosh-Server, Volumes, Verzeichnisse und Dateien. Sie können administrative Aufgaben automatisieren, indem Sie eine Reihe von Befehlen in Batch Dateien einschließen und manuell oder zu vordefinierten Zeiten starten.

## <a name="modify-directories-in-macintosh-accessible-volumes"></a>Ändern von Verzeichnissen in auf Macintosh zugänglichen Volumes

So ändern Sie den Verzeichnisnamen, den Speicherort, den Besitzer, die Gruppe und die Berechtigungen für auf Macintosh zugängliche Volumes

### <a name="syntax"></a>Syntax

```
macfile directory[/server:\\<computername>] /path:<directory> [/owner:<ownername>] [/group:<groupname>] [/permissions:<permissions>]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /server:`\\<computername>` | Gibt den Server an, auf dem ein Verzeichnis geändert werden soll. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt. |
| /Path`<directory>` | Gibt den Pfad zu dem Verzeichnis an, das Sie ändern möchten. Dieser Parameter ist erforderlich. **Hinweis:** Das Verzeichnis muss vorhanden sein, und das Verzeichnis " **MacFile** " erstellt keine Verzeichnisse. |
| /Owner`<ownername>` | Ändert den Besitzer des Verzeichnisses. Wenn der Name nicht angezeigt wird, ändert sich der Besitzer Name nicht. |
| Kreis`<groupname>` | Gibt die primäre Macintosh-Gruppe an, die dem Verzeichnis zugeordnet ist, oder ändert Sie. Wenn diese Angabe ausgelassen wird, bleibt die primäre Gruppe unverändert. |
| Griff`<permissions>` | Legt Berechtigungen für das Verzeichnis für den Besitzer, die primäre Gruppe und die Welt (alle) fest. Dabei muss es sich um eine elf stellige Zahl handeln, bei der die Zahl 1 die Berechtigung und die Berechtigung 0 (z. b. 11111011000) erteilt. Wenn dieser Parameter ausgelassen wird, bleiben die Berechtigungen unverändert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

##### <a name="position-of-permissions-digit"></a>Position der Berechtigungs Ziffer

Die Position der Berechtigungs Ziffer bestimmt, welche Berechtigung festgelegt wird, einschließlich:

| Position | Sets-Berechtigung |
| -------- | --------------- |
| First | Besitzer Dateien |
| Sekunde | Besitzer Ordner |
| Third | Besitzmakechanges |
| Vierter | GroupSeeFiles |
| 5. | Groupseedner |
| 6. | GroupMakeChanges |
| Siebten | Worldseefiles |
| Platz | Worldseedner |
| När | WorldMakeChanges |
| Zehnten | Das Verzeichnis kann nicht umbenannt, verschoben oder gelöscht werden. |
| Stündigen | Die Änderungen gelten für das aktuelle Verzeichnis und alle Unterverzeichnisse. |

##### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z `<computer name>` . b. "").

- Verwenden Sie das **Verzeichnis "MacFile** ", um ein vorhandenes Verzeichnis auf einem auf Macintosh zugänglichen Volume für Macintosh-Benutzer verfügbar zu machen. Der Befehl " **Macfile Directory** " erstellt keine Verzeichnisse.

- Erstellen Sie mit dem Datei-Manager, der Eingabeaufforderung oder dem **Macintosh New Folder** -Befehl ein Verzeichnis auf einem auf Macintosh zugänglichen Volume, bevor Sie den Befehl " **Macfile Directory** " verwenden.

#### <a name="examples"></a>Beispiele

Wenn Sie " *Dateien*anzeigen", " *Ordner*anzeigen" und " *Änderungen ändern* " für den Besitzer zuweisen möchten, geben Sie die *Ordner* Berechtigungen für alle anderen Benutzer an, und verhindern Sie, dass das Verzeichnis umbenannt, verschoben oder gelöscht wird, indem Sie Folgendes eingeben:

```
macfile directory /path:e:\statistics\may sales /permissions:11111011000
```

Wenn das Unterverzeichnis " *Sales*" ist, das sich in der auf Macintosh zugänglichen Volumen *Statistik*befindet, auf dem e:\ Laufwerk des lokalen Servers.

## <a name="join-a-macintosh-files-data-and-resource-forks"></a>Beitreten zu den Daten und Ressourcen Verzweigungen einer Macintosh-Datei

Zum Angeben des Servers, auf dem die Dateien verknüpft werden sollen, der Dateityp, in dem sich die Daten Verzweigung befindet, der Speicherort der Ressourcen Verzweigung und der Speicherort der Ausgabedatei.

### <a name="syntax"></a>Syntax

```
macfile forkize[/server:\\<computername>] [/creator:<creatorname>] [/type:<typename>]  [/datafork:<filepath>] [/resourcefork:<filepath>] /targetfile:<filepath>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /server:`\\<computername>` | Gibt den Server an, auf dem Dateien verknüpft werden sollen. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt. |
| Hersteller`<creatorname>` | Gibt den Ersteller der Datei an. Der Macintosh-Finder verwendet die Befehlszeilenoption **/Creator** , um die Anwendung zu ermitteln, die die Datei erstellt hat. |
| /Type`<typename>` | Gibt den Dateityp an. Der Macintosh-Finder verwendet die Befehlszeilenoption **/Type** , um den Dateityp innerhalb der Anwendung zu ermitteln, von der die Datei erstellt wurde. |
| /datafork:`<filepath>` | Gibt den Speicherort der Daten Verzweigung an, die verknüpft werden soll. Sie können einen Remote Pfad angeben. |
| /resourcefork:`<filepath>` | Gibt den Speicherort der Ressourcenverzweigung an, der verknüpft werden soll. Sie können einen Remote Pfad angeben. |
| targetfile`<filepath>` | Gibt den Speicherort der Datei an, die durch den Beitritt zu einer Daten Verzweigung und einer Ressourcen Verzweigung erstellt wird, oder gibt den Speicherort der Datei an, deren Typ oder Ersteller Sie ändern. Die Datei muss sich auf dem angegebenen Server befinden. Dieser Parameter ist erforderlich. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

##### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z `<computer name>` . b. "").

#### <a name="examples"></a>Beispiele

So erstellen Sie die Datei *tree_app* auf dem vom Macintosh zugänglichen *Volume d:\Release*mit der Ressourcen Verzweigung *c:\cross\mac\appcode*, und damit diese neue Datei den Macintosh-Clients als Anwendung angezeigt wird (Macintosh-Anwendungen verwenden den Typ *Appl*), wobei der Ersteller (Signatur) auf *Magnolia*festgelegt ist, geben Sie Folgendes ein:

```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\tree_app
```

Um den Datei Ersteller in *Microsoft Word 5,1*zu ändern, geben Sie für die Datei *Word.txt* im Verzeichnis *d:\Word documents\group files*auf dem Server * \\ Servera*Folgendes ein:

```
macfile forkize /server:\\ServerA /creator:MSWD /type:TEXT /targetfile:d:\Word documents\Group files\Word.txt
```

## <a name="change-the-sign-in-message-and-limit-sessions"></a>Ändern der Anmelde Nachricht und beschränken von Sitzungen

Zum Ändern der Anmelde Nachricht, die angezeigt wird, wenn sich ein Benutzer beim Datei Server für den Macintosh-Server anmeldet und die Anzahl der Benutzer einschränkt, die gleichzeitig Datei-und Druckserver für Macintosh verwenden können.

### <a name="syntax"></a>Syntax

```
macfile server [/server:\\<computername>] [/maxsessions:{number | unlimited}] [/loginmessage:<message>]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |------------ |
| /server:`\\<computername>` | Gibt den Server an, auf dem die Parameter geändert werden sollen. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt. |
| MaxSessions`{number | unlimited}` | Gibt die maximale Anzahl von Benutzern an, die gleichzeitig Datei-und Druckserver für Macintosh verwenden können. Wenn der Wert nicht angegeben wird, bleibt die **MaxSessions** -Einstellung für den Server unverändert. |
| /loginmessage:`<message>` | Ändert die Nachricht, die Macintosh-Benutzer bei der Anmeldung beim Datei Server für Macintosh-Server sehen. Die maximale Anzahl von Zeichen für die Anmelde Nachricht beträgt 199. Wenn der Wert nicht ausgelassen wird, bleibt die **loginmessage** -Nachricht für den Server unverändert. Wenn Sie eine vorhandene Anmelde Nachricht entfernen möchten, schließen Sie den **/loginmessage** -Parameter ein, lassen Sie die *Nachrichten* Variable jedoch leer. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

##### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z `<computer name>` . b. "").

#### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Anzahl zulässiger Dateien und Druck Server für Macintosh-Sitzungen auf dem lokalen Server in fünf Sitzungen zu ändern und die Anmelde Nachricht "Abmelden von Server für Macintosh, wenn Sie fertig sind" hinzuzufügen:

```
macfile server /maxsessions:5 /loginmessage:Sign off from Server for Macintosh when you are finished
```

## <a name="add-change-or-remove-macintosh-accessible-volumes"></a>Hinzufügen, ändern oder Entfernen von Macintosh-zugänglichen Volumes

Zum Hinzufügen, ändern oder Entfernen eines auf Macintosh zugänglichen Volumes.

### <a name="syntax"></a>Syntax

```
macfile volume {/add|/set} [/server:\\<computername>] /name:<volumename>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<password>] [/maxusers:{<number>>|unlimited}]
macfile volume /remove[/server:\\<computername>] /name:<volumename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `{/add | /set}` | Erforderlich, wenn ein auf Macintosh zugängliches Volume hinzugefügt oder geändert wird. Fügt das angegebene Volume hinzu oder ändert es. |
| /server:`\\<computername>` | Gibt den Server an, auf dem ein Volume hinzugefügt, geändert oder entfernt werden soll. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt. |
| /Name`<volumename>` | Erforderlich. Gibt den Volumenamen an, der hinzugefügt, geändert oder entfernt werden soll. |
| /Path`<directory>` | Erforderlich und gültig nur, wenn Sie ein Volume hinzufügen. Gibt den Pfad zum Stammverzeichnis des hinzu zufügenden Volumes an. |
| ReadOnly`{true | false}` | Gibt an, ob Benutzer Dateien im Volume ändern können. Verwenden Sie **true** , um anzugeben, dass Benutzer Dateien im Volume nicht ändern können. Verwenden Sie **false** , um anzugeben, dass Benutzer Dateien im Volume ändern können. Wenn beim Hinzufügen eines Volumes weggelassen wird, sind Änderungen an Dateien zulässig. Wenn beim Ändern eines Volumes ausgelassen wird, bleibt die Schreib **geschützte Einstellung für** das Volume unverändert. |
| /guestsallowed:`{true | false}` | Gibt an, ob Benutzer, die sich als Gäste anmelden, das Volume verwenden können. Verwenden Sie **true** , um anzugeben, dass Gäste das Volume verwenden können. Verwenden Sie **false** , um anzugeben, dass Gäste das Volume nicht verwenden können. Wenn Sie beim Hinzufügen eines Volumes ausgelassen werden, können Gäste das Volume verwenden. Wenn beim Ändern eines Volumes ausgelassen wird, bleibt die Einstellung **GUESTSALLOWED** für das Volume unverändert. |
| /Password`<password>` | Gibt ein Kennwort an, das für den Zugriff auf das Volume erforderlich ist. Wenn beim Hinzufügen eines Volumes kein Kennwort angegeben wird, wird kein Kennwort erstellt. Wenn beim Ändern eines Volumes kein Kennwort angegeben wird, bleibt das Kennwort unverändert. |
| /maxusers:`{<number>> | unlimited}` | Gibt die maximale Anzahl von Benutzern an, die die Dateien auf dem Volume gleichzeitig verwenden können. Wenn der Wert beim Hinzufügen eines Volumes weggelassen wird, kann das Volume von einer unbegrenzten Anzahl von Benutzern verwendet werden. Wenn beim Ändern eines Volumes ausgelassen wird, bleibt der Wert **maxUsers** unverändert.                                                 |
| /remove | Erforderlich, wenn Sie ein auf Macintosh zugängliches Volume entfernen. entfernt das angegebene Volume. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

##### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z `<computer name>` . b. "").

#### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Volume mit der Bezeichnung " *US-Marketing Statistik* " auf dem lokalen Server zu erstellen, indem Sie das Verzeichnis " *Stats* " im Laufwerk E verwenden und angeben, dass der Zugriff auf das Volume nicht von Gästen

```
macfile volume /add /name:US Marketing Statistics /guestsallowed:false /path:e:\Stats
```

Geben Sie Folgendes ein, um das oben erstellte Volume so zu ändern, dass es schreibgeschützt ist, um ein Kennwort anzufordern und die maximale Anzahl von Benutzern auf fünf festzulegen:

```
macfile volume /set /name:US Marketing Statistics /readonly:true /password:saturn /maxusers:5
```

Geben Sie zum Hinzufügen eines Volumes namens *Landscape Design*auf der Server- * \\ Magnolie*unter Verwendung des *Trees* -Verzeichnisses im Laufwerk E ein, und um anzugeben, dass auf das Volume von Gästen zugegriffen werden kann, geben Sie Folgendes ein:

```
macfile volume /add /server:\\Magnolia /name:Landscape Design /path:e:\trees
```

Geben Sie Folgendes ein, um das Volume namens *Sales Reports* auf dem lokalen Server zu entfernen:

```
macfile volume /remove /name:Sales Reports
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
