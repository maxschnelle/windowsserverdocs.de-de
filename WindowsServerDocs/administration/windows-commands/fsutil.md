---
ms.assetid: 2e748187-6a10-4bb0-aed5-34f886a250d2
title: Fsutil
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: df8d25b01b67010734deb8dd7e42f3233e6011fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866811"
---
# <a name="fsutil"></a>Fsutil

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Führt Aufgaben aus, die in der Zuordnung (Table, DATEIZUORDNUNGSTABELLE) und NTFS-Dateisystemen wie Verwalten von Analysepunkten Datei verweist Verwalten von Dateien mit geringer Dichte oder Aufheben der Bereitstellung eines Volumes, verknüpft sind. Wenn es ohne Parameter verwendet wird **Fsutil** zeigt eine Liste der unterstützten Unterbefehle. 

> [!Note] 
> Sie müssen als Administrator oder Mitglied der Gruppe "Administratoren" zur Verwendung von Fsutil angemeldet werden. Der Befehl "Fsutil" ist sehr leistungsstark und sollten nur von erfahrenen Benutzern, die über umfassende Kenntnisse in Windows-Betriebssystemen verwendet werden.
>
>Sie müssen die Windows-Subsystem für Linux aktivieren, vor dem Ausführen **Fsutil**. Führen Sie den folgenden Befehl als Administrator in PowerShell, um diese optionale Funktion zu aktivieren:
>
>```
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
>```
> Sie werden aufgefordert, den Computer neu starten, nachdem es installiert ist. Nach dem Neustart des Computers Sie Lage sein, führen Sie **Fsutil** als Administrator.

## <a name="parameters"></a>Parameter

|Unterbefehl |Beschreibung|
|---|---|
|[Fsutil 8dot3name](fsutil-8dot3name.md) | Abfragen oder Änderungen der Einstellungen für Kurznamen-Verhalten des Systems, z. B., generiert der 8.3-Dateinamen Zeichen. Abkürzungen für alle Dateien in einem Verzeichnis entfernt. Scannen ein Verzeichnis und Identifizieren von Registrierungsschlüsseln, die betroffen sein könnten, wenn Sie kurze Namen aus den Dateien im Verzeichnis entfernt wurden.|
|[Fsutil behavior](fsutil-behavior.md) |Volume-Verhalten Abfragen, oder legt ihn fest.|
|[Fsutil geändert](fsutil-dirty.md)| Fragt ab, ob dirty Bit des Volumes festgelegt ist, oder legt diesen dirty Bit des Volumes fest. Wenn ein Volume geändert ist Bit festgelegt ist, **Autochk** automatisch geprüft, ob das Volume für Fehler beim nächsten des Computers Neustart.|
|[Fsutil-Datei](fsutil-file.md)|Sucht nach einer Datei über den Benutzernamen, (wenn Datenträgerkontingente aktiviert sind), fragt zugewiesene Bereiche für eine Datei, legt den kurzen Namen, einer Datei gültige Datenlänge, legt keine Daten für eine Datei fest, erstellt eine neue Datei mit einer angegebenen Größe, sucht nach einer Datei-ID, wenn der Name , oder sucht einen Dateinamen für die Verknüpfung für eine angegebene Datei-ID.|
|[Fsutil fsinfo](fsutil-fsinfo.md)|Listet alle Laufwerke und fragt die Laufwerkstyp, Informationen über Volume, NTFS-Volumeinformationen oder System Dateistatistiken ab.|
|[Fsutil hardlink](fsutil-hardlink.md)|Listet die festen Links für eine Datei oder einen festen Link (einem Verzeichniseintrag für eine Datei) erstellt. Jede Datei kann betrachtet werden, um mindestens einen festen Link zu erhalten. Auf NTFS-Volumes kann jede Datei mehrere feste Links, sein, damit eine einzelne Datei in mehreren Verzeichnissen (oder sogar im gleichen Verzeichnis, mit unterschiedlichen Namen) angezeigt werden können. Da alle Verknüpfungen auf dieselbe Datei verweisen, können Programme öffnen einen der Links, und ändern Sie die Datei. Nur verwendet werden, nachdem alle Links, gelöscht wurden, wird eine Datei aus dem Dateisystem gelöscht. Nachdem Sie einen festen Link erstellt haben, können Programme wie jeden anderen Dateinamen verwenden.|
|[Fsutil-Objekt-ID](fsutil-objectid.md)|Verwaltet die Objektbezeichner, die durch das Windows-Betriebssystem verwendet werden, um Objekte wie Dateien und Verzeichnissen zu verfolgen.|
|[Fsutil quota](fsutil-quota.md)|Verwaltet Datenträgerkontingente auf NTFS-Volumes, um eine genauere Steuerung der Netzwerk-basierten Speicher bereitzustellen. Datenträgerkontingente pro Volume implementiert, und aktivieren beide schwierig und Soft-Storage - Beschränkungen auf pro-Benutzer implementiert werden.|
|[Fsutil repair](fsutil-repair.md)|Abfragen, oder legt die Selbstreparatur Status des Volumes. Selbst heilen NTFS versucht, die Beschädigungen des NTFS-Dateisystem ohne korrigieren **Chkdsk.exe** ausgeführt werden. Enthält, auf dem Datenträger Überprüfung initiiert, und Warten auf Abschluss der Reparatur.|
|[Fsutil reparsepoint](fsutil-reparsepoint.md)|Abfragen oder Löschvorgänge Analysepunkte (NTFS Dateisystemobjekte, die definierbare Attribute mit benutzergesteuerten Daten haben). Reparse Points werden verwendet, um die Funktionalität in der Eingabe/Ausgabe (e/a)-Subsystem zu erweitern. Sie werden für Directory Verknüpfungspunkte und Volumebereitstellungspunkten verwendet. Sie werden auch von Dateisystemfilter-Treiber verwendet, um bestimmte Dateien als Sonderzeichen auf diesen Treiber zu markieren.|
|[Fsutil-Ressource](fsutil-resource.md)|Erstellt einen sekundären Transaktionsressourcen-Manager., beginnt oder beendet einen Transaktionsressourcen-Manager., zeigt die Informationen über eine transaktionale Ressource-Manager an oder ändert sein Verhalten.|
|[Fsutil-sparsedatei](fsutil-sparse.md)|Verwaltet die Dateien mit geringer Dichte. Eine Datei mit geringer Dichte ist eine Datei mit einer oder mehreren Regionen des nicht zugeordneten Daten. Ein Programm, wird diese nicht zugewiesenen Regionen als mit Bytes, die mit dem Wert 0 (null) angezeigt, aber kein Speicherplatz wird verwendet, um diese Nullen darstellen. Alle Daten von Bedeutung sind oder ungleich NULL sind reserviert, während alle nicht lesbare Daten (lange Zeichenfolgen von Daten aus Nullen) ist nicht zugeordnet. Wenn eine Datei mit geringer Dichte gelesen wird, zugeordnete Daten werden zurückgegeben, da gespeichert und nicht zugeordnete Daten werden als Nullen (standardmäßig in Übereinstimmung mit der C2-Sicherheitsspezifikation Anforderung) zurückgegeben. Unterstützung der Datei mit geringer Dichte kann Daten an einer beliebigen Stelle in der Datei aufgehoben werden soll.|
|[Fsutil-tiering](fsutil-tiering.md)|Ermöglicht die Verwaltung von Speicher-Tier-Funktionen, wie das Festlegen und das Deaktivieren der Flags und eine Liste der Ebenen.|
|[Fsutil-Transaktion](fsutil-transaction.md)|Führt einen Commit für eine angegebene Transaktion, eine angegebene Transaktion wird ein Rollback ausgeführt, oder zeigt Informationen über die Transaktion.|
|[Fsutil usn](fsutil-usn.md)|Verwaltet Update Sequence Number (USN) Änderung Erfassung, die enthält alle Änderungen an Dateien auf dem Volume, dauerhaft protokolliert.|
|[Fsutil volume](fsutil-volume.md)|Verwaltet ein Volume. Hebt die Bereitstellung eines Volumes, Abfragen, um festzustellen, wie viel freier Speicherplatz auf einem Datenträger verfügbar ist, oder sucht nach einer Datei, die einen angegebenen Cluster verwendet wird.|
|[Fsutil-wim](fsutil-wim.md)|Stellt Funktionen zur Erkennung und Verwaltung von WIM-gesicherten Dateien bereit.|

## <a name="see-also"></a>Siehe auch
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)