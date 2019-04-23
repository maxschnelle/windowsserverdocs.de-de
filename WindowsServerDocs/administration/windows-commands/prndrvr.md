---
title: prndrvr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13c89b78ba177362cb9bf1d6a1e601eefb4f4ce3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882121"
---
# <a name="prndrvr"></a>prndrvr

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Verwenden der **Prndrvr** Befehl zum Hinzufügen, löschen und Auflisten von Druckertreibern.

## <a name="syntax"></a>Syntax
```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] 
[-e <environment>] [-s <ServerName>] [-u <UserName>] [-w <Password>] 
[-h <path>] [-i <inf file>]
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-a|Wird ein Treiber installiert.|
|-d|Löscht einen Treiber.|
|-l|Listet alle Druckertreiber auf dem vom angegebenen Server installiert die **-s** Parameter. Wenn Sie keinen Server angeben, führt Windows die Druckertreiber auf dem lokalen Computer installiert.|
|-x|Löscht alle Druckertreiber und zusätzliche Druckertreiber nicht in Gebrauch von einem logischen Drucker auf dem Server, die gemäß der **-s** Parameter. Wenn Sie einen Server aus der Liste zu entfernenden nicht angeben, löscht Windows alle nicht verwendeten Treiber auf dem lokalen Computer.|
|-m \<DrivermodelName\>|Gibt an (nach Namen) der Treiber, die, den Sie installieren möchten. Treiber werden häufig für das Modell des Druckers mit dem Namen, die sie unterstützen. Finden Sie auf Drucker, Weitere Informationen.|
|-v {0 &#124; 1 &#124; 2 &#124; 3}|Gibt die Version des Treibers, die Sie installieren möchten. Siehe dazu die Beschreibung der **-e**Parameter für die Versionen für die Umgebung verfügbar sind. Wenn Sie keine Version angeben, wird die Version des Treibers für die Version von Windows auf dem Computer, auf dem Sie den Treiber installieren werden, installiert.<br /><br />– Version **0** Windows 95, Windows 98 und Windows Millennium Edition unterstützt.<br />– Version **1** Windows NT 3.51 unterstützt.<br />– Version **2** Windows NT 4.0 unterstützt.<br />– Version **3** unterstützt Windows Vista, Windows XP, Windows 2000 und die Windows Server 2003-Betriebssysteme. Beachten Sie, dass dies die einzige Printer Driver-Version, die von Windows Vista unterstützt.|
|-e: \<Umgebung >|Gibt die Umgebung für den Treiber, die, den Sie installieren möchten. Wenn Sie eine Umgebung nicht angeben, wird die Umgebung des Computers, auf dem Sie den Treiber installieren, verwendet. Die unterstützten Umgebung-Parameter sind:<br /><br />-   **"Windows NT x86"**<br />-   **"Windows x64"**<br />-   **"Windows IA64"**|
|-s \<ServerName >|Gibt den Namen des Remotecomputers, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie einen Computer nicht angeben, wird der lokale Computer verwendet.|
|-u \<UserName > -w \<Kennwort >|Gibt ein Konto mit Berechtigungen zum Verbinden mit dem Computer, der den Drucker hostet, den Sie verwalten möchten. Alle Mitglieder der lokalen Gruppe Administratoren des Zielcomputers über diese Berechtigungen verfügen, aber die Berechtigungen können auch für andere Benutzer erteilt werden. Wenn Sie ein Konto nicht angeben, müssen Sie über ein Konto mit Berechtigungen für der Befehl funktioniert angemeldet sein.|
|-h \<Pfad >|Gibt den Pfad zur Treiberdatei. Wenn Sie keinen Pfad angeben, wird der Pfad zum Speicherort, auf dem Windows installiert wurde, verwendet.|
|-i \<Dateiname.inf >|Gibt den vollständigen Pfad und Namen für den Treiber, die, den Sie installieren möchten. Wenn Sie keinen Dateinamen angeben, verwendet das Skript eine der Posteingang Drucker INF-Dateien im Unterverzeichnis "inf" des Windows-Verzeichnisses.<br /><br />Wenn der Treiberpfad nicht angegeben wird, sucht das Skript Treiberdateien in der driver.cab-Datei.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **Prndrvr** Befehl ist eine Visual Basic-Skript befindet sich in der %WINdir%\System32\printing_Admin_Scripts\\ <language> Verzeichnis. Um diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben **Cscript** gefolgt von den vollständigen Pfad und die Prndrvr-Datei, oder wechseln in den entsprechenden Ordner.
   
   Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr
    ```
-   Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. `"computer Name"`).
-   Die X - Option löscht alle zusätzliche Druckertreiber (Treiber für die Verwendung auf Clients installiert ausgeführt alternative Versionen von Windows), auch wenn der primäre Grund verwendet wird. Wenn die Faxkomponente installiert ist, wird diese Option auch Faxtreiber gelöscht. Der primäre Faxtreiber wird gelöscht, wenn es nicht (d.h., wenn es keine Warteschlange verwendet wird ist) verwendet wird. Wenn der primäre Faxtreiber gelöscht wird, ist die einzige Möglichkeit, das Fax erneut zu aktivieren, auf die Faxkomponente neu installieren.
-   Ohne Parameter verwendet **Prndrvr** zeigt die Befehlszeilenhilfe für die **Prndrvr** Befehl.

## <a name="BKMK_examples"></a>Beispiele für

Listen Sie alle Treiber für die \\\printServer1-Server, Typ:
```
cscript Prndrvr -l -s
```

So fügen Sie einen Windows X64-Druckertreiber von Version 3 für das Modell "Laserdrucker Modell 1" des Druckers mit dem C:\temp\Laserprinter1.inf Treiber-Informationsdatei für einen Treiber im Ordner C:\temp Typ gespeichert hinzu:
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows x64" -i c:\temp\Laserprinter1.inf -h c:\temp
```

Um einen Windows NT X86-Druckertreiber von Version 3 für "Laserdrucker Modell 1" zu löschen, geben Sie Folgendes ein:
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows NT x86" 
```

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[druckbefehlsreferenz](print-command-reference.md)
