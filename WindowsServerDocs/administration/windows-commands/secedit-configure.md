---
title: secedit:configure
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a92e68ca-003c-4219-8655-0e7734f5fab3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9420945dca9b72de1937258201e7072d2bb115b2
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441526"
---
# <a name="seceditconfigure"></a>secedit:configure



Können Sie so konfigurieren Sie die aktuellen Systemeinstellungen, die mithilfe der Sicherheitseinstellungen, die in einer Datenbank gespeichert. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /configure /db <database file name> [/cfg <configuration file name>] [/overwrite] [/areas SECURITYPOLICY | GROUP_MGMT | USER_RIGHTS | REGKEYS | FILESTORE | SERVICES] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und Dateinamen Namen einer Datenbank, die die gespeicherte Konfiguration enthält.</br>Wenn Dateiname, eine Datenbank, die nicht über eine Sicherheitsvorlage angibt (dargestellt durch die Konfigurationsdatei) zugeordnet, wurde die `/cfg \<configuration file name>` Befehlszeilenoption muss auch angegeben werden.|
|cfg|Dies ist optional.</br>Gibt an, der Pfad und Dateiname für die Sicherheitsvorlage, die in der Datenbank für die Analyse importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit der `/db \<database file name>` Parameter. Wenn dies nicht angegeben wird, erfolgt die Analyse für eine Konfiguration, die bereits in der Datenbank gespeichert.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheitsvorlage, die im Parameter "/ cfg" überschrieben werden sollen, alle oder zusammengesetzte Vorlagen, die in die Datenbank anstatt durch Anfügen der Ergebnisse an die gespeicherte Vorlage gespeichert wird.</br>Diese Befehlszeilenoption ist nur gültig, wenn die `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage in der/cfg-Parameter an die gespeicherte Vorlage angefügt.|
|Bereiche|Optional.</br>Gibt an, die Sicherheitsbereiche, die auf das System angewendet werden. Wenn dieser Parameter nicht angegeben ist, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Um mehrere Bereiche konfigurieren möchten, trennen Sie diese durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:</br>-SecurityPolicy</br>    Überwachen lokale Richtlinien und Domänenrichtlinien für das System, einschließlich der Kontorichtlinien, Richtlinien, Sicherheitsoptionen und So weiter.</br>-Group_Mgmt</br>    Eingeschränkte Gruppe von Einstellungen für alle Gruppen, die in der Sicherheitsvorlage angegeben.</br>-User_Rights</br>    Benutzerrechte für die Anmeldung und gewähren von Berechtigungen.</br>-   RegKeys</br>    Sicherheit für lokale Registrierungsschlüssel.</br>-Dateispeicher</br>    Sicherheit auf lokalen Speicherplatz.</br>-Dienste</br>    Sicherheit für alle definierten Dienste.|
|log|Optional.</br>Gibt den Pfad und Dateiname den Namen der Protokolldatei für den Prozess.|
|Quiet|Optional.</br>Unterdrückt die Ausgabe von Bildschirm und Protokolldateien. Sie können dennoch Analyseergebnisse Ansicht mit der Sicherheitskonfiguration und-Analyse-Snap-in auf der Microsoft Management Console (MMC).|

## <a name="remarks"></a>Hinweise

Wenn der Pfad für die Protokolldatei nicht, die Standardprotokolldatei, bereitgestellt wird (*Systemroot*\Users \*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>.log) wird verwendet.

Ab Windows Server 2008, `Secedit /refreshpolicy` wurde durch ersetzt `gpupdate`. Informationen zum Aktualisieren von Sicherheitseinstellungen, finden Sie unter [Gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Beispiele für

Führen Sie die Analyse für die Sicherheitsparameter "auf die Sicherheitskonten-Datenbank, SecDbContoso.sdb, Sie mit der Sicherheitskonfiguration und des Analysis-Snap-in erstellt. Leiten Sie die Ausgabe in die Datei, die SecAnalysisContosoFY11 mit aufgefordert wird, sodass Sie den Befehl überprüfen können ordnungsgemäß ausgeführt wurde.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
Nehmen wir an, dass es sich bei die Analyse einige Inadequacies offengelegt, damit die Sicherheitsvorlage SecContoso.inf, geändert wurde. Führen Sie den Befehl erneut aus, um die Änderungen, die Ausgabe an die vorhandene Datei SecAnalysisContosoFY11 mit keine Eingabeaufforderung weitergeleitet.
```
Secedit /configure /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
-   [Secedit:analyze](secedit-analyze.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)