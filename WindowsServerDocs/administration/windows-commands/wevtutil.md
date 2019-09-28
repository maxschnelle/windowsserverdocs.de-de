---
title: wevtutil
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4c791e0-7e59-45c5-aa55-0223b77a4822 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21f3b721a2a08a7fa101ec09f1f11b5e984f0113
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362168"
---
# <a name="wevtutil"></a>wevtutil



Ermöglicht das Abrufen von Informationen über Ereignisprotokolle und Herausgeber. Dieser Befehl dient auch zum Installieren und Deinstallieren von Ereignismanifesten, um Abfragen auszuführen, und zum Exportieren, Archivieren und Löschen von Protokollen. Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

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

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{El \|-Aufzählungs Protokolle}|Zeigt die Namen aller Protokolle an.|
|{GL \| Get-Log} \<logname > [/f: \<format >]|Zeigt die Konfigurationsinformationen für das angegebene Protokoll an, das enthält, ob das Protokoll aktiviert ist oder nicht, die aktuelle maximale Größenbeschränkung des Protokolls und den Pfad zu der Datei, in der das Protokoll gespeichert ist.|
|{SL \| Set-Log} \<logname > [/e: \<aktivierte >] [/i: \<isolation >] [/LFN: \<logpath >] [/RT: \<retention >] [/ab: \<auto >] [/MS: \<maxsize >] [/l: \<level >] [/k: @no__ t-9keywords >] [/ca: 0channel >] [/c: 1config >]|Ändert die Konfiguration des angegebenen Protokolls.|
|{EP \|-Aufzählung-Verleger}|Zeigt die Ereignis Herausgeber auf dem lokalen Computer an.|
|{GP \| Get-Publisher} \<publishername > [/ge: \<metadata >] [/GM: \<message >] [/f: \<Format >]]|Zeigt die Konfigurationsinformationen für den angegebenen Ereignis Herausgeber an.|
|{im \| Install-Manifest} \<manifest >|Installiert Ereignis Herausgeber und-Protokolle aus einem Manifest. Weitere Informationen zu Ereignis Manifesten und zur Verwendung dieses Parameters finden Sie im Windows-Ereignisprotokoll-SDK auf der MSDN-Website (Microsoft Developer Network) ([https://msdn.microsoft.com](https://msdn.microsoft.com)).|
|{um \| Uninstall-Manifest} \<manifest >|Deinstalliert alle Verleger und Protokolle aus einem Manifest. Weitere Informationen zu Ereignis Manifesten und zur Verwendung dieses Parameters finden Sie im Windows-Ereignisprotokoll-SDK auf der MSDN-Website (Microsoft Developer Network) ([https://msdn.microsoft.com](https://msdn.microsoft.com)).|
|{QE \| Query-Events} \<pfad > [/LF: \<logfile >] [/sq: \<structquery >] [/q: \<query >] [/BM: \<bookmark >] [/SBM: \<savebm >] [/RD: \<direction >] [/f: \<format >] [/l: @no_ _T-9locale >] [/c: 0count >] [/e: 1element >]|Liest Ereignisse aus einem Ereignisprotokoll, aus einer Protokolldatei oder mithilfe einer strukturierten Abfrage. Standardmäßig geben Sie einen Protokollnamen für \<path-> an. Wenn Sie jedoch die **/LF** -Option verwenden, muss \<path > ein Pfad zu einer Protokolldatei sein. Wenn Sie den **/SQ** -Parameter verwenden, muss \<path > ein Pfad zu einer Datei sein, die eine strukturierte Abfrage enthält.|
|{Gli \| Get-LogInfo} \<logname > [/LF: \<logfile >]|Zeigt Statusinformationen zu einem Ereignisprotokoll oder einer Protokolldatei an. Wenn die **/LF** -Option verwendet wird, ist \<logname > ein Pfad zu einer Protokolldatei. Zum Abrufen einer Liste von Protokollnamen können Sie **wevtutil El** ausführen.|
|{EPL \| Export-Log} \<pfad > \<exportfile > [/LF: \<logfile >] [/sq: \<structquery >] [/q: \<query >] [/OW: \<überschreibungs >]|Exportiert Ereignisse aus einem Ereignisprotokoll, aus einer Protokolldatei oder mithilfe einer strukturierten Abfrage in die angegebene Datei. Standardmäßig geben Sie einen Protokollnamen für \<path-> an. Wenn Sie jedoch die **/LF** -Option verwenden, muss \<path > ein Pfad zu einer Protokolldatei sein. Wenn Sie die Option **/SQ** verwenden, muss \<path > ein Pfad zu einer Datei sein, die eine strukturierte Abfrage enthält. \<exportfile > ist ein Pfad zu der Datei, in der die exportierten Ereignisse gespeichert werden.|
|{Al \| Archive-Log} \<logpath > [/l: \<locale >]|Archiviert die angegebene Protokolldatei in einem eigenständigen Format. Ein Unterverzeichnis mit dem Namen des Gebiets Schemas wird erstellt, und alle Gebiets Schema spezifischen Informationen werden in diesem Unterverzeichnis gespeichert. Nachdem das Verzeichnis und die Protokolldatei durch Ausführen von **wevtutil Al**erstellt wurden, können Ereignisse in der Datei unabhängig davon gelesen werden, ob der Verleger installiert ist oder nicht.|
|{cl \| Clear-log} \<logname > [/BU: \<backup >]|Löscht Ereignisse aus dem angegebenen Ereignisprotokoll. Die Option **/BU** kann verwendet werden, um die gelöschten Ereignisse zu sichern.|

## <a name="options"></a>Optionen

|       Option       |                                                                                                                                                                                                                                                                 Beschreibung                                                                                                                                                                                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /f: \<format >    |                                                                                                                                                               Gibt an, dass die Ausgabe entweder ein XML-oder Textformat sein soll. Wenn \<format > XML ist, wird die Ausgabe im XML-Format angezeigt. Wenn \<format > Text ist, wird die Ausgabe ohne XML-Tags angezeigt. Der Standardwert ist Text.                                                                                                                                                                |
|   /e: @no__t 0aktivierte >    |                                                                                                                                                                                                                                         Aktiviert oder deaktiviert ein Protokoll. @no__t 0aktivierte > kann "true" oder "false" sein.                                                                                                                                                                                                                                          |
|  /i: \<isolation >   | Legt den Protokoll Isolations Modus fest. \<isolation > kann System, Anwendung oder Benutzer definiert sein. Der Isolations Modus eines Protokolls bestimmt, ob ein Protokoll eine Sitzung mit anderen Protokollen in derselben Isolations Klasse gemeinsam nutzt. Wenn Sie die System Isolation angeben, wird das Ziel Protokoll mindestens über Schreibberechtigungen für das System Protokoll verfügen. Wenn Sie die Anwendungs Isolation angeben, wird das Ziel Protokoll mindestens über Schreibberechtigungen mit dem Anwendungsprotokoll verfügen. Wenn Sie die benutzerdefinierte Isolation angeben, müssen Sie auch mithilfe der **/ca** -Option eine Sicherheits Beschreibung bereitstellen. |
|  /LFN: \<logpath >   |                                                                                                                                                                                                           Definiert den Namen der Protokolldatei. \<logpath > ist ein vollständiger Pfad zu der Datei, in der der Ereignisprotokoll Dienst Ereignisse für dieses Protokoll speichert.                                                                                                                                                                                                           |
|  /RT: \<beibehaltungs Dauer >  |                                                            Legt den Protokoll Beibehaltungs Modus fest. \<retention > kann true oder false sein. Der Protokoll Beibehaltungs Modus bestimmt das Verhalten des Ereignisprotokoll Dienstanbieter, wenn ein Protokoll seine maximale Größe erreicht. Wenn ein Ereignisprotokoll seine maximale Größe erreicht und der Protokoll Beibehaltungs Modus true ist, werden vorhandene Ereignisse beibehalten und eingehende Ereignisse verworfen. Wenn der Protokoll Beibehaltungs Modus false lautet, überschreiben eingehende Ereignisse die ältesten Ereignisse im Protokoll.                                                             |
|    /ab: \<auto >     |                                                                                                                                   Gibt die Protokolldatei für die automatische Sicherung an. \<auto > kann "true" oder "false" sein. Wenn dieser Wert true ist, wird das Protokoll automatisch gesichert, wenn die maximale Größe erreicht wird. Wenn dieser Wert true ist, muss die Aufbewahrung (angegeben mit der Option **/RT** ) auch auf true festgelegt werden.                                                                                                                                    |
|   /MS: \<maxsize->   |                                                                                                                                                                        Legt die maximale Größe des Protokolls in Bytes fest. Die minimale Protokoll Größe beträgt 1048576 Bytes (1024 KB), und Protokolldateien entsprechen immer einem Vielfachen von 64 KB, sodass der von Ihnen eingegebene Wert entsprechend gerundet wird.                                                                                                                                                                         |
|    /l: \<level >     |                                                                                                                                                                     Definiert den Filter für die Ebene des Protokolls. > \<level kann jeder gültige ebenendwert sein. Diese Option gilt nur für Protokolle mit einer dedizierten Sitzung. Sie können einen ebenendfilter entfernen, indem Sie <Level> auf 0 festlegen.                                                                                                                                                                      |
|   /k: \<schlüsselwörter >   |                                                                                                                                                                                         Gibt den Schlüsselwort Filter für das Protokoll an. \<schlüsselwörter > kann eine beliebige gültige 64-Bit-Schlüsselwort Maske sein. Diese Option gilt nur für Protokolle mit einer dedizierten Sitzung.                                                                                                                                                                                         |
|   /ca: \<channel >   |                                                                                                                   Legt die Zugriffsberechtigung für ein Ereignisprotokoll fest. \<channel > ist eine Sicherheits Beschreibung, die die Security Deskriptor Definition Language (SDDL) verwendet. Weitere Informationen zum SDDL-Format finden Sie auf der MSDN-Website (Microsoft Developer Network) ([https://msdn.microsoft.com](https://msdn.microsoft.com)).                                                                                                                    |
|    /c: \<config >    |                                                                                                                                  Gibt den Pfad zu einer Konfigurationsdatei an. Diese Option bewirkt, dass die Protokoll Eigenschaften aus der Konfigurationsdatei gelesen werden, die in \<config > definiert ist. Wenn Sie diese Option verwenden, dürfen Sie keinen <Logname>-Parameter angeben. Der Protokoll Name wird aus der Konfigurationsdatei gelesen.                                                                                                                                   |
|  /ge: \<metadata >   |                                                                                                                                                                                                                 Ruft Metadateninformationen für Ereignisse ab, die von diesem Verleger ausgelöst werden können. \<metadata > kann "true" oder "false" sein.                                                                                                                                                                                                                 |
|   /GM: \<message >   |                                                                                                                                                                                                                       Zeigt die tatsächliche Meldung anstelle der numerischen Nachrichten-ID an. \<message > kann "true" oder "false" sein.                                                                                                                                                                                                                        |
|   /LF: \<logfile >   |                                                                                                                                                                                  Gibt an, dass die Ereignisse aus einem Protokoll oder aus einer Protokolldatei gelesen werden sollen. \<logfile > kann "true" oder "false" sein. True gibt an, dass der-Parameter für den-Befehl der Pfad zu einer Protokolldatei ist.                                                                                                                                                                                   |
| /SQ: \<structquery > |                                                                                                                                                                                Gibt an, dass Ereignisse mit einer strukturierten Abfrage abgerufen werden sollen. \<structquery > kann "true" oder "false" sein. True gibt an, dass <Path> der Pfad zu einer Datei ist, die eine strukturierte Abfrage enthält.                                                                                                                                                                                |
|    /q: \<query >     |                                                                                                                                                                     Definiert die XPath-Abfrage, um die gelesenen oder exportierten Ereignisse zu filtern. Wenn diese Option nicht angegeben wird, werden alle Ereignisse zurückgegeben oder exportiert. Diese Option ist nicht verfügbar, wenn **/SQ** den Wert true hat.                                                                                                                                                                     |
|  /BM: \<-Lesezeichen >   |                                                                                                                                                                                                                                 Gibt den Pfad zu einer Datei an, die ein Lesezeichen aus einer vorherigen Abfrage enthält.                                                                                                                                                                                                                                 |
|   /SBM: \<savebm >   |                                                                                                                                                                                                             Gibt den Pfad zu einer Datei an, die verwendet wird, um ein Lesezeichen für diese Abfrage zu speichern. Die Dateinamenerweiterung sollte ". xml" lauten.                                                                                                                                                                                                              |
|  /RD: \<direction >  |                                                                                                                                                                                                   Gibt die Richtung an, in der Ereignisse gelesen werden. \<direction > kann true oder false sein. Wenn true, werden zuerst die neuesten Ereignisse zurückgegeben.                                                                                                                                                                                                   |
|    /l: \<locale >    |                                                                                                                                                                                          Definiert eine Gebiets Schema Zeichenfolge, die zum Drucken von Ereignis Text in einem bestimmten Gebiets Schema verwendet wird. Nur verfügbar, wenn Ereignisse im Textformat mithilfe der **/f** -Option gedruckt werden.                                                                                                                                                                                          |
|    /c: \<count >     |                                                                                                                                                                                                                                                  Legt die maximale Anzahl der zu lesenden Ereignisse fest.                                                                                                                                                                                                                                                  |
|   /e: \<element >    |                                                                                                                                                           Schließt ein root-Element ein, wenn Ereignisse in XML angezeigt werden. \<element > ist die Zeichenfolge, die innerhalb des Stamm Elements angezeigt werden soll. Beispielsweise würde **/e: root** zu XML führen, das das Stamm Element paar \<root > </root> enthält.                                                                                                                                                            |
|  /oW: \<überschreibungs >  |                                                                                                                                                                 Gibt an, dass die Exportdatei überschrieben werden soll. \<überschreibungs > kann "true" oder "false" sein. Wenn true und die in <Exportfile> angegebene Exportdatei bereits vorhanden ist, wird Sie ohne Bestätigung überschrieben.                                                                                                                                                                 |
|   /BU: \<backup >    |                                                                                                                                                                                                      Gibt den Pfad zu einer Datei an, in der die gelöschten Ereignisse gespeichert werden. Fügen Sie die Erweiterung. evtx in den Namen der Sicherungsdatei ein.                                                                                                                                                                                                       |
|    /r: \<remote >    |                                                                                                                                                                                            Führt den Befehl auf einem Remote Computer aus. \<remote > ist der Name des Remote Computers. Der **im** -und der **um** -Parameter unterstützen keinen Remote Vorgang.                                                                                                                                                                                            |
|   /u: \<username >   |                                                                                                                                                                          Gibt einen anderen Benutzer an, der sich an einem Remote Computer anmelden soll. \<username > ist ein Benutzername in der Form "Domäne \ Benutzer" oder "Benutzer". Diese Option ist nur anwendbar, wenn die **/r** -Option angegeben wird.                                                                                                                                                                          |
|   /p: \<password >   |                                                                                                                                               Gibt das Kennwort für den Benutzer an. Wenn die **/u** -Option verwendet wird und diese Option nicht angegeben ist oder \<password > " *" ist, wird der Benutzer zur Eingabe eines Kennworts aufgefordert. Diese Option ist nur anwendbar, wenn die Option \* @ no__t-1/u @ no__t-2 @ no__t-3 angegeben wird.                                                                                                                                                |
|     /a: \<auth >     |                                                                                                                                                                                             Definiert den Authentifizierungstyp zum Herstellen einer Verbindung mit einem Remote Computer. \<auth > kann Default, Aushandlungs, Kerberos oder NTLM sein. Der Standardwert ist "aushandeln".                                                                                                                                                                                              |
|  /Uni: \<unicode >   |                                                                                                                                                                                                             Zeigt die Ausgabe in Unicode an. \<unicode-> kann "true" oder "false" sein. Wenn <Unicode> true ist, wird die Ausgabe in Unicode ausgegeben.                                                                                                                                                                                                             |

## <a name="remarks"></a>Hinweise

-   Verwenden einer Konfigurationsdatei mit dem SL-Parameter

    Bei der Konfigurationsdatei handelt es sich um eine XML-Datei, die das gleiche Format wie die Ausgabe von wevtutil GL \<logname >/f: XML hat. Das folgende Beispiel zeigt das Format einer Konfigurationsdatei, die die Beibehaltung aktiviert, die automatische Sicherung aktiviert und die maximale Protokoll Größe für das Anwendungsprotokoll festlegt:  
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <channel name="Application" isolation="Application"
    xmlns="https://schemas.microsoft.com/win/2004/08/events">
    <logging>
    <retention>true</retention>
    <autoBackup>true</autoBackup>
    <maxSize>9000000</maxSize>
    </logging>
    <publishing>
    </publishing>
    </channel>
    ```

## <a name="BKMK_examples"></a>Beispiele

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
Installieren Sie Herausgeber und Protokolle aus der Manifest-Datei "mymanifest. xml":
```
wevtutil im myManifest.xml
```
Deinstallieren Sie Herausgeber und Protokolle aus der Manifest-Datei "mymanifest. xml":
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

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
