---
title: secedit:generaterollback
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa655d80c2698430827ad814c2b476e526529323
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441553"
---
# <a name="seceditgeneraterollback"></a>secedit:generaterollback



Können Sie eine Rollbackvorlage für eine Vorlage für die angegebene Konfiguration zu generieren. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und Dateinamen Namen einer Datenbank, die die gespeicherte Konfiguration enthält, für die Analyse ausgeführt wird.</br>Wenn Dateiname, eine Datenbank, die nicht über eine Sicherheitsvorlage angibt (dargestellt durch die Konfigurationsdatei) zugeordnet, wurde die `/cfg \<configuration file name>` Befehlszeilenoption muss auch angegeben werden.|
|cfg|Erforderlich.</br>Gibt an, der Pfad und Dateiname für die Sicherheitsvorlage, die in der Datenbank für die Analyse importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit der `/db \<database file name>` Parameter. Wenn dies nicht angegeben wird, erfolgt die Analyse für eine Konfiguration, die bereits in der Datenbank gespeichert.|
|rbk|Erforderlich.</br>Gibt an, eine Sicherheitsvorlage, die in der die Rollbackinformationen geschrieben wird. Sicherheitsvorlagen werden mithilfe des MMC-Snap-Ins Sicherheitsvorlagen erstellt. Rollbackdateien können mit diesem Befehl erstellt werden.|
|log|Optional.</br>Gibt den Pfad und Dateiname den Namen der Protokolldatei für den Prozess.|
|Quiet|Optional.</br>Unterdrückt die Ausgabe von Bildschirm und Protokolldateien. Sie können dennoch Analyseergebnisse Ansicht mit der Sicherheitskonfiguration und-Analyse-Snap-in auf der Microsoft Management Console (MMC).|

## <a name="remarks"></a>Hinweise

Wenn der Pfad für die Protokolldatei nicht, die Standardprotokolldatei, bereitgestellt wird (*Systemroot*\Users \*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>.log) wird verwendet.

Ab Windows Server 2008, `Secedit /refreshpolicy` wurde durch ersetzt `gpupdate`. Informationen zum Aktualisieren von Sicherheitseinstellungen, finden Sie unter [Gpupdate](gpupdate.md).

Die erfolgreiche Ausführung dieses Befehls wird Status "die Aufgabe erfolgreich abgeschlossen wurde." und die Protokolle nur die Konflikte zwischen den angegebenen Sicherheitsvorlage und Konfiguration von Sicherheitsrichtlinien. Diese Konflikte in der scesrv.log aufgeführt.

Wenn eine vorhandenen Rollbackvorlage für das angegeben wird, wird mit diesem Befehl überschrieben. Sie können eine neue Rollbackvorlage für das mit diesem Befehl erstellen. Es sind keine zusätzlichen Parameter für die Bedingung erforderlich.

## <a name="BKMK_Examples"></a>Beispiele für

Erstellen Sie nach dem Erstellen der Sicherheitsvorlage mit der Sicherheitskonfiguration und des Analysis-Snap-in SecTmplContoso.inf, die Rollback-Konfigurationsdatei, um die ursprünglichen Einstellungen zu speichern. Schreiben Sie die Aktion in der Protokolldatei FY11.
```
Secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)