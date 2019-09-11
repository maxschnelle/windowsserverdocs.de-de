---
title: 'secedit: Konfigurieren'
description: 'Windows-Befehle Thema ****- '
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
ms.openlocfilehash: 9844ed9ac1c53d0a3b9f8bb28ab085a20a48509d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868822"
---
# <a name="seceditconfigure"></a>secedit: Konfigurieren



Ermöglicht es Ihnen, die aktuellen Systemeinstellungen mithilfe der in einer Datenbank gespeicherten Sicherheitseinstellungen zu konfigurieren. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /configure /db <database file name> [/cfg <configuration file name>] [/overwrite] [/areas SECURITYPOLICY | GROUP_MGMT | USER_RIGHTS | REGKEYS | FILESTORE | SERVICES] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Utility|Erforderlich.</br>Gibt den Pfad und den Dateinamen einer Datenbank an, in der die gespeicherte Konfiguration enthalten ist.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss auch `/cfg \<configuration file name>` die Befehlszeilenoption angegeben werden.|
|cfg|Optional.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie `/db \<database file name>` mit dem-Parameter verwendet wird. Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheits Vorlage im/cfg-Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen.</br>Diese Befehlszeilenoption ist nur gültig, wenn der `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage im/cfg-Parameter an die gespeicherte Vorlage angehängt.|
|Felder|Optional.</br>Gibt die Sicherheitsbereiche an, die auf das System angewendet werden sollen. Wenn dieser Parameter nicht angegeben wird, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Zum Konfigurieren mehrerer Bereiche trennen Sie jeden Bereich durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:</br>-SecurityPolicy</br>    Lokale Richtlinie und Domänen Richtlinie für das System, einschließlich Konto Richtlinien, Überwachungs Richtlinien, Sicherheitsoptionen usw.</br>- Group_Mgmt</br>    Eingeschränkte Gruppeneinstellungen für alle Gruppen, die in der Sicherheits Vorlage angegeben sind.</br>- User_Rights</br>    Benutzer Anmelde Rechte und erteilen von Berechtigungen.</br>-REGKEYS</br>    Sicherheit für lokale Registrierungsschlüssel.</br>-File Store</br>    Sicherheit im lokalen Dateispeicher.</br>-Dienste</br>    Sicherheit für alle definierten Dienste.|
|angezeigt|Optional.</br>Gibt den Pfad und den Dateinamen der Protokolldatei für den Prozess an.|
|Geschwiegen|Optional.</br>Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Hinweise

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Users \*Useraccount<em>\My\*documents\security\logs DatabaseName</em>. log) verwendet.

Ab Windows Server 2008 `Secedit /refreshpolicy` wurde durch `gpupdate`ersetzt. Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Beispiele

Führen Sie die Analyse für die Sicherheitsparameter in der Sicherheitsdatenbank "secdbtso. sdb" aus, die Sie mit dem Snap-in "Sicherheitskonfiguration und-Analyse" erstellt haben. Leiten Sie die Ausgabe an die Datei weiter SecAnalysisContosoFY11 mit Aufforderung, damit Sie überprüfen können, ob der Befehl korrekt ausgeführt wurde.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
Nehmen wir an, dass die Analyse einige Unzulänglichkeiten offenbarte, damit die Sicherheits Vorlage "secmso. inf" geändert wurde. Führen Sie den Befehl erneut aus, um die Änderungen einzubeziehen, und leiten Sie die Ausgabe an die vorhandene Datei SecAnalysisContosoFY11 ohne Aufforderung.
```
Secedit /configure /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit](secedit.md)
-   [Secedit:analyze](secedit-analyze.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)