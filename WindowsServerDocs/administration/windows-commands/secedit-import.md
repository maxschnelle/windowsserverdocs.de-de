---
title: Secedit:Import
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1dd59d4c-9d48-444a-871b-b957eb682597
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f24cf173d1bacd70d92b325bfe7b342d0589a490
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874281"
---
# <a name="seceditimport"></a>Secedit:Import



Importiert die Sicherheitseinstellungen, die in einer inf-Datei zuvor aus der Datenbank mit Sicherheitsvorlagen konfiguriert exportiert gespeichert. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /import /db <database file name> /cfg <configuration file name> [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]

```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und Dateinamen Namen einer Datenbank, die die gespeicherte Konfiguration enthält, in der der Import ausgeführt wird.</br>Wenn Dateiname, eine Datenbank, die nicht über eine Sicherheitsvorlage angibt (dargestellt durch die Konfigurationsdatei) zugeordnet, wurde die `/cfg \<configuration file name>` Befehlszeilenoption muss auch angegeben werden.|
|overwrite|Dies ist optional.</br>Gibt an, ob die Sicherheitsvorlage, die im Parameter "/ cfg" überschrieben werden sollen, alle oder zusammengesetzte Vorlagen, die in die Datenbank anstatt durch Anfügen der Ergebnisse an die gespeicherte Vorlage gespeichert wird.</br>Diese Befehlszeilenoption ist nur gültig, wenn die `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage in der/cfg-Parameter an die gespeicherte Vorlage angefügt.|
|cfg|Erforderlich.</br>Gibt an, der Pfad und Dateiname für die Sicherheitsvorlage, die in der Datenbank für die Analyse importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit der `/db \<database file name>` Parameter. Wenn dies nicht angegeben wird, erfolgt die Analyse für eine Konfiguration, die bereits in der Datenbank gespeichert.|
|overwrite|Optional.</br>Gibt an, ob die Sicherheitsvorlage, die im Parameter "/ cfg" überschrieben werden sollen, alle oder zusammengesetzte Vorlagen, die in die Datenbank anstatt durch Anfügen der Ergebnisse an die gespeicherte Vorlage gespeichert wird.</br>Diese Befehlszeilenoption ist nur gültig, wenn die `/cfg \<configuration file name>` -Parameter ebenfalls verwendet wird. Wenn dies nicht angegeben ist, wird die Vorlage in der/cfg-Parameter an die gespeicherte Vorlage angefügt.|
|Bereiche|Optional.</br>Gibt an, die Sicherheitsbereiche, die auf das System angewendet werden. Wenn dieser Parameter nicht angegeben ist, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Um mehrere Bereiche konfigurieren möchten, trennen Sie diese durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:</br>-SecurityPolicy</br>    Überwachen lokale Richtlinien und Domänenrichtlinien für das System, einschließlich der Kontorichtlinien, Richtlinien, Sicherheitsoptionen und So weiter.</br>-Group_Mgmt</br>    Eingeschränkte Gruppe von Einstellungen für alle Gruppen, die in der Sicherheitsvorlage angegeben.</br>-User_Rights</br>    Benutzerrechte für die Anmeldung und gewähren von Berechtigungen.</br>-   RegKeys</br>    Sicherheit für lokale Registrierungsschlüssel.</br>-Dateispeicher</br>    Sicherheit auf lokalen Speicherplatz.</br>-Dienste</br>    Sicherheit für alle definierten Dienste.|
|log|Dies ist optional.</br>Gibt den Pfad und Dateiname den Namen der Protokolldatei für den Prozess.|
|Quiet|Optional.</br>Unterdrückt die Ausgabe von Bildschirm und Protokolldateien. Sie können dennoch Analyseergebnisse Ansicht mit der Sicherheitskonfiguration und-Analyse-Snap-in auf der Microsoft Management Console (MMC).|

## <a name="remarks"></a>Hinweise

Führen Sie den Befehl Secedit /generaterollback für die Datenbank vor dem Importieren einer INF-Datei auf einem anderen Computer, auf dem der Import ausgeführt wird und Secedit / in der Importdatei, überprüfen die Integrität zu überprüfen.

Wenn der Pfad für die Protokolldatei nicht, die Standardprotokolldatei, bereitgestellt wird (*Systemroot*\Documents and Settings\*UserAccount*\My Documents\Security\Logs\*DatabaseName*. Protokoll) wird verwendet.

In Windows Server 2008 `Secedit /refreshpolicy` wurde durch ersetzt `gpupdate`. Informationen zum Aktualisieren von Sicherheitseinstellungen, finden Sie unter [Gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Beispiele für

Exportieren Sie die Sicherheitskonten-Datenbank und die Sicherheitsrichtlinien für die Domäne in eine inf-Datei und importieren Sie diese Datei in eine andere Datenbank, um die Sicherheitseinstellungen für die Richtlinie auf einem anderen Computer zu replizieren.
```
Secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg NetworkShare\Policies\SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```
Importieren Sie den Security-Richtlinien Teil der Datei mit einer anderen Datenbank auf einem anderen Computer.
```
Secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg NetworkShare\Policies\SecContoso.inf /areas securitypolicy /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit:export](secedit-export.md)
-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit:validate](secedit-validate.md)
-   [Secedit](secedit.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)