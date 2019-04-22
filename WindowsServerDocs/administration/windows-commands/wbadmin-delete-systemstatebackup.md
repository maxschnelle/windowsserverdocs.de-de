---
title: Wbadmin Delete systemstatebackup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 707d37cb-448d-4542-b6ac-1fc89e749788
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6801ca5985af626ccb7f6170fbcd6f8fc8305ba1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813151"
---
# <a name="wbadmin-delete-systemstatebackup"></a>Wbadmin Delete systemstatebackup



Löscht die systemstatussicherungen, die Sie angeben. Wenn das angegebene Volume Sicherungen als systemstatussicherungen Ihres lokalen Servers enthält, werden diese Sicherungen nicht gelöscht werden.

> [!NOTE]
> Windows Server-Sicherung nicht sichern oder Benutzer Registrierungsstrukturen (HKEY_CURRENT_USER) als Teil des Systemstatus-Sicherung oder Wiederherstellung des Systemstatus wiederherstellen.

Um eine Sicherung des Systemstatus mit diesem Unterbefehl zu löschen, Sie müssen Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin delete systemstatebackup
{-keepVersions:<NumberofCopies> | -version:<VersionIdentifier> | -deleteOldest}
[-backupTarget:<VolumeName>]
[-machine:<BackupMachineName>]
[-quiet]
```

> [!IMPORTANT]
> Nur einer dieser Parameter müssen angegeben werden: **- KeepVersions**, **-Version**, oder **- DeleteOldest**.

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-keepVersions|Gibt die Anzahl von der aktuellen Sicherungen des Systemstatus, zu halten. Der Wert muss eine positive ganze Zahl sein. Der Wert des Parameters **- KeepVersions: 0** löscht alle systemstatussicherungen.|
|-Version|Gibt die Versions-ID der Sicherung in MM/TT/JJJJ-hh: mm-Format. Wenn Sie die Versions-ID nicht kennen, geben Sie **Wbadmin get Versionen**.</br>Versionen, die ausschließlich systemstatussicherungen sind, können mit diesem Befehl gelöscht werden. Verwendung **Wbadmin Elemente abrufen** an den Versionstyp.|
|-deleteOldest|Löscht die älteste systemstatussicherung.|
|-backupTarget|Gibt den Speicherort für die Sicherung, die Sie löschen möchten. Der Speicherort für Sicherungen von Datenträgern kann es sich um einen Laufwerkbuchstaben, einen Bereitstellungspunkt oder einen GUID-basierte Volume-Pfad sein. Dieser Wert muss nur angegeben werden, für die Suche nach Sicherungen, die nicht von dem lokalen Computer vorhanden sind. Informationen zu Sicherungen für den lokalen Computer wird im Sicherungskatalog auf dem lokalen Computer verfügbar sein.|
|-Computer|Gibt den Computer, dessen systemstatussicherung, die Sie löschen möchten. Hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn die **- BackupTarget** Parameter angegeben ist.|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|

## <a name="BKMK_examples"></a>Beispiele für

Zum Löschen der systemstatussicherung, die am 31. März 2013 um 10:00 Uhr erstellt haben, geben Sie Folgendes ein:
```
wbadmin delete systemstatebackup -version:03/31/2013-10:00
```
Geben Sie Folgendes ein, um alle Sicherungen des Systemstatus, mit Ausnahme der letzten drei zu löschen:
```
wbadmin delete systemstatebackup -keepVersions:3
```
Geben Sie zum Löschen der ältesten Sicherung des Systemstatus auf Datenträger f gespeichert:
```
wbadmin delete systemstatebackup -backupTarget:f -deleteOldest
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)