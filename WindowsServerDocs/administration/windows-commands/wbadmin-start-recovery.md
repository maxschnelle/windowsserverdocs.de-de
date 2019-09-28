---
title: Wbadmin-Wiederherstellung starten
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: edb287573dc76619502faf58018f48c464140629
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362349"
---
# <a name="wbadmin-start-recovery"></a>Wbadmin-Wiederherstellung starten



Führt einen Wiederherstellungs Vorgang basierend auf den Parametern aus, die Sie angeben.

Um mit diesem Unterbefehl eine Wiederherstellung durchzuführen, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten auf **Start**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele für die Verwendung dieses Unterbefehls finden Sie unter [Beispiele](#BKMK_Examples).

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
|-Version|Gibt den Versions Bezeichner der wiederherzustellenden Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, geben Sie **Wbadmin Get Versions**ein.|
|-Elemente|Gibt eine durch Trennzeichen getrennte Liste von Volumes, Anwendungen, Dateien oder Ordnern an, die wieder hergestellt werden sollen.</br>Wenn **-ItemType** ein **Volume**ist, können Sie nur ein einzelnes Volume angeben – indem Sie den volumedatenträger, den volumeeinstellungspunkt oder den GUID-basierten Volumenamen angeben.</br>-Wenn **-ItemType** eine **App**ist, können Sie nur eine einzige Anwendung angeben. Damit die Anwendung wieder hergestellt werden kann, muss Sie bei Windows Server-Sicherung registriert sein. Sie können auch den Wert **adifm** verwenden, um eine Installation von Active Directory wiederherzustellen. Weitere Informationen finden Sie in den Hinweisen unter.</br>Wenn **-ItemType** auf **File**festgelegt ist, können Sie Dateien oder Ordner angeben, aber Sie sollten Teil desselben Volumes sein, und Sie sollten sich im selben übergeordneten Ordner befinden.|
|-ItemType|Gibt den Typ der wiederherzustellenden Elemente an. Muss ein **Volume**, eine **App**oder eine **Datei**sein.|
|-backupTarget|Gibt den Speicherort an, der die Sicherung enthält, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn sich der Standort von dem Speicherort unterscheidet, in dem die Sicherungen dieses Computers normalerweise gespeichert werden.|
|-Computer|Gibt den Namen des Computers an, für den Sie die Sicherung wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sie sollte verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird.|
|-wiederherstellungziel|Gibt den Speicherort für die Wiederherstellung an. Dieser Parameter ist hilfreich, wenn sich dieser Speicherort von dem Speicherort unterscheidet, der zuvor gesichert wurde. Sie kann auch für die Wiederherstellung von Volumes, Dateien oder Anwendungen verwendet werden. Wenn Sie ein Volume wiederherstellen, können Sie den volumelaufwerks Buchstaben des alternativen Volumes angeben. Wenn Sie eine Datei oder Anwendung wiederherstellen, können Sie einen alternativen Wiederherstellungs Speicherort angeben.|
|-rekursiv|Nur beim Wiederherstellen von Dateien gültig. Stellt die Dateien in den Ordnern und alle Dateien wieder her, die den angegebenen Ordnern untergeordnet sind. Standardmäßig werden nur Dateien, die sich direkt in den angegebenen Ordnern befinden, wieder hergestellt.|
|-Überschreiben|Nur beim Wiederherstellen von Dateien gültig. Gibt die Aktion an, die ausgeführt werden soll, wenn eine wieder herzustellende Datei bereits am gleichen Speicherort vorhanden ist.</br>-   **Skip** bewirkt, dass Windows Server-Sicherung die vorhandene Datei auslassen und die Wiederherstellung der nächsten Datei fortsetzen.</br>der @no__t-**0-** Vorgang bewirkt, dass Windows Server-Sicherung eine Kopie der vorhandenen Datei erstellt, sodass die vorhandene Datei nicht geändert wird.</br>-   -über**Schreiben** bewirkt, dass Windows Server-Sicherung die vorhandene Datei mit der Datei aus der Sicherung überschreibt.|
|-notrestoreacl|Nur beim Wiederherstellen von Dateien gültig. Gibt an, dass die Sicherheits-Zugriffs Steuerungs Listen (ACLs) der Dateien, die aus der Sicherung wieder hergestellt werden, nicht wieder hergestellt werden. Standardmäßig werden die Sicherheits-ACLs wieder hergestellt (der Standardwert ist **true)** . Wenn dieser Parameter verwendet wird, werden die ACLs für die wiederhergestellten Dateien von dem Speicherort geerbt, an dem die Dateien wieder hergestellt werden.|
|-skipbadclustercheck|Nur beim Wiederherstellen von Volumes gültig. Überspringt die Überprüfung der wiederherzustellenden Datenträger auf fehlerhafte Cluster Informationen. Wenn Sie auf einem anderen Server oder einer anderen Hardware wiederherstellen, wird empfohlen, diesen Parameter nicht zu verwenden. Sie können den Befehl **chkdsk/b** auf diesen Datenträgern jederzeit manuell ausführen, um Sie auf fehlerhafte Cluster zu überprüfen, und dann die Dateisystem Informationen entsprechend aktualisieren.</br>Wichtig: Bis Sie **chkdsk** wie beschrieben ausführen, sind die in Ihrem wiederhergestellten System gemeldeten fehlerhaften Cluster möglicherweise nicht korrekt.|
|-norollforward|Nur beim Wiederherstellen von Anwendungen gültig. Ermöglicht die vorherige Wiederherstellung einer Anwendung zu einem bestimmten Zeitpunkt, wenn die neueste Version aus den Sicherungen ausgewählt ist. Bei anderen Versionen der Anwendung, bei denen es sich nicht um die neuesten handelt, wird die vorherige Zeit Punkt Wiederherstellung als Standardeinstellung ausgeführt.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="remarks"></a>Hinweise

-   Verwenden Sie zum Anzeigen einer Liste von Elementen, die von einer bestimmten Sicherungs Version für die Wiederherstellung verfügbar sind, **Wbadmin Get Items**. Wenn ein Volume zum Zeitpunkt der Sicherung keinen Einfügepunkt oder Laufwerk Buchstabe enthielt, gibt dieser Unterbefehl einen GUID-basierten Volumenamen zurück, der für die Wiederherstellung des Volumes verwendet werden soll.
-   Wenn " **-ItemType** " eine **App**ist, können Sie den Wert " **adifm** for **-Item** " verwenden, um eine Installation von einem Medien Vorgang auszuführen, um alle zugehörigen Daten wiederherzustellen, die für die Active Directory Domain Services benötigt werden. **Adifm** erstellt eine Kopie der Active Directory Datenbank-, Registrierungs-und SYSVOL-Status und speichert diese Informationen dann an dem Speicherort, der von **-Wiederherstellungsziel**angegeben wird. Verwenden Sie diesen Parameter nur, wenn " **-herstellytarget** " angegeben wird.

>     [!NOTE]
>     Before using **wbadmin** to perform an install from media operation, you should consider using the **ntdsutil** command because **ntdsutil** only copies the minimum amount of data needed, and it uses a more secure data transport method.

## <a name="BKMK_Examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Wiederherstellung der Sicherung ab dem 31. März 2013 (um 9:00 Uhr) von Volume d: durchzuführen:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume -items:d:
```
Geben Sie Folgendes ein, um eine Wiederherstellung auf Laufwerk d der Sicherung ab dem 31. März 2013 (9:00 Uhr) der Registrierung auszuführen:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```
Geben Sie Folgendes ein, um eine Wiederherstellung der Sicherung vom 31. März 2013 (um 9:00 Uhr) der Ordner "d:\folder" und der untergeordneten Ordner "d:\folder" durchzuführen:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:File -items:d:\folder -recursive
```
Zum Ausführen einer Wiederherstellung der Sicherung ab dem 31. März 2013 (um 9:00 Uhr) des Volumes \\ @ no__t-1? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963} \,-Typ:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume 
-items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
Zum Ausführen einer Wiederherstellung der Sicherung ab dem 30. April 2013 (um 9:00 Uhr) des freigegebenen Ordners \\ @ no__t-1servername\share von Server01 geben Sie Folgendes ein:
```
wbadmin start recovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Start-wbfilerecovery](https://technet.microsoft.com/library/jj902457.aspx) -Cmdlet
-   [Start-wbhypervrecovery](https://technet.microsoft.com/library/jj902463.aspx) -Cmdlet
-   [Start-wbsystemstatus](https://technet.microsoft.com/library/jj902449.aspx) -Cmdlet
-   [Start-wbvolumerecovery](https://technet.microsoft.com/library/jj902470.aspx) -Cmdlet