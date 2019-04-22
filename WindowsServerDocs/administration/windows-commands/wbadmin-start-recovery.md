---
title: Wbadmin Start-Wiederherstellung
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52381316-a0fa-459f-b6a6-01e31fb21612
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9f24c9dfeb0ce87474e58d3bd2bce8b68e31cb63
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823281"
---
# <a name="wbadmin-start-recovery"></a>Wbadmin Start-Wiederherstellung



Führt einen Wiederherstellungsvorgang auf Grundlage der Parameter, die Sie angeben.

Um eine Wiederherstellung mit diesem Unterbefehl durchführen, Sie müssen Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie auf **starten**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
wbadmin start recovery
-version:<VersionIdentifier>
-items:{<VolumesToRecover> | <AppsToRecover> | <FilesOrFoldersToRecover>}
-itemtype:{Volume | App | File}
[-backupTarget:{<VolumeHostingBackup> | <NetworkShareHostingBackup>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:{<TargetVolumeForRecovery> | <TargetPathForRecovery>}]
[-recursive]
[-overwrite:{Overwrite | CreateCopy | Skip}]
[-notRestoreAcl]
[-skipBadClusterCheck]
[-noRollForward]
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Version|Gibt an, die Versions-ID der Sicherung zum Wiederherstellen in MM/TT/JJJJ-hh: mm-Format. Wenn Sie die Versions-ID nicht kennen, geben Sie **Wbadmin get Versionen**.|
|-items|Gibt eine durch Trennzeichen getrennte Liste der Volumes, Anwendungen, Dateien oder Ordner wiederherstellen.</br>-If **Itemtype -** ist **Volume**, können Sie nur ein einzelnes Volume angeben, durch die Bereitstellung der Laufwerkbuchstabe des Volumes, Datenträger-Bereitstellungspunkt oder GUID-basierter Volumename.</br>-If **Itemtype -** ist **App**, können Sie nur eine einzelne Anwendung angeben. Um wiederhergestellt werden, muss die Anwendung Windows Server-Sicherung registriert haben. Sie können auch den Wert **ADIFM** zum Wiederherstellen einer Installations von Active Directory. Weitere Informationen finden Sie unter "Hinweise" in.</br>-If **Itemtype -** ist **Datei**, können Sie Dateien oder Ordner angeben, jedoch werden sollten Teil desselben Volume, und unter dem gleichen übergeordneten Ordner werden sollten.|
|-itemtype|Gibt Elemente wiederherstellen. Muss **Volume**, **App**, oder **Datei**.|
|-backupTarget|Gibt den Speicherort, der die Sicherung enthält, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn der Speicherort unterscheidet sich vom, wo die Sicherungen dieses Computers in der Regel gespeichert werden.|
|-Computer|Gibt den Namen des Computers, der die Sicherung wiederhergestellt werden soll. Dieser Parameter ist hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Wird verwendet, wenn die **- BackupTarget** Parameter angegeben ist.|
|-recoveryTarget|Gibt den Speicherort zum Wiederherstellen. Dieser Parameter ist hilfreich, wenn sich dieser Speicherort als den Speicherort unterscheidet, die zuvor gesichert wurde. Sie können auch für Wiederherstellungen von Volumes, Dateien oder Anwendungen verwendet werden. Wenn Sie ein Volume wiederherstellen möchten, können Sie den Laufwerkbuchstaben Volumes, der das alternative Volume angeben. Wenn Sie eine Datei oder einer Anwendung wiederherstellen möchten, können Sie einen alternativen Wiederherstellungsspeicherort angeben.|
|-rekursiv|Nur gültig, wenn Dateien wiederherstellen. Die Dateien in die Ordner und alle Dateien, die die angegebenen Ordner untergeordnet wiederhergestellt. Standardmäßig werden nur Dateien, die direkt in den angegebenen Ordnern befinden, wiederhergestellt.|
|-overwrite|Nur gültig, wenn Dateien wiederherstellen. Gibt die Aktion an, wenn eine Datei, die bereits wiederhergestellt werden, die am gleichen Speicherort vorhanden ist.</br>-   **Skip** bewirkt, dass Windows Server-Sicherung, überspringen Sie die vorhandene Datei, und fahren Sie mit der Wiederherstellung der nächsten Datei fort.</br>-   **CreateCopy** bewirkt, dass Windows Server-Sicherung um eine Kopie der vorhandenen Datei zu erstellen, damit die vorhandene Datei nicht geändert wird.</br>-   **Überschreiben** bewirkt, dass Windows Server-Sicherung zum Überschreiben der vorhandenen Datei mit der Datei aus der Sicherung.|
|-notRestoreAcl|Nur gültig, wenn Dateien wiederherstellen. Gibt die Sicherheit Zugriffssteuerungslisten (ACLs) der Dateien aus der Sicherung wiederhergestellt wird nicht wiederhergestellt werden. Standardmäßig werden die Sicherheits-ACLs wiederhergestellt (der Standardwert ist **"true")**. Wenn dieser Parameter verwendet wird, werden die ACLs für die wiederhergestellten Dateien aus dem Speicherort geerbt werden, zu denen die Dateien wiederhergestellt werden.|
|-skipBadClusterCheck|Nur gültig, wenn für die Wiederherstellung von Volumes. Überspringt das prüfen die Datenträger, die Sie für die fehlerhaften Clusterinformationen zum Wiederherstellen verwenden. Wenn Sie einen anderen Server oder die Hardware wiederherstellen möchten, empfehlen wir, dass Sie diesen Parameter nicht verwenden. Sie können manuell ausführen den Befehl **Chkdsk/b** auf diesen Datenträgern zu einem beliebigen Zeitpunkt auf fehlerhafte Cluster überprüft diese, und klicken Sie dann die Systeminformationen für die Datei entsprechend zu aktualisieren.</br>Wichtig: Bis zur Ausführung von **Chkdsk** wie beschrieben, die fehlerhafte Cluster gemeldet, auf dem wiederhergestellten System möglicherweise nicht ganz genau.|
|-noRollForward|Nur gültig, wenn Anwendungen wiederherstellen. Für die vorherigen Point-in-Time-Wiederherstellung einer Anwendung ermöglicht, wenn die neueste Version aus den Sicherungen ausgewählt ist. Die neueste und vorherige Point-in-Time-Wiederherstellung erfolgt für andere Versionen der Anwendung, die nicht als Standard verwendet wird.|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|

## <a name="remarks"></a>Hinweise

-   Verwenden Sie zum Anzeigen einer Liste von Elementen, die für die Wiederherstellung nach einer bestimmten Sicherung Version verfügbar sind **Wbadmin Elemente abrufen**. Wenn ein Volume einer Bereitstellung oder Laufwerkbuchstaben nicht zum Zeitpunkt der Sicherung hatte, würde dieser Unterbefehl einen GUID-basierten Volumenamen zurück, der für die Wiederherstellung des Datenträgers verwendet werden soll.
-   Wenn die **Itemtype -** ist **App**, können Sie einen Wert von **ADIFM** für **-Element** , führen Sie eine Installation von Medienvorgang zum Wiederherstellen von allen die Verwandte Daten, die für Active Directory Domain Services benötigt werden. **ADIFM** erstellt eine Kopie der Active Directory-Datenbank, die Registrierung und den SYSVOL-Status und speichert dann diese Informationen in der vom angegebenen Position **- RecoveryTarget**. Verwenden Sie diesen Parameter nur, wenn **- RecoveryTarget** angegeben ist.

>     [!NOTE]
>     Before using **wbadmin** to perform an install from media operation, you should consider using the **ntdsutil** command because **ntdsutil** only copies the minimum amount of data needed, and it uses a more secure data transport method.

## <a name="BKMK_Examples"></a>Beispiele für

Geben Sie Folgendes ein, führen Sie eine Wiederherstellung der Sicherung von am 31. März 2013 um 9:00 Uhr, von Volume "d:", erstellt:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume -items:d:
```
Geben Sie zum Ausführen einer Wiederherstellung auf Laufwerk d der Sicherung von am 31. März 2013 um 9:00 Uhr, von der Registrierung erstellt:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```
Geben Sie Folgendes ein, führen Sie eine Wiederherstellung der Sicherung von am 31. März 2013 um 9:00 Uhr, d:\folder und untergeordnet d:\folder, Ordner erstellt:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:File -items:d:\folder -recursive
```
Eine Wiederherstellung der Sicherung von 31. März 2013 ausführen ausgeführt wird, um 9:00 Uhr, des Volumes \\ \\? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\, Typ:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume 
-items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
Zum Ausführen einer Wiederherstellung der Sicherung vom 30. April 2013, zu die um 9:00 Uhr, der den freigegebenen Ordner erstellt \\ \\Servername\share von server01, Typ:
```
wbadmin start recovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Start-WBFileRecovery](https://technet.microsoft.com/library/jj902457.aspx) cmdlet
-   [Start-WBHyperVRecovery](https://technet.microsoft.com/library/jj902463.aspx) cmdlet
-   [Start-WBSystemStateRecovery](https://technet.microsoft.com/library/jj902449.aspx) cmdlet
-   [Start-WBVolumeRecovery](https://technet.microsoft.com/library/jj902470.aspx) cmdlet