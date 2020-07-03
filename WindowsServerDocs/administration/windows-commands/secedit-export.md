---
title: 'secedit: Export'
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 49a8b241-aa8c-45b7-844d-67a29fab708e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d2093b813a6aca5b03bf94c6f0943bc9ffa00346
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924160"
---
# <a name="seceditexport"></a>secedit: Export



Exportiert Sicherheitseinstellungen, die in einer Datenbank gespeichert sind, die mit Sicherheits Vorlagen konfiguriert wurde.

## <a name="syntax"></a>Syntax

```
Secedit /export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|db|Erforderlich.</br>Gibt den Pfad und den Dateinamen einer Datenbank an, die die gespeicherte Konfiguration enthält, für die die Analyse ausgeführt wird.</br>Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, `/cfg \<configuration file name>` muss auch die Befehlszeilenoption angegeben werden.|
|mergedpolicy|Dies ist optional.</br>Führt die Sicherheitseinstellungen für die Domäne und die lokale Richtlinie zusammen.|
|cfg|Erforderlich.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden.</br>Diese/cfg-Option ist nur gültig, wenn Sie mit dem-Parameter verwendet wird `/db \<database file name>` . Wenn dies nicht angegeben ist, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist.|
|Felder|Dies ist optional.</br>Gibt die Sicherheitsbereiche an, die auf das System angewendet werden sollen. Wenn dieser Parameter nicht angegeben wird, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Zum Konfigurieren mehrerer Bereiche trennen Sie jeden Bereich durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:</br>-SecurityPolicy</br>    Lokale Richtlinie und Domänen Richtlinie für das System, einschließlich Konto Richtlinien, Überwachungs Richtlinien, Sicherheitsoptionen usw.</br>-Group_Mgmt</br>    Eingeschränkte Gruppeneinstellungen für alle Gruppen, die in der Sicherheits Vorlage angegeben sind.</br>-User_Rights</br>    Benutzer Anmelde Rechte und erteilen von Berechtigungen.</br>-REGKEYS</br>    Sicherheit für lokale Registrierungsschlüssel.</br>-File Store</br>    Sicherheit im lokalen Dateispeicher.</br>-Dienste</br>    Sicherheit für alle definierten Dienste.|
|log|Dies ist optional.</br>Gibt den Pfad und den Dateinamen der Protokolldatei für den Prozess an.|
|quiet|Dies ist optional.</br>Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden.|

## <a name="remarks"></a>Hinweise

Sie können diesen Befehl verwenden, um Ihre Sicherheitsrichtlinien auf einem lokalen Computer zu sichern, zusätzlich zum Importieren der Einstellungen auf einen anderen Computer.

Wenn der Pfad für die Protokolldatei nicht bereitgestellt wird, wird die Standardprotokoll Datei (*systemroot*\Documents and Settings \* Useraccount<em>\My documents\security\logs \* DatabaseName</em>. log) verwendet.

In Windows Server 2008 wurde durch `Secedit /refreshpolicy` ersetzt `gpupdate` . Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="examples"></a>Beispiele

Exportieren Sie die Sicherheitsdatenbank und die Domänen Sicherheitsrichtlinien in eine INF-Datei, und importieren Sie diese Datei in eine andere Datenbank, um die Sicherheitsrichtlinien Einstellungen auf einem anderen Computer zu replizieren.
```
Secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```
Importieren Sie diese Datei in eine andere Datenbank auf einem anderen Computer.
```
Secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

## <a name="additional-references"></a>Weitere Verweise

-   [Secedit:import](secedit-import.md)
-   [Secedit](secedit.md)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)