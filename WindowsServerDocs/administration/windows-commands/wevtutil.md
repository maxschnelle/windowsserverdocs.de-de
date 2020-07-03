---
title: wevtutil
description: Referenz Artikel zu wevtutil, mit dem Sie Informationen über Ereignisprotokolle und Herausgeber abrufen können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4c791e0-7e59-45c5-aa55-0223b77a4822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f87ab51c0e24f9df421d7540e85d05a534635947
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936644"
---
# <a name="wevtutil"></a>wevtutil



Ermöglicht das Abrufen von Informationen über Ereignisprotokolle und Herausgeber. Dieser Befehl dient auch zum Installieren und Deinstallieren von Ereignismanifesten, um Abfragen auszuführen, und zum Exportieren, Archivieren und Löschen von Protokollen.

## <a name="syntax"></a>Syntax

```
wevtutil [{el | enum-logs}] [{gl | get-log} <Logname> [/f:<Format>]]
[{sl | set-log} <Logname> [/e:<Enabled>] [/i:<Isolation>] [/lfn:<Logpath>] [/rt:<Retention>] [/ab:<Auto>] [/ms:<MaxSize>] [/l:<Level>] [/k:<Keywords>] [/ca:<Channel>] [/c:<Config>]]
[{ep | enum-publishers}]
[{gp | get-publisher} <Publishername> [/ge:<Metadata>] [/gm:<Message>] [/f:<Format>]] [{im | install-manifest} <Manifest>]
[{um | uninstall-manifest} <Manifest>] [{qe | query-events} <Path> [/lf:<Logfile>] [/sq:<Structquery>] [/q:<Query>] [/bm:<Bookmark>] [/sbm:<Savebm>] [/rd:<Direction>] [/f:<Format>] [/l:<Locale>] [/c:<Count>] [/e:<Element>]]
[{gli | get-loginfo} <Logname> [/lf:<Logfile>]]
[{epl | export-log} <Path> <Exportfile> [/lf:<Logfile>] [/sq:<Structquery>] [/q:<Query>] [/ow:<Overwrite>]]
[{al | archive-log} <Logpath> [/l:<Locale>]]
[{cl | clear-log} <Logname> [/bu:<Backup>]] [/r:<Remote>] [/u:<Username>] [/p:<Password>] [/a:<Auth>] [/uni:<Unicode>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{El \| -Aufzählungs Protokolle}|Zeigt die Namen aller Protokolle an.|
|{GL \| Get-Log} \<Logname> [/f: \<Format> ]|Zeigt die Konfigurationsinformationen für das angegebene Protokoll an, das enthält, ob das Protokoll aktiviert ist oder nicht, die aktuelle maximale Größenbeschränkung des Protokolls und den Pfad zu der Datei, in der das Protokoll gespeichert ist.|
|{SL \| set-log} \<Logname> [/e: \<Enabled> ] [/i: \<Isolation> ] [/LFN: \<Logpath> ] [/RT: \<Retention> ] [/ab: \<Auto> ] [/MS: \<MaxSize> ] [/l: \<Level> ] [/k: \<Keywords> ] [/ca: \<Channel> ] [/c: \<Config> ]|Ändert die Konfiguration des angegebenen Protokolls.|
|{EP \| -Aufzählung-Verleger}|Zeigt die Ereignis Herausgeber auf dem lokalen Computer an.|
|{GP \| Get-Publisher} \<Publishername> [/ge: \<Metadata> ] [/GM: \<Message> ] [/f: \<Format> ]]|Zeigt die Konfigurationsinformationen für den angegebenen Ereignis Herausgeber an.|
|{im \| Install-Manifest}\<Manifest>|Installiert Ereignis Herausgeber und-Protokolle aus einem Manifest. Weitere Informationen zu Ereignis Manifesten und zur Verwendung dieses Parameters finden Sie im Windows-Ereignisprotokoll-SDK auf der MSDN-Website (Microsoft Developer Network) ( [https://msdn.microsoft.com](https://msdn.microsoft.com) ).|
|{um \| Uninstall-Manifest}\<Manifest>|Deinstalliert alle Verleger und Protokolle aus einem Manifest. Weitere Informationen zu Ereignis Manifesten und zur Verwendung dieses Parameters finden Sie im Windows-Ereignisprotokoll-SDK auf der MSDN-Website (Microsoft Developer Network) ( [https://msdn.microsoft.com](https://msdn.microsoft.com) ).|
|{QE \| -Abfrage-Ereignisse} \<Path> [/LF: \<Logfile> ] [/sq: \<Structquery> ] [/q: \<Query> ] [/BM: \<Bookmark> ] [/SBM: \<Savebm> ] [/RD: \<Direction> ] [/f: \<Format> ] [/l: \<Locale> ] [/c: \<Count> ] [/e: \<Element> ]|Liest Ereignisse aus einem Ereignisprotokoll, aus einer Protokolldatei oder mithilfe einer strukturierten Abfrage. Standardmäßig geben Sie einen Protokollnamen für an \<Path> . Wenn Sie jedoch die **/LF** -Option verwenden, \<Path> muss ein Pfad zu einer Protokolldatei sein. Wenn Sie den **/SQ** -Parameter verwenden, \<Path> muss ein Pfad zu einer Datei sein, die eine strukturierte Abfrage enthält.|
|{Gli \| Get-LogInfo} \<Logname> [/LF: \<Logfile> ]|Zeigt Statusinformationen zu einem Ereignisprotokoll oder einer Protokolldatei an. Wenn die **/LF** -Option verwendet wird, \<Logname> ist ein Pfad zu einer Protokolldatei. Zum Abrufen einer Liste von Protokollnamen können Sie **wevtutil El** ausführen.|
|{EPL \| -Export-Log} \<Path> \<Exportfile> [/LF: \<Logfile> ] [/sq: \<Structquery> ] [/q: \<Query> ] [/OW: \<Overwrite> ]|Exportiert Ereignisse aus einem Ereignisprotokoll, aus einer Protokolldatei oder mithilfe einer strukturierten Abfrage in die angegebene Datei. Standardmäßig geben Sie einen Protokollnamen für an \<Path> . Wenn Sie jedoch die **/LF** -Option verwenden, \<Path> muss ein Pfad zu einer Protokolldatei sein. Wenn Sie die **/SQ** -Option verwenden, \<Path> muss ein Pfad zu einer Datei sein, die eine strukturierte Abfrage enthält. \<Exportfile>ist ein Pfad zu der Datei, in der die exportierten Ereignisse gespeichert werden.|
|{Al \| Archive-log} \<Logpath> [/l: \<Locale> ]|Archiviert die angegebene Protokolldatei in einem eigenständigen Format. Ein Unterverzeichnis mit dem Namen des Gebiets Schemas wird erstellt, und alle Gebiets Schema spezifischen Informationen werden in diesem Unterverzeichnis gespeichert. Nachdem das Verzeichnis und die Protokolldatei durch Ausführen von **wevtutil Al**erstellt wurden, können Ereignisse in der Datei unabhängig davon gelesen werden, ob der Verleger installiert ist oder nicht.|
|{cl \| Clear-log} \<Logname> [/BU: \<Backup> ]|Löscht Ereignisse aus dem angegebenen Ereignisprotokoll. Die Option **/BU** kann verwendet werden, um die gelöschten Ereignisse zu sichern.|

## <a name="options"></a>Optionen

|       Option       |                                                                                                                                                                                                                                                                 Beschreibung                                                                                                                                                                                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /f\<Format>    |                                                                                                                                                               Gibt an, dass die Ausgabe entweder ein XML-oder Textformat sein soll. Wenn \<Format> XML ist, wird die Ausgabe im XML-Format angezeigt. Wenn \<Format> Text ist, wird die Ausgabe ohne XML-Tags angezeigt. Der Standardwert ist Text.                                                                                                                                                                |
|   /e:\<Enabled>    |                                                                                                                                                                                                                                         Aktiviert oder deaktiviert ein Protokoll. \<Enabled>kann "true" oder "false" sein.                                                                                                                                                                                                                                          |
|  /i\<Isolation>   | Legt den Protokoll Isolations Modus fest. \<Isolation>kann System, Anwendung oder Benutzer definiert sein. Der Isolations Modus eines Protokolls bestimmt, ob ein Protokoll eine Sitzung mit anderen Protokollen in derselben Isolations Klasse gemeinsam nutzt. Wenn Sie die System Isolation angeben, wird das Ziel Protokoll mindestens über Schreibberechtigungen für das System Protokoll verfügen. Wenn Sie die Anwendungs Isolation angeben, wird das Ziel Protokoll mindestens über Schreibberechtigungen mit dem Anwendungsprotokoll verfügen. Wenn Sie die benutzerdefinierte Isolation angeben, müssen Sie auch mithilfe der **/ca** -Option eine Sicherheits Beschreibung bereitstellen. |
|  /lfn:\<Logpath>   |                                                                                                                                                                                                           Definiert den Namen der Protokolldatei. \<Logpath>ist ein vollständiger Pfad zu der Datei, in der der Ereignisprotokoll Dienst Ereignisse für dieses Protokoll speichert.                                                                                                                                                                                                           |
|  imposante\<Retention>  |                                                            Legt den Protokoll Beibehaltungs Modus fest. \<Retention>kann "true" oder "false" sein. Der Protokoll Beibehaltungs Modus bestimmt das Verhalten des Ereignisprotokoll Dienstanbieter, wenn ein Protokoll seine maximale Größe erreicht. Wenn ein Ereignisprotokoll seine maximale Größe erreicht und der Protokoll Beibehaltungs Modus true ist, werden vorhandene Ereignisse beibehalten und eingehende Ereignisse verworfen. Wenn der Protokoll Beibehaltungs Modus false lautet, überschreiben eingehende Ereignisse die ältesten Ereignisse im Protokoll.                                                             |
|    ab\<Auto>     |                                                                                                                                   Gibt die Protokolldatei für die automatische Sicherung an. \<Auto>kann "true" oder "false" sein. Wenn dieser Wert true ist, wird das Protokoll automatisch gesichert, wenn die maximale Größe erreicht wird. Wenn dieser Wert true ist, muss die Aufbewahrung (angegeben mit der Option **/RT** ) auch auf true festgelegt werden.                                                                                                                                    |
|   /MS\<MaxSize>   |                                                                                                                                                                        Legt die maximale Größe des Protokolls in Bytes fest. Die minimale Protokoll Größe beträgt 1048576 Bytes (1024 KB), und Protokolldateien entsprechen immer einem Vielfachen von 64 KB, sodass der von Ihnen eingegebene Wert entsprechend gerundet wird.                                                                                                                                                                         |
|    /l:\<Level>     |                                                                                                                                                                     Definiert den Filter für die Ebene des Protokolls. \<Level>kann ein beliebiger gültiger Level-Wert sein. Diese Option gilt nur für Protokolle mit einer dedizierten Sitzung. Sie können einen Ebenen-Filter entfernen, indem Sie <Level> auf 0 festlegen.                                                                                                                                                                      |
|   /k\<Keywords>   |                                                                                                                                                                                         Gibt den Schlüsselwort Filter für das Protokoll an. \<Keywords>kann eine beliebige gültige 64-Bit-Schlüsselwort Maske sein. Diese Option gilt nur für Protokolle mit einer dedizierten Sitzung.                                                                                                                                                                                         |
|   etwa\<Channel>   |                                                                                                                   Legt die Zugriffsberechtigung für ein Ereignisprotokoll fest. \<Channel>ist eine Sicherheits Beschreibung, die die Security Deskriptor Definition Language (SDDL) verwendet. Weitere Informationen zum SDDL-Format finden Sie auf der MSDN-Website (Microsoft Developer Network) ( [https://msdn.microsoft.com](https://msdn.microsoft.com) ).                                                                                                                    |
|    /c\<Config>    |                                                                                                                                  Gibt den Pfad zu einer Konfigurationsdatei an. Diese Option bewirkt, dass die Protokoll Eigenschaften aus der Konfigurationsdatei gelesen werden, die in definiert ist \<Config> . Wenn Sie diese Option verwenden, dürfen Sie keinen Parameter angeben <Logname> . Der Protokoll Name wird aus der Konfigurationsdatei gelesen.                                                                                                                                   |
|  /ge\<Metadata>   |                                                                                                                                                                                                                 Ruft Metadateninformationen für Ereignisse ab, die von diesem Verleger ausgelöst werden können. \<Metadata>kann "true" oder "false" sein.                                                                                                                                                                                                                 |
|   /GM\<Message>   |                                                                                                                                                                                                                       Zeigt die tatsächliche Meldung anstelle der numerischen Nachrichten-ID an. \<Message>kann "true" oder "false" sein.                                                                                                                                                                                                                        |
|   verlangt\<Logfile>   |                                                                                                                                                                                  Gibt an, dass die Ereignisse aus einem Protokoll oder aus einer Protokolldatei gelesen werden sollen. \<Logfile>kann "true" oder "false" sein. True gibt an, dass der-Parameter für den-Befehl der Pfad zu einer Protokolldatei ist.                                                                                                                                                                                   |
| /SQ\<Structquery> |                                                                                                                                                                                Gibt an, dass Ereignisse mit einer strukturierten Abfrage abgerufen werden sollen. \<Structquery>kann "true" oder "false" sein. Wenn true, <Path> ist der Pfad zu einer Datei, die eine strukturierte Abfrage enthält.                                                                                                                                                                                |
|    /q\<Query>     |                                                                                                                                                                     Definiert die XPath-Abfrage, um die gelesenen oder exportierten Ereignisse zu filtern. Wenn diese Option nicht angegeben wird, werden alle Ereignisse zurückgegeben oder exportiert. Diese Option ist nicht verfügbar, wenn **/SQ** den Wert true hat.                                                                                                                                                                     |
|  Messgerät\<Bookmark>   |                                                                                                                                                                                                                                 Gibt den Pfad zu einer Datei an, die ein Lesezeichen aus einer vorherigen Abfrage enthält.                                                                                                                                                                                                                                 |
|   /sbm:\<Savebm>   |                                                                                                                                                                                                             Gibt den Pfad zu einer Datei an, die verwendet wird, um ein Lesezeichen für diese Abfrage zu speichern. Die Dateinamenerweiterung sollte ". xml" lauten.                                                                                                                                                                                                              |
|  /RD\<Direction>  |                                                                                                                                                                                                   Gibt die Richtung an, in der Ereignisse gelesen werden. \<Direction>kann "true" oder "false" sein. Wenn true, werden zuerst die neuesten Ereignisse zurückgegeben.                                                                                                                                                                                                   |
|    /l:\<Locale>    |                                                                                                                                                                                          Definiert eine Gebiets Schema Zeichenfolge, die zum Drucken von Ereignis Text in einem bestimmten Gebiets Schema verwendet wird. Nur verfügbar, wenn Ereignisse im Textformat mithilfe der **/f** -Option gedruckt werden.                                                                                                                                                                                          |
|    /c\<Count>     |                                                                                                                                                                                                                                                  Legt die maximale Anzahl der zu lesenden Ereignisse fest.                                                                                                                                                                                                                                                  |
|   /e:\<Element>    |                                                                                                                                                           Schließt ein root-Element ein, wenn Ereignisse in XML angezeigt werden. \<Element>die Zeichenfolge, die innerhalb des Stamm Elements angezeigt werden soll. Beispielsweise würde **/e: root** zu XML führen, das das Stamm Element Paar enthält \<root> </root> .                                                                                                                                                            |
|  nieder\<Overwrite>  |                                                                                                                                                                 Gibt an, dass die Exportdatei überschrieben werden soll. \<Overwrite>kann "true" oder "false" sein. Wenn true und die in angegebene Exportdatei <Exportfile> bereits vorhanden ist, wird Sie ohne Bestätigung überschrieben.                                                                                                                                                                 |
|   ECM\<Backup>    |                                                                                                                                                                                                      Gibt den Pfad zu einer Datei an, in der die gelöschten Ereignisse gespeichert werden. Fügen Sie die Erweiterung. evtx in den Namen der Sicherungsdatei ein.                                                                                                                                                                                                       |
|    /r\<Remote>    |                                                                                                                                                                                            Führt den Befehl auf einem Remote Computer aus. \<Remote>der Name des Remote Computers. Der **im** -und der **um** -Parameter unterstützen keinen Remote Vorgang.                                                                                                                                                                                            |
|   /u\<Username>   |                                                                                                                                                                          Gibt einen anderen Benutzer an, der sich an einem Remote Computer anmelden soll. \<Username>ein Benutzername im Format "Domäne \ Benutzer" oder "Benutzer". Diese Option ist nur anwendbar, wenn die **/r** -Option angegeben wird.                                                                                                                                                                          |
|   /p\<Password>   |                                                                                                                                               Gibt das Kennwort für den Benutzer an. Wenn die **/u** -Option verwendet wird und diese Option nicht angegeben ist oder \<Password> ist *, wird der Benutzer zur Eingabe eines Kennworts aufgefordert. Diese Option ist nur anwendbar, wenn die \* \* /u* - \* Option angegeben wird.                                                                                                                                                |
|     /a\<Auth>     |                                                                                                                                                                                             Definiert den Authentifizierungstyp zum Herstellen einer Verbindung mit einem Remote Computer. \<Auth>kann Default, Aushandlungs, Kerberos oder NTLM sein. Der Standardwert ist "aushandeln".                                                                                                                                                                                              |
|  unidirektionale\<Unicode>   |                                                                                                                                                                                                             Zeigt die Ausgabe in Unicode an. \<Unicode>kann "true" oder "false" sein. Wenn <Unicode> den Wert true hat, erfolgt die Ausgabe in Unicode.                                                                                                                                                                                                             |

## <a name="remarks"></a>Hinweise

-   Verwenden einer Konfigurationsdatei mit dem SL-Parameter

    Bei der Konfigurationsdatei handelt es sich um eine XML-Datei, die das gleiche Format wie die Ausgabe von wevtutil GL \<Logname> /f: XML hat. Um das Format einer Konfigurationsdatei zu zeigen, die die Beibehaltung ermöglicht, aktiviert die automatische Sicherung und legt die maximale Protokoll Größe für das Anwendungsprotokoll fest:
    ```
    <?xml version=1.0 encoding=UTF-8?>
    <channel name=Application isolation=Application
    xmlns=https://schemas.microsoft.com/win/2004/08/events>
    <logging>
    <retention>true</retention>
    <autoBackup>true</autoBackup>
    <maxSize>9000000</maxSize>
    </logging>
    <publishing>
    </publishing>
    </channel>
    ```

## <a name="examples"></a>Beispiele

Auflisten der Namen aller Protokolle:
```
wevtutil el
```
Anzeigen von Konfigurationsinformationen über das System Protokoll auf dem lokalen Computer im XML-Format:
```
wevtutil gl System /f:xml
```
Verwenden Sie eine Konfigurationsdatei, um Ereignisprotokoll Attribute festzulegen (Weitere Informationen finden Sie in den Hinweisen zu einem Beispiel für eine Konfigurationsdatei):
```
wevtutil sl /c:config.xml
```
Anzeigen von Informationen zum Microsoft-Windows-EventLog-Ereignis Herausgeber, einschließlich der Metadaten zu den Ereignissen, die der Verleger hervorrufen kann:
```
wevtutil gp Microsoft-Windows-Eventlog /ge:true
```
Installieren Sie Herausgeber und Protokolle aus der myManifest.xml Manifest-Datei:
```
wevtutil im myManifest.xml
```
Deinstallieren Sie Herausgeber und Protokolle aus der myManifest.xml Manifest-Datei:
```
wevtutil um myManifest.xml
```
Zeigen Sie die drei neuesten Ereignisse aus dem Anwendungsprotokoll im Textformat an:
```
wevtutil qe Application /c:3 /rd:true /f:text
```
Zeigen Sie den Status des Anwendungs Protokolls an:
```
wevtutil gli Application
```
Exportieren Sie Ereignisse aus dem System Protokoll nach c:\backup\system0506.evtx:
```
wevtutil epl System C:\backup\system0506.evtx
```
Löschen Sie alle Ereignisse aus dem Anwendungsprotokoll, nachdem Sie Sie im Verzeichnis "c:\admin\backups\a10306.evtx" gespeichert haben:
```
wevtutil cl Application /bu:C:\admin\backups\a10306.evtx
```

#### <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
