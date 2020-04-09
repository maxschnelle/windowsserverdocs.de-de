---
title: prndrvr
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eebb28ae50f4546ac5ab3d495994c96e293f6928
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837303"
---
# <a name="prndrvr"></a>prndrvr

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwenden Sie den Befehl **prndrvr** zum Hinzufügen, löschen und Auflisten von Druckertreibern.

## <a name="syntax"></a>Syntax
```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] 
[-e <environment>] [-s <ServerName>] [-u <UserName>] [-w <Password>] 
[-h <path>] [-i <inf file>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|-a|Installiert einen Treiber.|
|-d|Löscht einen Treiber.|
|-l|Listet alle Druckertreiber auf, die auf dem durch den **-s-** Parameter angegebenen Server installiert sind. Wenn Sie keinen Server angeben, werden die auf dem lokalen Computer installierten Druckertreiber von Windows aufgelistet.|
|-x|Löscht alle Druckertreiber und zusätzlichen Druckertreiber, die nicht von einem logischen Drucker auf dem Server verwendet werden, der durch den **-s-** Parameter angegeben wird. Wenn Sie keinen Server angeben, der aus der Liste entfernt werden soll, löscht Windows alle nicht verwendeten Druckertreiber auf dem lokalen Computer.|
|-m \<drivermodelname\>|Gibt (nach Name) den Treiber an, den Sie installieren möchten. Treiber werden oft für das Drucker Modell benannt, das Sie unterstützen. Weitere Informationen finden Sie in der Druckerdokumentation.|
|-v {0 &#124; 1 &#124; 2 &#124; 3}|Gibt die Version des Treibers an, den Sie installieren möchten. Informationen dazu, welche Versionen für welche Umgebung verfügbar sind, finden Sie in der Beschreibung des **-e-** Parameters. Wenn Sie keine Version angeben, wird die Version des Treibers für die Version von Windows, die auf dem Computer ausgeführt wird, auf dem Sie den Treiber installieren, installiert.<p>-Version **0** unterstützt Windows 95, Windows 98 und Windows Millennium Edition.<br />-Version **1** unterstützt Windows NT 3,51.<br />-Version **2** unterstützt Windows NT 4,0.<br />-Version **3** unterstützt die Betriebssysteme Windows Vista, Windows XP, Windows 2000 und Windows Server 2003. Beachten Sie, dass dies die einzige Druckertreiber Version ist, die von Windows Vista unterstützt wird.|
|-e \<Umgebung >|Gibt die Umgebung für den Treiber an, den Sie installieren möchten. Wenn Sie keine Umgebung angeben, wird die Umgebung des Computers verwendet, auf dem Sie den Treiber installieren. Folgende Umgebungsparameter werden unterstützt:<p>-   **Windows NT x86**<br />-   **Windows x64**<br />-   **Windows ia64**|
|-s \<Servername >|Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.|
|-u \<Benutzername >-w \<Kennwort ein >|Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert.|
|-h \<Pfad >|Gibt den Pfad zur Treiberdatei an. Wenn Sie keinen Pfad angeben, wird der Pfad zu dem Speicherort verwendet, an dem Windows installiert wurde.|
|-i \<filename. inf->|Gibt den kompletten Pfad und den Dateinamen für den Treiber an, den Sie installieren möchten. Wenn Sie keinen Dateinamen angeben, verwendet das Skript eine der INF-Posteingangs Dateien im INF-Unterverzeichnis des Windows-Verzeichnisses.<p>Wenn der Treiber Pfad nicht angegeben ist, sucht das Skript nach Treiberdateien in der CAB-Datei des Treibers.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
- Der **prndrvr** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\<language>" befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad der prndrvr-Datei, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner.

  Beispiel:
  ```
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr
  ```
- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `computer Name`).
- Die Option-x löscht alle zusätzlichen Druckertreiber (Treiber, die für die Verwendung auf Clients installiert sind, auf denen alternative Versionen von Windows ausgeführt werden), auch wenn der primäre Treiber verwendet wird. Wenn die Faxkomponente installiert ist, werden mit dieser Option auch Faxtreiber gelöscht. Der primäre Faxtreiber wird gelöscht, wenn er nicht verwendet wird (d. h., wenn keine Warteschlange verwendet wird). Wenn der primäre Faxtreiber gelöscht wird, besteht die einzige Möglichkeit zum erneuten Aktivieren von Fax darin, die Faxkomponente erneut zu installieren.
- Wenn Sie ohne Parameter verwendet wird, zeigt **prndrvr** die Befehlszeilen Hilfe für den Befehl **prndrvr** an.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um alle Treiber auf dem \\\printserver1-Server aufzulisten, geben Sie Folgendes ein:
```
cscript Prndrvr -l -s
```

Zum Hinzufügen eines Windows x64-Druckertreibers der Version 3 für das Modell "Laser Drucker Modell 1" mithilfe der c:\temp\laserprinter1.inf-Treiber Informationsdatei für einen Treiber, der im Ordner "c:\temp" gespeichert ist:
```
cscript Prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64 -i c:\temp\Laserprinter1.inf -h c:\temp
```

Zum Löschen eines Windows NT x86-Druckertreibers der Version 3 für das Laser Drucker Modell 1 geben Sie Folgendes ein:
```
cscript Prndrvr -a -m Laser printer model 1 -v 3 -e Windows NT x86 
```

## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Print-Befehlsreferenz](print-command-reference.md)
