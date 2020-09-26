---
title: servermanagercmd
description: Referenz Artikel für den ServerManagerCmd-Befehl, mit dem Rollen, Rollen Dienste und Features installiert und entfernt werden.
ms.topic: reference
ms.assetid: 507c4b87-8e13-4872-8b34-0c7508eecbc1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 4a00294b70728a41cc68ae15d35a8c19fd768cf7
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389158"
---
# <a name="servermanagercmd"></a>servermanagercmd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Installiert und entfernt Rollen, Rollen Dienste und Features. Zeigt außerdem die Liste aller verfügbaren Rollen, Rollen Dienste und Features an und zeigt an, welche auf diesem Computer installiert sind.

> [!IMPORTANT]
> Dieser Befehl, ServerManagerCmd, ist veraltet und wird in zukünftigen Versionen von Windows nicht mehr unterstützt. Stattdessen wird empfohlen, dass Sie die Windows PowerShell-Cmdlets verwenden, die für Server-Manager verfügbar sind. Weitere Informationen finden Sie unter [Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](/administration/server-manager/install-or-uninstall-roles-role-services-or-features).

## <a name="syntax"></a>Syntax

```
servermanagercmd -query [[[<drive>:]<path>]<query.xml>] [-logpath [[<drive>:]<path>]<log.txt>]
servermanagercmd -inputpath  [[[<drive>:]<path>]<answer.xml>] [-resultpath <result.xml> [-restart] | -whatif] [-logpath [[<drive>:]<path>]<log.txt>]
servermanagercmd -install <id> [-allSubFeatures] [-resultpath [[<drive>:]<path>]<result.xml> [-restart] | -whatif] [-logpath [[<Drive>:]<path>]<log.txt>]
servermanagercmd -remove <id> [-resultpath <result.xml> [-restart] | -whatif] [-logpath  [[<drive>:]<path>]<log.txt>]
servermanagercmd [-help | -?]
servermanagercmd -version
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -Abfrage `[[[<drive>:]<path>]<query.xml>]` | Hiermit wird eine Liste aller Rollen, Rollen Dienste und Features angezeigt, die installiert und für die Installation auf dem Server verfügbar sind. Sie können auch die Kurzform dieses Parameters ( **-q**) verwenden. Wenn die Abfrageergebnisse in einer XML-Datei gespeichert werden sollen, geben Sie eine XML-Datei an, die ersetzt werden soll `<query.xml>` . |
| -inputPath  `[[[<drive>:]<path>]<answer.xml>]` | Installiert oder entfernt die Rollen, Rollen Dienste und Funktionen, die in einer durch dargestellten XML-Antwortdatei angegeben sind `<answer.xml>` . Sie können auch die Kurzform dieses Parameters ( **-p** ) verwenden. |
| -Installation `<id>` | Installiert die von angegebene Rolle, den Rollen Dienst oder das Feature `<id>` . Bei den bezeichlern wird die Groß-/Kleinschreibung beachtet Mehrere Rollen, Rollen Dienste und Features müssen durch Leerzeichen getrennt werden. Die folgenden optionalen Parameter werden mit dem Parameter **-install** verwendet:<ul><li>**-Einstellung** `<SettingName>=<SettingValue>` : Gibt die erforderlichen Einstellungen für die Installation an.</li><li>**-allSubFeatures** : gibt die Installation aller untergeordneten Dienste und Features zusammen mit der übergeordneten Rolle, dem Rollen Dienst oder der Funktion an, die im Wert benannt ist `<id>` .<p>**HINWEIS**<br>Einige Rollen Container verfügen nicht über einen Befehlszeilen Bezeichner, um die Installation aller Rollen Dienste zuzulassen. Dies ist der Fall, wenn Rollen Dienste nicht in derselben Instanz des Server-Manager Befehls installiert werden können. Beispielsweise kann der Verbunddienst Rollen Dienst von Active Directory-Verbund Diensten und der Verbunddienstproxy-Rollen Dienst nicht mit derselben Server-Manager Befehls Instanz installiert werden.</li><li>**-resultPath** `<result.xml>` -Speichert die Installations Ergebnisse in einer XML-Datei, die durch dargestellt wird `<result.xml>` . Sie können auch die Kurzform dieses Parameters ( **-r**) verwenden.<p>**HINWEIS**<br>ServerManagerCmd kann nicht sowohl mit dem Parameter " **-resultPath** " als auch mit dem angegebenen Parameter " **-WhatIf** " ausgeführt werden.</li><li>**-neu starten** : der Computer wird nach Abschluss der Installation automatisch neu gestartet (wenn die installierten Rollen oder Features neu gestartet werden müssen).</li><li>**-WhatIf** -zeigt alle Vorgänge an, die für den Parameter " **-install** " angegeben sind. Sie können auch die Kurzform des **-WhatIf-** Parameters **-w**verwenden. **ServerManagerCmd** kann nicht sowohl mit dem Parameter " **-resultPath** " als auch mit dem angegebenen Parameter " **-WhatIf** " ausgeführt werden.</li><li>**-logPath** `<[[<drive>:]<path>]<log.txt>>` : Gibt einen Namen und einen Speicherort für die Protokolldatei an, die nicht die Standardeinstellung ist `%windir%\temp\servermanager.log` .</li></ul> |
| -Entfernen `<id>` | Entfernt die von angegebene Rolle, den Rollen Dienst oder das Feature `<id>` . Bei den bezeichlern wird die Groß-/Kleinschreibung beachtet Mehrere Rollen, Rollen Dienste und Features müssen durch Leerzeichen getrennt werden. Die folgenden optionalen Parameter werden mit dem Parameter **-Remove** verwendet:<ul><li>**-resultPath** `<[[<drive>:]<path>]result.xml>` -Speichert Entfernungs Ergebnisse in einer XML-Datei, die durch dargestellt wird `<result.xml>` . Sie können auch die Kurzform dieses Parameters ( **-r**) verwenden.<p>**HINWEIS**<br>ServerManagerCmd kann nicht mit den angegebenen Parametern " **-resultPath** " und " **-WhatIf** " ausgeführt werden.</li><li>**-Restart** : der Computer wird automatisch neu gestartet, wenn der Vorgang beendet ist (wenn der Neustart für die verbleibenden Rollen oder Features erforderlich ist).</li><li>**-WhatIf** -zeigt alle Vorgänge an, die für den Parameter "-Remove" angegeben sind. Sie können auch die Kurzform des-WhatIf-Parameters **-w**verwenden. ServerManagerCmd kann nicht mit den angegebenen Parametern " **-resultPath** " und " **-WhatIf** " ausgeführt werden.</li><li>**-logPath** `<[[<Drive>:]<path>]<log.txt>>` : Gibt einen Namen und einen Speicherort für die Protokolldatei an, die nicht die Standardeinstellung ist `%windir%\temp\servermanager.log` .</li></ul> |
| -version | Zeigt die Server-Manager Versionsnummer an. Sie können auch die Kurzform **-v**verwenden. |
| -help | Zeigt die Hilfe im Eingabe Aufforderungs Fenster an. Sie können auch die Kurzform verwenden: **-?**. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste aller Rollen, Rollen Dienste und Features anzuzeigen, die verfügbar sind und welche Rollen, Rollen Dienste und Features auf dem Computer installiert sind:

```
servermanagercmd -query
```

Geben Sie Folgendes ein, um die Rolle "Webserver (IIS)" zu installieren und die Installations Ergebnisse in einer XML-Datei zu speichern, die durch *installResult.xml*dargestellt wird:

```
servermanagercmd -install Web-Server -resultpath installResult.xml
```

Um ausführliche Informationen zu den Rollen, Rollen Diensten und Features anzuzeigen, die installiert oder entfernt werden, basierend auf den Anweisungen, die in einer durch *install.xml*dargestellten XML-Antwortdatei angegeben sind, geben Sie Folgendes ein:

```
servermanagercmd -inputpath install.xml -whatif
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Übersicht über Server-Manager](/administration/server-manager/server-manager)
