---
title: Wbadmin delete systemstatebackup
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 1f324cba3fcdae8639009395c4df734a2db6b814
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362525"
---
# <a name="wbadmin-delete-systemstatebackup"></a>Wbadmin delete systemstatebackup



Löscht die von Ihnen angegebenen Systemstatus Sicherungen. Wenn das angegebene Volume andere Sicherungen als Systemstatus Sicherungen des lokalen Servers enthält, werden diese Sicherungen nicht gelöscht.

> [!NOTE]
> Windows Server-Sicherung dient nicht zum Sichern oder Wiederherstellen von registrierungsbenutzer Strukturen (HKEY_CURRENT_USER) im Rahmen der Sicherung oder Wiederherstellung des Systemstatus.

Zum Löschen einer Systemstatus Sicherung mit diesem Unterbefehl müssen Sie ein Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

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
> Ein und nur einer dieser Parameter muss angegeben werden: **-keepversions**, **-Version**oder **-deleteältesten**.

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-keepversions|Gibt die Anzahl der aktuellen Sicherungen des Systemstatus an, die aufbewahrt werden sollen. Der Wert muss eine positive ganze Zahl sein. Mit dem Parameterwert **-keepversions: 0** werden alle Systemstatus Sicherungen gelöscht.|
|-Version|Gibt den Versions Bezeichner der Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, geben Sie **Wbadmin Get Versions**ein.</br>Versionen, die ausschließlich Systemstatus Sicherungen sind, können mit diesem Befehl gelöscht werden. Verwenden Sie **Wbadmin Get Items** , um den Versionstyp anzuzeigen.|
|-deleteälteste|Löscht die älteste Systemstatus Sicherung.|
|-backupTarget|Gibt den Speicherort für die Sicherung an, die Sie löschen möchten. Der Speicherort für Sicherungen von Datenträgern kann ein Laufwerk Buchstabe, ein Einstellungspunkt oder ein GUID-basierter volumesfad sein. Dieser Wert muss nur für die Suche nach Sicherungen angegeben werden, die sich nicht auf dem lokalen Computer befinden. Informationen zu Sicherungen für den lokalen Computer werden im Sicherungs Katalog auf dem lokalen Computer verfügbar sein.|
|-Computer|Gibt den Computer an, dessen Systemstatus Sicherung Sie löschen möchten. Nützlich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die am 31. März 2013 und 10:00 Uhr erstellte Systemstatus Sicherung zu löschen:
```
wbadmin delete systemstatebackup -version:03/31/2013-10:00
```
Geben Sie Folgendes ein, um alle Systemstatus Sicherungen außer den drei neuesten zu löschen:
```
wbadmin delete systemstatebackup -keepVersions:3
```
Geben Sie Folgendes ein, um die älteste auf Laufwerk f gespeicherte Systemstatus Sicherung zu löschen:
```
wbadmin delete systemstatebackup -backupTarget:f -deleteOldest
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)