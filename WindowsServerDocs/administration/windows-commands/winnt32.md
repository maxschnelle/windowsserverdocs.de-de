---
title: winnt32
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a0a6fb3-ba4e-4ace-8984-7f6d3875560e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28675ac6d5a1f1a7f56a9b72ef11a3e99e4ed130
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851261"
---
# <a name="winnt32"></a>winnt32

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Führt eine Installation von oder ein Upgrade auf ein Produkt in Windows Server 2003. Sie können ausführen **winnt32** an der Eingabeaufforderung auf einem Computer unter Windows 95, Windows 98, Windows Millennium Edition, Windows NT, Windows 2000, Windows XP, oder ein Produkt in der Windows Server 2003. Wenn das Ausführen **winnt32** auf einem Computer unter Windows NT, Version 4.0, müssen Sie zunächst Servicepack 5 oder höher anwenden.
## <a name="syntax"></a>Syntax
```
winnt32 [/checkupgradeonly] [/cmd: <CommandLine>] [/cmdcons] [/copydir:{i386|ia64}\<FolderName>] [/copysource: <FolderName>] [/debug[<Level>]:[ <FileName>]] [/dudisable] [/duprepare: <pathName>] [/dushare: <pathName>] [/emsport:{com1|com2|usebiossettings|off}] [/emsbaudrate: <BaudRate>] [/m: <FolderName>]  [/makelocalsource] [/noreboot] [/s: <Sourcepath>] [/syspart: <DriveLetter>] [/tempdrive: <DriveLetter>] [/udf: <ID>[,<UDB_File>]] [/unattend[<Num>]:[ <AnswerFile>]]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/checkupgradeonly|Überprüft den Computer für die Upgradekompatibilität mit Produkten in Windows Server 2003.<br /><br />Wenn Sie diese Option mit verwenden **/ unattend**, keine Benutzereingabe erforderlich ist.  Andernfalls werden die Ergebnisse auf dem Bildschirm angezeigt, und können Sie sie speichern, unter dem Dateinamen, die, den Sie angeben. Der Standarddateiname ist **upgrade.txt** im Ordner.|
|/cmd|Weist Setup an, einen bestimmten Befehl vor der letzten Phase von Setup auszuführen. Dies tritt nach dem Neustart des Computers, und Setup ist abgeschlossen, nachdem Setup die erforderlichen Informationen gesammelt hat, aber vor.|
|\<CommandLine>|Gibt an, die Befehlszeile vor der abschließenden Phase des Setups ausgeführt werden.|
|/cmdcons|Ein X86-basierten Computern wird mit den Recovery-Konsole als Startoption installiert.  Die Recovery-Konsole ist eine Befehlszeilen-Schnittstelle, die von der Sie Aufgaben wie das Starten und Beenden von Diensten und den Zugriff auf dem lokalen Laufwerk (einschließlich Laufwerke, die mit NTFS formatiert) ausführen können. Können Sie nur die **/cmdcons** option nach Abschluss des Setups.|
|/copydir|erstellt einen zusätzlichen Ordner innerhalb des Ordners, in dem die Dateien des Betriebssystems installiert werden.  beispielsweise für X86 und X64-basierte Computer können, erstellen Sie einen Ordner namens *Private_Treiber* im i386-Quellordner für die Installation und die Dateien im Ordner Treiber. Typ **/copydir:i386\\*** Private_Treiber* des Setups diesen Ordner auf den neu installierten Computer, sodass den neuen Speicherort des Ordners kopiert **Systemroot** \\*Private_Treiber *.<br /><br />-   **i386** gibt i386<br />-   **ia64** gibt ia64<br /><br />Sie können **/copydir** beliebig viele zusätzliche Ordner erstellen.|
|\<Ordnername >|Gibt den Ordner, den Sie zum Speichern von Änderungen für Ihre Website erstellt.|
|/copysource|erstellt einen zusätzlichen temporären Ordner innerhalb des Ordners, in dem die Dateien des Betriebssystems installiert werden. Sie können **/copysource** beliebig viele zusätzliche Ordner erstellen.<br /><br />Im Gegensatz zu den Ordnern **/copydir** erstellt, **/copysource** Ordner werden gelöscht, nachdem Setup abgeschlossen ist.|
|/debug|erstellt ein Debugprotokoll an der angegebenen Ebene, z. B. **/debug4: Debug.log**.  Die Standardprotokolldatei wird **C:\ Systemroot\winnt32.log**, und|
|\<level>|Level-Werten und Beschreibungen<br /><br />-   0: Schwerwiegende Fehler<br />-   1: Fehler<br />-   2: Standardebene. Warnungen<br />-   3: Informationen<br />-4: Ausführliche Informationen zum Debuggen<br /><br />Jede Ebene enthält die darunter liegenden Ebenen an.|
|/dudisable|Verhindert, dass dynamische Update ausgeführt. Ohne dynamische Updates verwendet Setup ausschließlich die ursprünglichen Installationsdateien. Diese Option wird die dynamische Updates deaktiviert, selbst wenn Sie eine Antwortdatei verwenden, und geben Sie Optionen für dynamische Updates in dieser Datei.|
|/duprepare|Bereitet eine Installationsfreigabe, damit sie mit der dynamischen Updatedateien verwendet werden kann, die Sie aus der Windows Update-Website heruntergeladen haben. Diese Freigabe kann dann für die Installation von Windows XP für mehrere Clients verwendet werden.|
|\<pathName>|Gibt die vollständigen Pfadnamen an.|
|/dushare|Eine Freigabe auf dem Sie zuvor heruntergeladen für das dynamische Update (aktualisierte Dateien für die Verwendung mit dem Setup haben) gibt an, von der Windows Update-Website, und klicken Sie auf die Sie zuvor ausgeführt wurde **/duprepare: *** < Pfadname >*. Wenn auf einem Client ausgeführt wird, gibt an, dass es sich bei der Clientinstallation verwendet die aktualisierten Dateien für die Freigabe, die im angegebenen <pathName>.|
|/emsport|Aktiviert oder deaktiviert Emergency Management Services, während des Setups und der Server-Betriebssystem installiert wurde. Klicken Sie mit Emergency Management Services Sie können Remote Verwalten eines Servers in Notfallsituationen, die in der Regel erfordern eine lokale Tastatur, Maus und Monitor, z. B. wenn das Netzwerk nicht verfügbar ist, oder der Server ist nicht ordnungsgemäß funktioniert. Emergency Management Services gelten bestimmte Hardware, und es ist nur für Produkte in Windows Server 2003 verfügbar.<br /><br />-   **COM1** gilt nur für X86-basierten Computer (keine Itanium-Architektur).<br />-   **COM2**gilt nur für X86-basierten Computer (keine Itanium-Architektur).<br />– Default. Verwendet die Einstellung, angegeben in der BIOS-Umleitung Konsole seriellen Port (SPCR) Tabelle oder, in den Itanium-basierten Systemen, über den Gerätepfad der EFI-Konsole. Bei Angabe von **Usebiossettings** und es gibt keine SPCR-Tabelle oder den Gerätepfad der entsprechenden EFI-Konsole, Emergency Management Serices nicht aktiviert.<br />-   **Off** Emergency Management Services deaktiviert. Sie können es später noch Mal aktivieren, durch Ändern der starteinstellungen.|
|/emsbaudrate|für X86-basierten Computer verwenden gibt die Baudrate für Emergency Management Services an. (Die Option gilt nicht für Itanium-basierte Computer.) Muss zusammen mit **/emsport: COM1** oder **/emsport: COM2** (andernfalls **/emsbaudrate** wird ignoriert).|
|\<BaudRate>|Gibt an, der Baudrate von 9.600, 19200 57600 oder 115200. 9600 ist die Standardeinstellung.|
|/m|Gibt an, dass Setup Ersatzdateien von einem anderen Speicherort kopiert.  Weist Setup am alternativen Speicherort zuerst, und wenn die Dateien sind vorhanden, um sie statt der Dateien aus dem Standardspeicherort zu verwenden.|
|/makelocalsource|Weist Setup an, alle Installationsquelldateien auf Ihre lokale Festplatte kopieren.  Verwendung **makelocalsource** bei der Installation von einer cd-Installationsdateien angeben, wenn die-cd nicht später bei der Installation verfügbar ist.|
|/noreboot|Weist Setup an den Computer nicht neu, nachdem der Kopierphase der Dateien von Setup abgeschlossen ist, sodass Sie einen weiteren Befehl ausführen können.|
|/s|Gibt den Quellspeicherort der Dateien für die Installation an. Geben Sie zum Kopieren von Dateien gleichzeitig von mehreren Servern, die **/s:**\<Sourcepath > Option mehrfach (bis zu einem Maximum von 8). Wenn Sie die Option mehrmals eingeben, muss der erste angegebene Server verfügbar sein, oder das Setup schlägt fehl.|
|\<Sourcepath>|Gibt die Pfadnamen für die vollständige Quelle an.|
|/syspart|Gibt an, dass Sie können Setup-Startdateien auf einer Festplatte zu kopieren, die Festplatte als aktiv markieren, und klicken Sie dann den Datenträger in einem anderen Computer installieren, auf einem Computer X86-basierten. Wenn Sie auf diesem Computer starten, wird es mit der nächsten Phase von Setup automatisch gestartet.<br /><br />Sie müssen immer verwenden die **tempdrive** Parameter mit dem **/Syspart** Parameter.<br /><br />Sie können beginnen, **winnt32** mit der **/Syspart** Option auf einem X86-basierten Computer unter Windows NT 4.0, Windows 2000, Windows XP oder eines Produkts in Windows Server 2003. Wenn der Computer mit Windows NT, Version 4.0 ausgeführt wird, ist Servicepack 5 oder höher. Der Computer kann nicht ausgeführt werden, Windows 95, Windows 98 oder Windows Millennium Edition.|
|\<DriveLetter>|Gibt den Laufwerkbuchstaben an.|
|/tempdrive|weist Setup an temporäre Dateien auf der angegebenen Partition zu speichern.<br /><br />für eine neue Installation wird auch das Server-Betriebssystem auf der angegebenen Partition installiert werden.<br /><br />Bei einem Upgrade die **tempdrive** Option wirkt sich auf die Platzierung von temporären Dateien nur; das Betriebssystem wird aktualisiert werden, in der Partition, die auf dem Sie ausgeführt **winnt32**.|
|/udf|Gibt einen Bezeichner (\<ID >), dass Setup verwendet wird, um anzugeben, wie eine Datei Uniqueness Database (UDB) eine Antwortdatei ändert (finden Sie unter den **/ unattend** Option).  Die UDB überschreibt Werte in der Antwortdatei, und die Kennung bestimmt, welche Werte in der UDF-Datei verwendet werden. Z. B. **/udf:RAS_user,Our_company.udb** für die RAS_user-ID in der Datei Our_company.udb angegebenen Einstellungen überschreibt. Wenn kein \<UDB-Datei > angegeben ist, wird Setup fordert den Benutzer auf einen Datenträger einzulegen, enthält die **$Unique$ UDB** Datei.|
|\<ID>|Gibt einen Bezeichner verwendet, um anzugeben, wie eine Datei Uniqueness Database (UDB) eine Antwortdatei ändert.|
|\<UDB_file>|Gibt eine Datei Uniqueness Database (UDB).|
|/unattend|Auf einem Computer X86-basierten aktualisiert frühere Versionen von Windows NT 4.0 Server (mit Service Pack 5 oder höher) oder Windows 2000 im unbeaufsichtigten Installationsmodus. Alle Einstellungen werden aus der vorherigen Installation übernommen, sodass kein Eingreifen des Benutzers während der Installation erforderlich ist.|
|\<num>|Gibt an, dass die Anzahl der Sekunden zwischen dem Zeitpunkt, das setup abgeschlossen ist, kopieren die Dateien und bei dem Neustart des Computers. Sie können \<Num > auf jedem Computer unter Windows 98, Windows Millennium Edition, Windows NT, Windows 2000, Windows XP oder eines Produkts in Windows Server 2003. Wenn der Computer mit Windows NT, Version 4.0 ausgeführt wird, ist Servicepack 5 oder höher.|
|\<AnswerFile>|Stellt dem Installationsprogramm die benutzerdefinierten Spezifikationen|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
Wenn Sie Windows XP auf Clientcomputern bereitstellen, können Sie die Version von winnt32.exe, die mit Windows XP geliefert wird. Eine weitere Möglichkeit zum Bereitstellen von Windows XP ist winnt32.msi, Verwendung der über Windows Installer, eine Komponente des IntelliMirror Technologien. Weitere Informationen zur Clientbereitstellung finden Sie unter Windows Server 2003 Deployment Kit, dies wird im beschrieben [mithilfe der Windows-Bereitstellung und Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).

Auf einem Itanium-basierte Computer **winnt32** aus der Schnittstelle EFI (Extensible Firmware) oder von Windows Server 2003 Enterprise, Windows Server 2003 R2 Enterprise, Windows Server 2003 R2 Datacenter oder Windows Server 2003 ausgeführt werden können Datacenter. Darüber hinaus auf einem Computer mit Itanium-Architektur **/cmdcons** und **/Syspart** nicht verfügbar sind, und Optionen für Updates sind nicht verfügbar.
Weitere Informationen zur Hardwarekompatibilität finden Sie unter [Hardwarekompatibilität](https://technet.microsoft.com/library/cc757927(v=ws.10).aspx).
Ausführlichere Informationen zur Verwendung des dynamischen Updates aus, und Installieren von mehreren Clients finden Sie unter Windows Server 2003 Deployment Kit, das im beschrieben ist [mithilfe der Windows-Bereitstellung und Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).
Informationen zum Ändern der Einstellungen finden Sie in der Windows-Bereitstellung und Resource Kits für Windows Server 2003. Weitere Informationen finden Sie unter [mithilfe der Windows-Bereitstellung und Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).
Mithilfe der **/ unattend** Befehlszeilenoption zum Automatisieren der Installation wird sichergestellt, dass Sie gelesen und die Microsoft-Lizenz Vereinbarung für Windows Server 2003 akzeptiert haben. Bevor Sie diese Befehlszeilenoption verwenden, um im Auftrag einer Organisation als Ihren eigenen Windows Server 2003 zu installieren, müssen Sie bestätigen, dass der Endbenutzer (ob eine Person oder einer einzelnen Entität) empfangen, gelesen und akzeptiert die Nutzungsbedingungen der Microsoft License Die Vereinbarung für dieses Produkt.  OEMs können diesen Schlüssel nicht auf Computern, die an Endbenutzer verkauft werden angeben.

## <a name="additional-references"></a>Weitere Verweise
-   [Befehlszeilensyntax](command-line-syntax-key.md)

