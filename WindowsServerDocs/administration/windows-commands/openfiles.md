---
title: openfiles
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83175d8529d9204c6b6d969a3db2aee2775bd0c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852381"
---
# <a name="openfiles"></a>openfiles



Ermöglicht einem Administrator zum Abfragen, anzeigen oder Trennen von Dateien und Verzeichnisse, die auf einem System geöffnet wurden. Außerdem aktiviert oder deaktiviert die Liste der Objekte verwalten globale Systemflag.

Dieses Thema enthält Informationen über die folgenden Befehle aus:
-   [openfiles /disconnect](#BKMK_disconnect)
-   [openfiles /query](#BKMK_query)
-   [openfiles /local](#BKMK_local)

## <a name="BKMK_disconnect"></a>openfiles /disconnect

Ermöglicht einem Administrator zum Trennen von Dateien und Ordnern, die über einen freigegebenen Ordner Remote geöffnet wurden.

### <a name="syntax"></a>Syntax

```
openfiles /disconnect [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/id <OpenFileID>] | [/a <AccessedBy>] | [/o {read | write | read/write}]} [/op <OpenFile>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/s \<System>|Gibt an, dem remoten System für die Verbindung (nach Name oder IP-Adresse). Verwenden Sie keine umgekehrte Schrägstriche. Wenn Sie nicht verwenden, die **/s** Option, den Befehl auf dem lokalen Computer ausgeführt wird, wird standardmäßig. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben werden.|
|/u [\<Domain>\]<UserName>|Führt den Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Wenn Sie nicht verwenden, die **/u** option System Berechtigungen werden standardmäßig verwendet.|
|/ p [\<Kennwort >]|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Option. Wenn Sie nicht verwenden, die **/p** Option aufgefordert, ein Kennwort angezeigt wird, wenn der Befehl ausgeführt wird.|
|/id \<OpenFileID>|Trennt die Verbindung geöffneten Dateien anhand der angegebenen Datei-ID Das Platzhalterzeichen (**&#42;**) kann mit diesem Parameter verwendet werden.</br>Hinweis: Sie können die **Openfiles/Query** Befehl aus, um die Datei-ID suchen|
|/a \<AccessedBy>|Trennt alle geöffneten Dateien im Zusammenhang mit den Benutzernamen ein, die in angegeben ist die *Zugriff durch* Parameter. Das Platzhalterzeichen (**&#42;**) kann mit diesem Parameter verwendet werden.|
|/ o {lesen \| schreiben \| Lese-/Schreibzugriff}|Trennt die Verbindung aller geöffneten Dateien mit dem Wert des angegebenen Modus "open". Gültige Werte sind Lese-, Schreib- oder Lese-/Schreibzugriff. Das Platzhalterzeichen (**&#42;**) kann mit diesem Parameter verwendet werden.|
|/op \<OpenFile>|Trennt alle geöffneten dateiverbindungen, die mit einem bestimmten geöffneten Dateinamen erstellt werden. Das Platzhalterzeichen (**&#42;**) kann mit diesem Parameter verwendet werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="examples"></a>Beispiele

Wenn Sie alle geöffneten Dateien mit der Datei-ID 26843578 trennen möchten, geben Sie Folgendes ein:
```
openfiles /disconnect /id 26843578
```
So trennen Sie alle geöffneten Dateien und Verzeichnisse, die Zugriff durch den Benutzer "Hiropln" Geben Sie Folgendes ein:
```
openfiles /disconnect /a hiropln
```
Wenn Sie alle geöffneten Dateien und Verzeichnisse mit Lese-/Schreibmodus trennen möchten, geben Sie Folgendes ein:
```
openfiles /disconnect /o read/write
```
So trennen Sie das Verzeichnis mit dem Namen der Datei öffnen "C:\TestShare\", unabhängig davon, wer ihn Typ zugreift:
```
openfiles /disconnect /a * /op "c:\testshare\"
```
So trennen Sie alle geöffneten Dateien auf dem Remotecomputer "Srvmain", durch den Benutzer "Hiropln", auf die zugegriffen wird, unabhängig von deren-ID, geben Sie Folgendes ein:
```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="BKMK_query"></a>OPENFILES/Query

Fragt ab und zeigt alle geöffneten Dateien.

### <a name="syntax"></a>Syntax

```
openfiles /query [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/s \<System>|Gibt an, dem remoten System für die Verbindung (nach Name oder IP-Adresse). Verwenden Sie keine umgekehrte Schrägstriche. Wenn Sie nicht verwenden, die **/s** Option, den Befehl auf dem lokalen Computer ausgeführt wird, wird standardmäßig. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben werden.|
|/u [\<Domain>\]<UserName>|Führt den Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Wenn Sie nicht verwenden, die **/u** option System Berechtigungen werden standardmäßig verwendet.|
|/ p [\<Kennwort >]|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Option. Wenn Sie nicht verwenden, die **/p** Option aufgefordert, ein Kennwort angezeigt wird, wenn der Befehl ausgeführt wird.|
|[/ FO {Tabelle \| Liste \| CSV}]|Zeigt die Ausgabe im angegebenen Format. Gültige Werte für *Format* sind:</br>TABELLE:  Zeigt die Ausgabe in einer Tabelle.</br>LISTE: Zeigt die Ausgabe in einer Liste.</br>CSV: Zeigt die Ausgabe in durch Trennzeichen getrennten Format.|
|/nh|Unterdrückt die Kopfzeile der Spalte in der Ausgabe. Nur gültig, wenn die **/Fo** Parametersatz zu **Tabelle** oder **CSV**.|
|/v|Gibt an, dass ausführliche Informationen in der Ausgabe angezeigt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="examples"></a>Beispiele

Zum Abfragen und alle geöffneten Dateien anzuzeigen, geben Sie Folgendes ein:
```
openfiles /query
```
Zum Abfragen, und zeigen alle geöffneten Dateien im Tabellenformat ohne Header, geben Sie Folgendes ein:
```
openfiles /query /fo table /nh
```
Zum Abfragen und alle geöffneten Dateien im Listenformat mit detaillierten Informationen anzuzeigen, geben Sie Folgendes ein:
```
openfiles /query /fo list /v
```
Zum Abfragen und alle geöffneten Dateien auf dem Remotesystem "Srvmain" mithilfe der Anmeldeinformationen für den Benutzer "Hiropln" in der Domäne "Maindom" anzuzeigen, geben Sie Folgendes ein:
```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> In diesem Beispiel wird das Kennwort in der Befehlszeile angegeben. Um zu verhindern, dass das Kennwort, lassen Sie die **/p** Option. Sie werden für das Kennwort aufgefordert werden die nicht auf dem Bildschirm ausgegeben wird.

## <a name="BKMK_local"></a>Openfiles/Local

Aktiviert oder deaktiviert das System globale Flag Objektliste verwalten. Wenn Sie ohne Angabe von Parametern **Openfiles/Local** zeigt den aktuellen Status der globalen Kennzeichnung Objektliste verwalten.

### <a name="syntax"></a>Syntax

```
openfiles /local [on | off]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[auf \| deaktiviert]|Aktiviert oder deaktiviert das System globalen Liste der Objekte verwalten-Flag, das lokalen Dateihandles nachverfolgt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

-   Aktivieren das globale Flag der Liste der Objekte verwalten kann Ihr System verlangsamen.
-   Änderungen, die mithilfe der **auf** oder **aus** Option werden nicht wirksam, bis Sie das System neu starten.

### <a name="examples"></a>Beispiele

Um den aktuellen Status des globalen Flags verwalten die Objektliste zu überprüfen, geben Sie Folgendes ein:
```
openfiles /local
```
Klicken Sie in der Standardeinstellung das globale Flag der Liste der Objekte beizubehalten ist deaktiviert, und die folgende Ausgabe wird angezeigt:
```
INFO: The system global flag 'maintain objects list' is currently disabled.
```
Um die Liste der Objekte verwalten globale Flag aktivieren, geben Sie Folgendes ein:
```
openfiles /local on
```
Die folgende Meldung wird angezeigt, wenn das globale Flag aktiviert ist:
```
SUCCESS: The system global flag 'maintain objects list' is enabled.
         This will take effect after the system is restarted.
```
Um die Liste der Objekte verwalten globale Flag zu deaktivieren, geben Sie Folgendes ein:
```
openfiles /local off
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)