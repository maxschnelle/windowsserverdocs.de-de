---
title: servermanagercmd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 507c4b87-8e13-4872-8b34-0c7508eecbc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: ba0b85814d942323b12e1874b852fcf28b8ac068
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883241"
---
# <a name="servermanagercmd"></a>servermanagercmd

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

> [!IMPORTANT]
> Dieser Befehl ist nur auf Servern unter Windows Server 2008 oder Windows Server 2008 R2 verfügbar. **ServerManagerCmd.exe** wurde als veraltet markiert und ist in Windows Server 2012 nicht verfügbar. Weitere Informationen zum Installieren oder Entfernen von Rollen, Rollendienste und Features in Windows Server 2012 finden Sie unter [installieren oder Deinstallieren von Rollen, Rollendienste und Features](https://go.microsoft.com/fwlink/?LinkID=239563) auf Microsoft TechNet.

Installiert und entfernt werden, Rollen, Rollendienste und Features. Außerdem zeigt die Liste der aller Rollen, Rollendienste und Features zur Verfügung und zeigt an, die auf diesem Computer installiert sind. Weitere Informationen zu den Rollen, Rollendienste und Features, die Sie angeben können, indem Sie mit diesem Tool finden Sie unter den [Hilfe zu Server Manager](https://go.microsoft.com/fwlink/?LinkID=137387). Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
servermanagercmd -query [[[<Drive>:]<path>]<query.xml>] [-logpath   [[<Drive>:]<path>]<log.txt>]
servermanagercmd -inputpath  [[<Drive>:]<path>]<answer.xml> [-resultpath <result.xml> [-restart] | -whatif] [-logpath [[<Drive>:]<path>]<log.txt>]
servermanagercmd -install <Id> [-allSubFeatures] [-resultpath   [[<Drive>:]<path>]<result.xml> [-restart] | -whatif] [-logpath   [[<Drive>:]<path>]<log.txt>]
servermanagercmd -remove <Id> [-resultpath    <result.xml> [-restart] | -whatif] [-logpath  [[<Drive>:]<path>]<log.txt>]
servermanagercmd [-help | -?]
servermanagercmd -version
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-Abfrage [[[\<Laufwerk >:]\<Pfad >]\<*query.xml*>]|Zeigt eine Liste mit allen Rollen, Rollendienste und Features installiert und verfügbar für die Installation auf dem Server. Sie können auch die Kurzform von diesen Parameter verwenden **- Q**. Wenn die Ergebnisse der Abfrage in eine XML-Datei gespeichert werden sollen, geben Sie eine XML-Datei ersetzen *query.xml*.|
|Inputpath - < [[\<Laufwerk >:]\<Pfad >]*answer.xml*>|Installiert oder entfernt werden, die Rollen, Rollendienste und Features, die in einer XML-Antwortdatei, die durch dargestellt angegeben *answer.xml*. Sie können auch die Kurzform von diesen Parameter verwenden **- p.**|
|– Installieren Sie \< *Id*>|Installiert die Rolle, Rollendienst oder Feature gemäß *Id*. Der Bezeichner sind Groß-/Kleinschreibung. Mehrere Rollen, Rollendienste und Features müssen durch Leerzeichen getrennt werden. Die folgenden optionalen Parameter werden verwendet, mit der **-Installation** Parameter.<br /><br />-   **– Festlegen von** \< *SettingName*>=\<*SettingValue*> Gibt die Einstellungen für die Installation erforderlichen.<br />-   **-AllSubFeatures** gibt an, die Installation aller untergeordneten Dienste und Funktionen zusammen mit der übergeordneten Rolle, Rollendienst oder Feature, mit dem Namen in der *Id* Wert. **Hinweis**:     Einige Rollencontainer keine Befehlszeilen-ID, die Installation von Rollendiensten zuzulassen. Dies ist der Fall, wenn in der gleichen Instanz des Server-Manager-Befehls Rollendienste installiert werden können. Beispielsweise kann nicht der Verbunddienst-Rollendienst, der active Directory-Verbunddienste und den Verbunddienstproxy-Rollendienst installiert werden, mithilfe der gleichen Befehlsinstanz des Server-Manager.<br />-   **-Resultpath** \< *result.xml > speichert die Ergebnisse als XML-Datei, die durch dargestellt *result.xml*. Sie können auch die Kurzform von diesen Parameter verwenden **- R**. **Hinweis:**     Kann nicht ausgeführt werden **Servermanagercmd** sowohl die **- Resultpath** Parameter und die **"- WhatIf"** Parameter wurde angegeben.<br /> -    **-Neustart** startet automatisch den Computer neu, wenn die Installation abgeschlossen ist (sofern es sich um eine neu zu starten, indem Sie die installierten Rollen oder Features erforderlich ist).<br /> -    **"- WhatIf"** zeigt alle Vorgänge angegeben, für die **-installieren** Parameter. Sie können auch die Kurzform von der **"- WhatIf"** Parameter **-w**. Kann nicht ausgeführt werden **Servermanagercmd** sowohl die **- Resultpath** Parameter und die **"- WhatIf"** Parameter wurde angegeben.<br /> -    **- Logpath** \<[[\<Laufwerk >:]\<Pfad >]* log.txt* > Gibt einen Namen und Speicherort für die Protokolldatei, nicht den Standardbereich **%windir%\temp\servermanager.log**.|
|-Entfernen Sie \< *Id*>|Entfernt die Rolle, Rollendienst oder Feature gemäß *Id*. Der Bezeichner sind Groß-/Kleinschreibung. Mehrere Rollen, Rollendienste und Features müssen durch Leerzeichen getrennt werden. Die folgenden optionalen Parameter werden verwendet, mit der **-entfernen Sie** Parameter.<br /><br />-   **-Resultpath** \<[[\<Laufwerk >:]\<Pfad >]*result.xml*> speichert Entfernungsergebnisse in eine XML-Datei, die durch dargestellt *result.xml*. Sie können auch die Kurzform von diesen Parameter verwenden **- R**. **Hinweis**:     Kann nicht ausgeführt werden **Servermanagercmd** sowohl die **- Resultpath** Parameter und die **"- WhatIf"** Parameter wurde angegeben.<br />-   **-Neustart** startet automatisch den Computer neu, wenn die Deinstallation ist abgeschlossen (wenn der Neustart verbleibende Rollen oder Features erforderlich ist).<br />-   **"- WhatIf"** zeigt alle Vorgänge angegeben, für die **-entfernen Sie** Parameter. Sie können auch die Kurzform von der **"- WhatIf"** Parameter **-w**. Kann nicht ausgeführt werden **Servermanagercmd** sowohl die **- Resultpath** Parameter und die **"- WhatIf"** Parameter wurde angegeben.<br />-   **-Logpath**\<[[\<Laufwerk >:]\<Pfad >]*"log.txt"*> Gibt einen Namen und Speicherort für die Protokolldatei, nicht den Standardbereich **%windir%\temp\ Servermanager.log**.|
|-Hilfe|Zeigt Hilfe in einem Eingabeaufforderungsfenster den Befehl. Sie können auch die Kurzform, **-?**.|
|-Version|Zeigt die Anzahl der Server-Manager-Version. Sie können auch die Kurzform, **- V**.|

## <a name="remarks"></a>Hinweise
**ServerManagerCmd** ist veraltet und nicht notwendigerweise in zukünftigen Versionen von Windows unterstützt werden. Es wird empfohlen, wenn Sie Server-Manager auf Computern ausgeführt werden, auf denen Windows Server 2008 R2 ausgeführt werden, die Windows PowerShell-Cmdlets zu verwenden, die für Server-Manager verfügbar sind. Weitere Informationen finden Sie unter [Server-Manager-Cmdlets](https://go.microsoft.com/fwlink/?LinkID=137653).
ServerManagerCmd kann aus einem beliebigen Verzeichnis auf einem lokalen Laufwerk des Servers ausgeführt werden. Sie müssen ein Mitglied der Gruppe "Administratoren" auf dem Server sein, auf denen Sie Software installieren oder deinstallieren möchten.

> [!IMPORTANT]
> Sie müssen aufgrund von sicherheitseinschränkungen durch die Benutzerkontensteuerung in Windows Server 2008 R2, ausführen **Servermanagercmd** in ein Eingabeaufforderungsfenster geöffnet, mit erweiterten Berechtigungen. Dazu, mit der Maustaste der Eingabeaufforderung ein, die ausführbare Datei an, oder die **Eingabeaufforderung** -Objekt, auf die **starten** , und klicken Sie dann auf **als Administrator ausführen**.

## <a name="BKMK_examples"></a>Beispiele für
Das folgende Beispiel zeigt, wie Sie mit **Servermanagercmd** angezeigt wird, eine Liste mit allen Rollen, Rollendienste und Features, die verfügbar sind, und welche Rollen, Rollendienste und Features auf dem Computer installiert sind.
```
servermanagercmd -query
```
Das folgende Beispiel zeigt, wie Sie mit **Servermanagercmd** , installieren Sie die Rolle Webserver (IIS), und speichern Sie die Installationsergebnisse, einer XML-Datei, die durch dargestellt *installResult.xml*.
```
servermanagercmd -install Web-Server -resultpath installResult.xml
```
Das folgende Beispiel zeigt, wie Sie mit der ** Parameter "WhatIf" ** mit **Servermanagercmd** zeigt detaillierte Informationen über die Rollen, Rollendienste und Features, die installiert oder entfernt, basierend auf Anweisungen, werden in einer XML-Antwortdatei, die durch dargestellt angegeben *"Install.xml"*.
```
servermanagercmd -inputpath install.xml -whatif
```

#### <a name="additional-references"></a>Weitere Verweise
-   eine vollständige Liste der die Rolle, Rollendienst oder Feature-IDs können Sie für angeben, die *Id* Parameter oder Weitere Informationen zum Verwenden einer XML-Antwortdatei mit **Servermanagercmd**, finden Sie unter den [Hilfe zu Server Manager](https://go.microsoft.com/fwlink/?LinkID=137387). (https://go.microsoft.com/fwlink/?LinkID=137387).
-   Finden Sie unter [Server-Manager-Cmdlets](https://go.microsoft.com/fwlink/?LinkID=137653) eine Liste der Windows PowerShell-Cmdlets, die für Server-Manager verfügbar sind.
-   [Befehlszeilensyntax](command-line-syntax-key.md)