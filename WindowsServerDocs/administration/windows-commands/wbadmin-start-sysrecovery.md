---
title: Wbadmin Start sysrecovery
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8232f-7c42-452b-838e-15b0cf6faebe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8e0ff114d09d70b9e50e8c4ea6af6330c74128c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847161"
---
# <a name="wbadmin-start-sysrecovery"></a>Wbadmin Start sysrecovery



Führt eine Systemwiederherstellung (bare-Metal-Recovery), die mit den Parametern, die Sie angeben.

> [!NOTE]
> Dieses Unterbefehl kann nur über die Windows-Wiederherstellungsumgebung ausgeführt werden, und es ist nicht standardmäßig in den Text der Nutzung der aufgeführt **Wbadmin**. Weitere Informationen finden Sie unter [Übersicht über die Windows-Wiederherstellungsumgebung (Windows RE)](https://technet.microsoft.com/library/hh825173.aspx).

Um eine Wiederherstellung des mit diesem Unterbefehl auszuführen, muss Sie Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert.

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin start sysrecovery
-version:<VersionIdentifier>
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-restoreAllVolumes]
[-recreateDisks]
[-excludeDisks]
[-skipBadClusterCheck]
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Version|Gibt an, die Versions-ID für die Sicherung zum Wiederherstellen in MM/TT/JJJJ-hh: mm-Format. Wenn Sie die Versions-ID nicht kennen, geben Sie **Wbadmin get Versionen**.|
|-backupTarget|Gibt den Speicherort, der enthält die Sicherung oder Sicherungen, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn der Speicherort unterscheidet sich von, wo die Sicherungen dieses Computers in der Regel gespeichert werden.|
|-Computer|Gibt den Namen des Computers ein, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn die **- BackupTarget** Parameter angegeben ist.|
|-restoreAllVolumes|Wiederherstellung der ausgewählten Sicherung aller Volumes. Wenn dieser Parameter nicht angegeben ist, werden nur wichtige Volumes (Volumes, die die Status und Betriebssystem Systemkomponenten enthalten) wiederhergestellt. Dieser Parameter ist hilfreich, wenn Sie das System nicht kritischen Volumes wiederherstellen möchten.|
|-recreateDisks|Wird die Konfiguration eines Datenträgers in den Zustand, der bei der Erstellung der Sicherung wiederhergestellt.</br>Warnung: Dieser Parameter löscht alle Daten auf Volumes, Host-Betriebssystem-Komponenten. Es kann auch Daten aus Datenvolumes löschen.|
|-excludeDisks|Nur gültig, wenn mit dem angegebenen die **- RecreateDisks** Parameter und muss als eine durch Trennzeichen getrennte Liste von Datenträger-IDs eingegeben werden (wie in der Ausgabe aufgeführt **Wbadmin get Datenträger**). Ausgeschlossenen Datenträger nicht partitioniert oder formatiert. Mit diesem Parameter können Daten auf Datenträgern zu erhalten, die nicht während des Wiederherstellungsvorgangs geändert werden sollen.|
|-skipBadClusterCheck|Überspringt die Überprüfung der Wiederherstellung Datenträger fehlerhaften Clusters Informationen. Wenn Sie auf einem anderen Server oder Hardware wiederherstellen möchten, empfehlen wir, dass Sie diesen Parameter nicht verwenden. Sie können manuell ausführen **Chkdsk/b** auf Ihren Datenträgern Wiederherstellung zu einem beliebigen Zeitpunkt auf fehlerhafte Cluster überprüft diese, und klicken Sie dann die Systeminformationen für die Datei entsprechend zu aktualisieren.</br>Warnung: Bis zur Ausführung von **Chkdsk** wie beschrieben, die fehlerhafte Cluster gemeldet, auf dem wiederhergestellten System möglicherweise nicht ganz genau.|
|-quiet|Führt den Befehl ohne aufforderungen für dem Benutzer an.|

## <a name="BKMK_examples"></a>Beispiele für

Befinden sich auf Laufwerk "d:", Typ, starten Sie die Wiederherstellung von Informationen aus der Sicherung, die auf dem 31. März 2013 um 9:00 Uhr ausgeführt wurde:
```
wbadmin start sysrecovery -version:03/31/2013-09:00 -backupTarget:d:
```
Starten Sie die Wiederherstellung von Informationen aus der Sicherung, die am 30. April 2013 um 9:00 Uhr ausgeführt wurde, die im freigegebenen Ordner befindet sich \\ \\Servername\shared: "SERVER01" eingeben:
```
wbadmin start sysrecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-WBBareMetalRecovery](https://technet.microsoft.com/library/jj902461.aspx) cmdlet