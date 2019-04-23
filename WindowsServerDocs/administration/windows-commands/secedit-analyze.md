---
title: 'Secedit: Analysieren'
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 324da8de153a5487c9d71872cd154928cc24c285
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848821"
---
# <a name="seceditanalyze"></a>Secedit: Analysieren



Können Sie die aktuellen Systemeinstellungen für die grundlegenden Einstellungen zu analysieren, die in einer Datenbank gespeichert sind. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und Dateinamen Namen einer Datenbank, die die gespeicherte Konfiguration enthält, für die Analyse ausgeführt wird.</br>Wenn Dateiname, eine Datenbank, die nicht über eine Sicherheitsvorlage angibt (dargestellt durch die Konfigurationsdatei) zugeordnet, wurde die `/cfg \<configuration file name>` Befehlszeilenoption muss auch angegeben werden.|
|cfg|Dies ist optional.</br>Gibt an, der Pfad und Dateiname für die Sicherheitsvorlage, die in der Datenbank für die Analyse importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit der `/db \<database file name>` Parameter. Wenn dies nicht angegeben wird, erfolgt die Analyse für eine Konfiguration, die bereits in der Datenbank gespeichert.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheitsvorlage, die im Parameter "/ cfg" überschrieben werden sollen, alle oder zusammengesetzte Vorlagen, die in die Datenbank anstatt durch Anfügen der Ergebnisse an die gespeicherte Vorlage gespeichert wird.</br>Diese Befehlszeilenoption ist nur gültig, wenn die `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage in der/cfg-Parameter an die gespeicherte Vorlage angefügt.|
|log|Optional.</br>Gibt an, der Pfad und Dateiname der Protokolldatei des Prozesses verwendet werden.|
|Quiet|Optional.</br>Unterdrückt die Bildschirmausgabe. Sie können dennoch Analyseergebnisse Ansicht mit der Sicherheitskonfiguration und-Analyse-Snap-in auf der Microsoft Management Console (MMC).|

## <a name="remarks"></a>Hinweise

Die Analyseergebnisse werden in einem separaten Bereich der Datenbank gespeichert und können in der Sicherheitskonfiguration und des Analysis-Snap-Ins zur MMC angezeigt werden.

Wenn der Pfad für die Protokolldatei nicht, die Standardprotokolldatei, bereitgestellt wird (*Systemroot*\Documents and Settings\*UserAccount*\My Documents\Security\Logs\*DatabaseName*. Protokoll) wird verwendet.

In Windows Server 2008 `Secedit /refreshpolicy` wurde durch ersetzt `gpupdate`. Informationen zum Aktualisieren von Sicherheitseinstellungen, finden Sie unter [Gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Beispiele für

Führen Sie die Analyse für die Sicherheitsparameter "auf die Sicherheitskonten-Datenbank, SecDbContoso.sdb, Sie mit der Sicherheitskonfiguration und des Analysis-Snap-in erstellt. Leiten Sie die Ausgabe in die Datei, die SecAnalysisContosoFY11 mit aufgefordert wird, sodass Sie den Befehl überprüfen können ordnungsgemäß ausgeführt wurde.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
Nehmen wir an, dass es sich bei die Analyse einige Inadequacies offengelegt, damit die Sicherheitsvorlage SecContoso.inf, geändert wurde. Führen Sie den Befehl erneut aus, um die Änderungen, die Ausgabe an die vorhandene Datei SecAnalysisContosoFY11 mit keine Eingabeaufforderung weitergeleitet.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)