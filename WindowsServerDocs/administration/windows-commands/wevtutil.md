---
title: wevtutil
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d99b1f1da3bcf2c59236ce9a8c41f933b100bf7a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440101"
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
|{el \| Enum-Logs}|Zeigt die Namen aller Protokolle.|
|{Gl \| Get-Log} \<"logName" > [/ f:\<Format >]|Zeigt die Konfigurationsinformationen für das angegebene Protokoll gehört, ob das Protokoll oder nicht aktiviert ist, die aktuelle maximale größenbeschränkung für die das Protokoll und den Pfad zur Datei, in dem das Protokoll gespeichert ist.|
|{sl \| Set-Log} \<"logName" > [/ e:\<aktiviert >] [/ i:\<Isolation >] [/ Lfn:\<Logpath >] [/ rt:\<Aufbewahrung >] [/ Ab:\<automatisch >] [/ ms:\< MaxSize-Wert >] [/ l:\<Ebene >] [/ k:\<Schlüsselwörter >] [/ ca:\<Kanal >] [/ c:\<Config >]|Ändert die Konfiguration des angegebenen Protokolls.|
|{Ep \| Enum-Verleger}|Zeigt den Ereignisherausgeber auf dem lokalen Computer.|
|{Gp \| Get-Publisher} \<Publishername > [/ ge:\<Metadaten >] [/ gm:\<Nachricht >] [/ f:\<Format >]]|Zeigt die Konfigurationsinformationen für den angegebenen Ereignisherausgeber.|
|{Im \| Install-Manifest} \<Manifest >|Installiert-Ereignisherausgeber und-Protokolle aus einem Manifest an. Weitere Informationen zum ereignismanifeste und verwenden diesen Parameter finden Sie unter dem Windows-Ereignisprotokoll-SDK auf der Website Microsoft Developers Network (MSDN) ([https://msdn.microsoft.com](https://msdn.microsoft.com)).|
|{um \| deinstallieren-Manifest} \<Manifest >|Deinstalliert alle Herausgeber und Protokolle aus einem Manifest an. Weitere Informationen zum ereignismanifeste und verwenden diesen Parameter finden Sie unter dem Windows-Ereignisprotokoll-SDK auf der Website Microsoft Developers Network (MSDN) ([https://msdn.microsoft.com](https://msdn.microsoft.com)).|
|{Qe \| Abfrageereignisse –} \<Pfad > [/ lf:\<Protokolldatei >] [/ sq:\<Structquery >] [/ f:\<Abfrage >] [/ bm:\<Lesezeichen >] [/ Sbm:\<Savebm >] [/ rd:\< Richtung >] [/ f:\<Format >] [/ l:\<Gebietsschema >] [/ c:\<Anzahl >] [/ e:\<Element >]|Liest Ereignisse aus einem Ereignisprotokoll, aus einer Protokolldatei oder über eine strukturierte Abfrage. Standardmäßig geben Sie einen Protokollnamen für \<Pfad >. Allerdings bei Verwendung der **/LF** klicken Sie dann die option \<Pfad > muss ein Pfad in eine Protokolldatei sein. Bei Verwendung der **/SQ** Parameter \<Pfad > muss ein Pfad zu einer Datei, die eine strukturierte Abfrage enthält.|
|{Gli \| Get-Loginfo} \<"logName" > [/ lf:\<Protokolldatei >]|Zeigt Statusinformationen zu einem Ereignisprotokoll oder eine Protokolldatei an. Wenn die **/LF** -Option verwendet wird, \<"logName" > ist ein Pfad zu einer Protokolldatei. Sie können ausführen **Wevtutil el** zum Abrufen einer Liste von Namen der Protokolldatei.|
|{Epl \| Exportprotokoll} \<Pfad > \<Exportfile > [/ lf:\<Protokolldatei >] [/ sq:\<Structquery >] [/ f:\<Abfrage >] [/ ow:\<überschreiben >]|Exportiert Ereignisse aus einem Ereignisprotokoll, aus einer Protokolldatei oder über eine strukturierte Abfrage in der angegebenen Datei. Standardmäßig geben Sie einen Protokollnamen für \<Pfad >. Allerdings bei Verwendung der **/LF** klicken Sie dann die option \<Pfad > muss ein Pfad in eine Protokolldatei sein. Bei Verwendung der **/SQ** Option \<Pfad > muss ein Pfad zu einer Datei, die eine strukturierte Abfrage enthält. \<Exportfile > ist ein Pfad zu der Datei an, wo die exportierten Ereignisse gespeichert werden werden.|
|{al \| im Archivierungsprotokoll} \<Logpath > [/ l:\<Gebietsschema >]|Die angegebene Protokolldatei in einem eigenständigen Format wird archiviert. Ein Unterverzeichnis mit dem Namen des Gebietsschemas wird erstellt, und alle gebietsschemaspezifischen Informationen in diesem Unterverzeichnis gespeichert. Nachdem die Verzeichnis- und-Protokolldatei werden erstellt, indem Sie Ausführung **Wevtutil al**, Ereignisse in der Datei, ob der Verleger oder nicht installiert ist gelesen werden können.|
|{cl \| Clear-Log} \<"logName" > [/ bu:\<Sicherung >]|Löscht Ereignisse aus dem angegebenen Ereignisprotokoll. Die **/bu** Option kann verwendet werden, um die gelöschten Ereignisse sichern.|

## <a name="options"></a>Optionen

|       Option       |                                                                                                                                                                                                                                                                 Beschreibung                                                                                                                                                                                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /f:\<Format>    |                                                                                                                                                               Gibt an, dass die Ausgabe entweder XML-oder Textformat sein soll. Wenn \<Format > XML ist, wird die Ausgabe im XML-Format angezeigt. Wenn \<Format > Text ist, wird die Ausgabe ohne die XML-Tags angezeigt. Der Standardwert ist Text.                                                                                                                                                                |
|   e:\<aktiviert >    |                                                                                                                                                                                                                                         Aktiviert oder deaktiviert ein Protokoll. \<Aktiviert > kann "true" oder "false" sein.                                                                                                                                                                                                                                          |
|  / i:\<Isolation >   | Legt fest, den Log-Isolationsmodus. \<Isolation > System, Anwendung oder benutzerdefinierter möglich. Der Isolationsmodus eines Protokolls bestimmt, ob es sich bei ein Protokoll eine Sitzung mit anderen Protokollen in der gleichen Isolation-Klasse verwendet. Wenn Sie Dateisystemisolation angeben, wird das Zielprotokoll freigeben mindestens Schreibberechtigungen mit im Systemprotokoll. Bei Angabe von Anwendungsisolation wird das Zielprotokoll freigeben mindestens Schreibberechtigungen für das Anwendungsprotokoll. Wenn Sie benutzerdefinierte Isolation angeben, müssen Sie auch eine Sicherheitsbeschreibung angeben, mit der **/ca** Option. |
|  /LFN:\<Logpath >   |                                                                                                                                                                                                           Definiert den Protokolldateinamen an. \<LogPath > ist ein vollständiger Pfad zu der Datei, in dem der Ereignisprotokolldienst Ereignisse für dieses Protokoll speichert.                                                                                                                                                                                                           |
|  /RT:\<Aufbewahrung >  |                                                            Legt den Log Retention-Modus. \<Aufbewahrung > kann "true" oder "false" sein. Der Protokollmodus der Aufbewahrung bestimmt das Verhalten der der Ereignisprotokolldienst, wenn eine Protokolldatei die maximale Größe erreicht. Wenn ein Ereignisprotokoll die maximale Größe erreicht, und der Log Retention-Modus "true ist", vorhandene Ereignisse werden beibehalten, und eingehende Ereignisse werden verworfen. Wenn der Log Retention-Modus auf "false" festgelegt ist, überschreiben die eingehende Ereignisse die ältesten Ereignisse im Protokoll.                                                             |
|    /ab:\<automatisch >     |                                                                                                                                   Gibt an, die Richtlinien für automatische Sicherung. \<Automatische > kann "true" oder "false" sein. Wenn dieser Wert auf "true" festgelegt ist, wird das Protokoll automatisch gesichert werden, wenn sie die maximale Größe erreicht. Wenn dieser Wert "true" ist die Aufbewahrung (angegeben mit der **/rt** Option) muss auch festgelegt werden, auf "true".                                                                                                                                    |
|   / ms:\<MaxSize-Wert >   |                                                                                                                                                                        Legt die maximale Größe des Protokolls in Byte. Die minimale Protokollgröße beträgt 1.048.576 Bytes (1024KB) und Protokolldateien sind immer ein Vielfaches von 64KB, sodass der Wert, die Sie eingeben abgerundet wird entsprechend.                                                                                                                                                                         |
|    /l:\<Level>     |                                                                                                                                                                     Definiert die Filter auf Seitenebene des Protokolls an. \<Ebene > kann jeder gültiger Wert für die Ebene sein. Diese Option gilt nur für Protokolle mit einer dedizierten Sitzung zur Verfügung. Sie können einen Filter auf Seitenebene entfernen, indem Sie die Einstellung <Level> auf 0.                                                                                                                                                                      |
|   /k:\<Keywords>   |                                                                                                                                                                                         Gibt den Schlüsselwörtern Filter des Protokolls. \<Schlüsselwörter > kann eine beliebige gültige 64-Bit-Schlüsselwortmaske sein. Diese Option gilt nur für Protokolle mit einer dedizierten Sitzung zur Verfügung.                                                                                                                                                                                         |
|   /CA:\<Kanal >   |                                                                                                                   Legt fest, die Zugriffsberechtigung für ein Ereignisprotokoll. \<Kanal > eine Sicherheitsbeschreibung, die die Security Descriptor Definition Language (SDDL) verwendet wird. Weitere Informationen zu SDDL-Format, finden Sie unter der Microsoft Developers Network (MSDN)-Website ([https://msdn.microsoft.com](https://msdn.microsoft.com)).                                                                                                                    |
|    /c:\<Config>    |                                                                                                                                  Gibt den Pfad zu einer Konfigurationsdatei. Diese Option bewirkt, dass die Protokolleigenschaften aus der Konfigurationsdatei, die in definierten gelesen werden \<Config >. Wenn Sie diese Option verwenden, müssen Sie nicht angeben einer <Logname> Parameter. Der Protokollname wird aus der Konfigurationsdatei gelesen werden.                                                                                                                                   |
|  / ge:\<Metadaten >   |                                                                                                                                                                                                                 Ruft Metadateninformationen für Ereignisse, die von diesem Verleger ausgelöst werden kann. \<Metadaten > kann "true" oder "false" sein.                                                                                                                                                                                                                 |
|   / GM:\<Meldung >   |                                                                                                                                                                                                                       Zeigt die tatsächliche Nachricht statt die numerischen Nachrichten-ID. \<Nachricht > kann "true" oder "false" sein.                                                                                                                                                                                                                        |
|   /lf:\<Logfile>   |                                                                                                                                                                                  Gibt an, dass die Ereignisse aus einem Protokoll oder aus einer Log-Datei gelesen werden soll. \<LogFile > kann "true" oder "false" sein. Bei "true", ist der Parameter für den Befehl den Pfad zu einer Protokolldatei an.                                                                                                                                                                                   |
| /sq:\<Structquery> |                                                                                                                                                                                Gibt an, dass Ereignisse mit der eine strukturierte Abfrage abgerufen werden sollen. \<Structquery > kann "true" oder "false" sein. True gibt an, <Path> ist der Pfad zur Datei, die eine strukturierte Abfrage enthält.                                                                                                                                                                                |
|    /q:\<Query>     |                                                                                                                                                                     Definiert die XPath-Abfrage, um die Ereignisse zu filtern, die gelesen oder exportiert werden. Wenn diese Option nicht angegeben ist, werden alle Ereignisse zurückgegeben oder exportiert werden. Diese Option ist nicht verfügbar, wenn **/SQ** ist "true".                                                                                                                                                                     |
|  /BM:\<Lesezeichen >   |                                                                                                                                                                                                                                 Gibt den Pfad zu einer Datei, die ein Lesezeichen in einer vorherigen Abfrage enthält.                                                                                                                                                                                                                                 |
|   /SBM:\<Savebm >   |                                                                                                                                                                                                             Gibt den Pfad zu einer Datei, die verwendet wird, um ein Lesezeichen dieser Abfrage zu speichern. Die Dateinamenerweiterung sollten .xml verwendet werden.                                                                                                                                                                                                              |
|  / RD:\<Richtung >  |                                                                                                                                                                                                   Gibt die Richtung, in der Ereignisse gelesen werden. \<Richtung > kann "true" oder "false" sein. Bei "true", werden die neuesten Ereignisse zuerst zurückgegeben.                                                                                                                                                                                                   |
|    /l:\<Locale>    |                                                                                                                                                                                          Definiert eine gebietsschemazeichenfolge, die zum Drucken von Text in einem bestimmten Gebietsschema Ereignis verwendet wird. Nur verfügbar, wenn Ereignisse in Text Format mit Drucken der **/f** Option.                                                                                                                                                                                          |
|    / c:\<Anzahl >     |                                                                                                                                                                                                                                                  Legt die maximale Anzahl von Ereignissen zu lesen.                                                                                                                                                                                                                                                  |
|   e:\<Element >    |                                                                                                                                                           Ein Stammelement enthält, wenn Ereignisse im XML-Format angezeigt. \<Element > ist die Zeichenfolge, die Sie in das Stammelement werden sollen. Z. B. **/e:root** würde zu XML-Code, der das Root-Element-Paar enthält \<Stamm ></root>.                                                                                                                                                            |
|  / ow:\<überschreiben >  |                                                                                                                                                                 Gibt an, dass die Exportdatei überschrieben werden soll. \<Overwrite > "true" oder "false" werden können. Wenn "true", und die Exportdatei in angegeben <Exportfile> bereits vorhanden ist, wird Sie ohne Bestätigung überschrieben.                                                                                                                                                                 |
|   /BU:\<Sicherung >    |                                                                                                                                                                                                      Gibt den Pfad zu einer Datei, in denen die gelöschten Ereignisse gespeichert werden. Enthalten Sie die Erweiterung EVTX den Namen der Sicherungsdatei an.                                                                                                                                                                                                       |
|    / r:\<remote >    |                                                                                                                                                                                            Führt den Befehl auf einem Remotecomputer befindet. \<Remote > ist der Name des Remotecomputers. Die **Instant-Messaging** und **um** Parameter unterstützen keine remote-Vorgangs.                                                                                                                                                                                            |
|   / u:\<Benutzername >   |                                                                                                                                                                          Gibt ein anderer Benutzer zum Anmelden bei eines Remotecomputers an. \<Benutzername > ist ein Benutzername im Format "Domäne\Benutzer" oder Benutzer. Diese Option ist nur anwendbar, wenn die **/r** angegeben wird.                                                                                                                                                                          |
|   / p:\<Kennwort >   |                                                                                                                                               Gibt das Kennwort für den Benutzer. Wenn die **/u** Option wird verwendet, und diese Option nicht angegeben oder \<Kennwort > ist " *", die Benutzer aufgefordert, ein Kennwort einzugeben. Diese Option ist nur anwendbar, wenn die \* \*/u* \* angegeben wird.                                                                                                                                                |
|     / a:\<Auth >     |                                                                                                                                                                                             Definiert den Authentifizierungstyp für die Verbindung mit einem Remotecomputer befindet. \<Auth > kann sein, Standardeinstellung, Negotiate, Kerberos oder NTLM. Der Standardwert lautet "aushandeln".                                                                                                                                                                                              |
|  /uni:\<Unicode>   |                                                                                                                                                                                                             Zeigt die Ausgabe im Unicode-Format. \<Unicode > kann "true" oder "false" sein. Wenn <Unicode> ist "true", und klicken Sie dann die Ausgabe in Unicode angegeben ist.                                                                                                                                                                                                             |

## <a name="remarks"></a>Hinweise

-   Verwenden eine Konfigurationsdatei mit dem sl-parameter

    Die Konfigurationsdatei ist eine XML-Datei mit demselben Format wie die Ausgabe des Wevtutil Gl \<"logName" > /f:xml. Das folgende Beispiel zeigt das Format einer Konfigurationsdatei, die Beibehaltungsdauer ermöglicht, können für die automatische Sicherung und legt die maximale Protokollgröße das Protokoll für die Anwendung:  
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

## <a name="BKMK_examples"></a>Beispiele für

Die Namen aller Protokolle aufgeführt:
```
wevtutil el
```
Anzeigen von Konfigurationsinformationen für das Systemprotokoll auf dem lokalen Computer im XML-Format:
```
wevtutil gl System /f:xml
```
Verwenden Sie eine Konfigurationsdatei zum Festlegen von Attributen Ereignisprotokoll (siehe "Hinweise" ein Beispiel einer Konfigurationsdatei):
```
wevtutil sl /c:config.xml
```
Anzeigen von Informationen zu den Microsoft-Windows-Eventlog-Ereignisherausgeber, einschließlich Metadaten, die über die Ereignisse, die vom Verleger ausgelöst werden kann:
```
wevtutil gp Microsoft-Windows-Eventlog /ge:true
```
Installieren Sie Ereignisherausgeber und-Protokolle aus der Manifestdatei "Manifest1.xml":
```
wevtutil im myManifest.xml
```
Deinstallieren Sie Ereignisherausgeber und-Protokolle aus der Manifestdatei "Manifest1.xml":
```
wevtutil um myManifest.xml
```
Zeigen Sie die drei neuesten Ereignisse aus dem Anwendungsprotokoll im Textformat an:
```
wevtutil qe Application /c:3 /rd:true /f:text
```
Der Status des Anwendungsprotokolls angezeigt:
```
wevtutil gli Application 
```
Exportieren Sie Ereignisse aus dem Systemprotokoll in C:\backup\system0506.evtx:
```
wevtutil epl System C:\backup\system0506.evtx
```
Löschen Sie alle Ereignisse aus dem Anwendungsprotokoll nach C:\admin\backups\a10306.evtx speichern möchten:
```
wevtutil cl Application /bu:C:\admin\backups\a10306.evtx
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
