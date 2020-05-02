---
title: 'secedit: Importieren'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1dd59d4c-9d48-444a-871b-b957eb682597
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9229bf0cf7483a9476d68984af3ac6c91e3c061
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722050"
---
# <a name="seceditimport"></a>secedit: Importieren



Importiert Sicherheitseinstellungen, die in einer INF-Datei gespeichert sind, die zuvor aus der mit Sicherheits Vorlagen konfigurierten Datenbank exportiert wurde.

## <a name="syntax"></a>Syntax

```
Secedit /import /db <database file name> /cfg <configuration file name> [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und den Dateinamen einer Datenbank an, in der die gespeicherte Konfiguration enthalten ist, in der der Import ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss auch `/cfg \<configuration file name>` die Befehlszeilenoption angegeben werden.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheits Vorlage im/cfg-Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen.</br>Diese Befehlszeilenoption ist nur gültig, wenn der `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage im/cfg-Parameter an die gespeicherte Vorlage angehängt.|
|cfg|Erforderlich.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie `/db \<database file name>` mit dem-Parameter verwendet wird. Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheits Vorlage im/cfg-Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen.</br>Diese Befehlszeilenoption ist nur gültig, wenn der `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage im/cfg-Parameter an die gespeicherte Vorlage angehängt.|
|Felder|Optional.</br>Gibt die Sicherheitsbereiche an, die auf das System angewendet werden sollen. Wenn dieser Parameter nicht angegeben wird, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Zum Konfigurieren mehrerer Bereiche trennen Sie jeden Bereich durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:</br>-SecurityPolicy</br>    Lokale Richtlinie und Domänen Richtlinie für das System, einschließlich Konto Richtlinien, Überwachungs Richtlinien, Sicherheitsoptionen usw.</br>-Group_Mgmt</br>    Eingeschränkte Gruppeneinstellungen für alle Gruppen, die in der Sicherheits Vorlage angegeben sind.</br>-User_Rights</br>    Benutzer Anmelde Rechte und erteilen von Berechtigungen.</br>-REGKEYS</br>    Sicherheit für lokale Registrierungsschlüssel.</br>-File Store</br>    Sicherheit im lokalen Dateispeicher.</br>-Dienste</br>    Sicherheit für alle definierten Dienste.|
|log|Optional.</br>Gibt den Pfad und den Dateinamen der Protokolldatei für den Prozess an.|
|quiet|Optional.</br>Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Bemerkungen

Bevor Sie eine INF-Datei auf einen anderen Computer importieren, führen Sie den Befehl secedit/generaterollback für die Datenbank aus, für die der Import ausgeführt wird, und secedit/Validate für die Import Datei, um deren Integrität zu überprüfen.

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Documents and\*Settings Useraccount<em>\My documents\security\logs\*DatabaseName</em>. log) verwendet.

In Windows Server 2008 `Secedit /refreshpolicy` wurde durch ersetzt. `gpupdate` Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="examples"></a>Beispiele

Exportieren Sie die Sicherheitsdatenbank und die Domänen Sicherheitsrichtlinien in eine INF-Datei, und importieren Sie diese Datei in eine andere Datenbank, um die Sicherheitsrichtlinien Einstellungen auf einem anderen Computer zu replizieren.
```
Secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg NetworkShare\Policies\SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```
Importieren Sie nur den Sicherheitsrichtlinien Teil der Datei in eine andere Datenbank auf einem anderen Computer.
```
Secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg NetworkShare\Policies\SecContoso.inf /areas securitypolicy /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Secedit:export](secedit-export.md)
-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit:validate](secedit-validate.md)
-   [Secedit](secedit.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)