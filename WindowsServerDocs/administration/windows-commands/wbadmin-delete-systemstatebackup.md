---
title: wbadmin delete systemstatebackup
description: Referenz Artikel für den Wbadmin delete systemstatebackup-Befehl, mit dem die von Ihnen angegebenen Systemstatus Sicherungen gelöscht werden.
ms.topic: reference
ms.assetid: 707d37cb-448d-4542-b6ac-1fc89e749788
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 05ce1e2deb8a2466df70b56a43c4532871d491b9
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156076"
---
# <a name="wbadmin-delete-systemstatebackup"></a>wbadmin delete systemstatebackup

Löscht die von Ihnen angegebenen Systemstatus Sicherungen. Wenn das angegebene Volume andere Sicherungen als Systemstatus Sicherungen des lokalen Servers enthält, werden diese Sicherungen nicht gelöscht.

Zum Löschen einer Systemstatus Sicherung mithilfe dieses Befehls müssen Sie Mitglied der Gruppe "Sicherungs- **Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

> [!NOTE]
> Windows Server-Sicherung dient nicht zum Sichern oder Wiederherstellen von registrierungsbenutzer Strukturen (HKEY_CURRENT_USER) im Rahmen der Sicherung oder Wiederherstellung des Systemstatus.

## <a name="syntax"></a>Syntax

```
wbadmin delete systemstatebackup {-keepVersions:<numberofcopies> | -version:<versionidentifier> | -deleteoldest} [-backupTarget:<volumename>] [-machine:<backupmachinename>] [-quiet]
```

> [!IMPORTANT]
> Sie müssen nur einen der folgenden Parameter angeben: **-keepversions**, **-Version**oder **-deleteältesten**.

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -keepversions | Gibt die Anzahl der aktuellen Sicherungen des Systemstatus an, die aufbewahrt werden sollen. Der Wert muss eine positive ganze Zahl sein. Mit dem Parameterwert **-keepversions: 0** werden alle Systemstatus Sicherungen gelöscht. |
| -version | Gibt den Versions Bezeichner der Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, führen Sie den Befehl [Wbadmin Get Versions](wbadmin-get-versions.md) aus.<p>Versionen, die ausschließlich aus Systemstatus Sicherungen bestehen, können mit diesem Befehl gelöscht werden. Führen Sie den Befehl [Wbadmin Get Items](wbadmin-get-items.md) aus, um den Versionstyp anzuzeigen. |
| -deleteälteste | Löscht die älteste Systemstatus Sicherung. |
| -backupTarget | Gibt den Speicherort für die Sicherung an, die Sie löschen möchten. Der Speicherort für Datenträger Sicherungen kann ein Laufwerk Buchstabe, ein Einstellungspunkt oder ein GUID-basierter volumesfad sein. Dieser Wert muss nur für die Suche nach Sicherungen angegeben werden, die sich nicht auf dem lokalen Computer befinden. Informationen zu Sicherungen für den lokalen Computer sind im Sicherungs Katalog auf dem lokalen Computer verfügbar. |
| -Computer | Gibt den Computer an, dessen Systemstatus Sicherung Sie löschen möchten. Nützlich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird. |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die am 31. März 2013 und 10:00 Uhr erstellte Systemstatus Sicherung zu löschen:

```
wbadmin delete systemstatebackup -version:03/31/2013-10:00
```

Geben Sie Folgendes ein, um alle Systemstatus Sicherungen außer den drei neuesten zu löschen:

```
wbadmin delete systemstatebackup -keepVersions:3
```

Geben Sie Folgendes ein, um die älteste auf Laufwerk f: gespeicherte Systemstatus Sicherung zu löschen:

```
wbadmin delete systemstatebackup -backupTarget:f:\ -deleteOldest
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Befehl "WBADMIN GET Versions"](wbadmin-get-versions.md)

- [Befehl "Get Items" in Wbadmin](wbadmin-get-items.md)
