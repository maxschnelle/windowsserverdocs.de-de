---
title: secedit:export
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49a8b241-aa8c-45b7-844d-67a29fab708e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 398d2fa47f2418aec910569c2eb85aec408ad482
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441590"
---
# <a name="seceditexport"></a>secedit:export



Exportiert die Sicherheitseinstellungen, die in einer Datenbank mit Sicherheitsvorlagen konfiguriert gespeichert. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und Dateinamen Namen einer Datenbank, die die gespeicherte Konfiguration enthält, für die Analyse ausgeführt wird.</br>Wenn Dateiname, eine Datenbank, die nicht über eine Sicherheitsvorlage angibt (dargestellt durch die Konfigurationsdatei) zugeordnet, wurde die `/cfg \<configuration file name>` Befehlszeilenoption muss auch angegeben werden.|
|mergedpolicy|Optional.</br>Zusammengeführt, und exportiert, Domäne und zu den lokalen Gruppenrichtlinien-Sicherheitseinstellungen.|
|cfg|Erforderlich.</br>Gibt an, der Pfad und Dateiname für die Sicherheitsvorlage, die in der Datenbank für die Analyse importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit der `/db \<database file name>` Parameter. Wenn dies nicht angegeben wird, erfolgt die Analyse für eine Konfiguration, die bereits in der Datenbank gespeichert.|
|Bereiche|Optional.</br>Gibt an, die Sicherheitsbereiche, die auf das System angewendet werden. Wenn dieser Parameter nicht angegeben ist, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Um mehrere Bereiche konfigurieren möchten, trennen Sie diese durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:</br>-SecurityPolicy</br>    Überwachen lokale Richtlinien und Domänenrichtlinien für das System, einschließlich der Kontorichtlinien, Richtlinien, Sicherheitsoptionen und So weiter.</br>-Group_Mgmt</br>    Eingeschränkte Gruppe von Einstellungen für alle Gruppen, die in der Sicherheitsvorlage angegeben.</br>-User_Rights</br>    Benutzerrechte für die Anmeldung und gewähren von Berechtigungen.</br>-   RegKeys</br>    Sicherheit für lokale Registrierungsschlüssel.</br>-Dateispeicher</br>    Sicherheit auf lokalen Speicherplatz.</br>-Dienste</br>    Sicherheit für alle definierten Dienste.|
|log|Dies ist optional.</br>Gibt den Pfad und Dateiname den Namen der Protokolldatei für den Prozess.|
|Quiet|Optional.</br>Unterdrückt die Ausgabe von Bildschirm und Protokolldateien. Sie können dennoch Analyseergebnisse Ansicht mit der Sicherheitskonfiguration und-Analyse-Snap-in auf der Microsoft Management Console (MMC).|

## <a name="remarks"></a>Hinweise

Sie können diesen Befehl verwenden, um Ihre Sicherheitsrichtlinien auf einem lokalen Computer zusätzlich zum Importieren der Einstellungen auf einem anderen Computer zu sichern.

Wenn der Pfad für die Protokolldatei nicht, die Standardprotokolldatei, bereitgestellt wird (*Systemroot*\Documents and Settings\*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>. Protokoll) wird verwendet.

In Windows Server 2008 `Secedit /refreshpolicy` wurde durch ersetzt `gpupdate`. Informationen zum Aktualisieren von Sicherheitseinstellungen, finden Sie unter [Gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Beispiele für

Exportieren Sie die Sicherheitskonten-Datenbank und die Sicherheitsrichtlinien für die Domäne in eine inf-Datei und importieren Sie diese Datei in eine andere Datenbank, um die Sicherheitseinstellungen für die Richtlinie auf einem anderen Computer zu replizieren.
```
Secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```
Importieren Sie diese Datei in eine andere Datenbank auf einem anderen Computer.
```
Secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit:import](secedit-import.md)
-   [Secedit](secedit.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)