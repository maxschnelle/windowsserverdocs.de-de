---
title: PowerShell in Erweiterungen verwenden
description: Mithilfe von PowerShell in Ihrer Erweiterung-SDK für Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ae5004104150c510a56c06161c9280e029968298
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867601"
---
# <a name="using-powershell-in-your-extension"></a>PowerShell in Erweiterungen verwenden #

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In das Windows Admin Center-Extensions-SDK wechseln wir tiefer greifende - sprechen wir über die PowerShell-Befehle zu Ihrer Erweiterung hinzufügen.

## <a name="powershell-in-typescript"></a>PowerShell in TypeScript ##

Der Gulp-Build-Prozess hat einen generieren Schritt, der alle ". ps1", die befindet sich im Ordner "/ Src/Ressourcen/Scripts", und erstellen sie in der Klasse "Powershell-Skripts" im Ordner "/ Src/generiert" gelangen.

>[!NOTE] 
> "Powershell-scripts.ts" noch die "strings.ts"-Dateien nicht manuell aktualisiert werden. Jede Änderung, die Sie vornehmen, werden auf der nächsten Generierung überschrieben.

### <a name="adding-your-own-powershell-script"></a>Hinzufügen eigener PowerShell-Skripts ##

Wir fügen Weitere Informationen zum Hinzufügen von Ihren eigenen PowerShell-Skripts in Kürze.

### <a name="managing-powershell-sessions"></a>Verwalten von PowerShell-Sitzungen ###

Wenn Sie mithilfe von PowerShell in Windows Admin Center verwenden, sind Sitzungen eine erforderliche Komponente der Skriptprozess für die Ausführung an. Zum Ausführen von Skripts auf den remote verwalteten Servern mithilfe von PowerShell Runspaces. Windows Admin Center umschließt Runspace-Erstellung und Verwaltung in einem PowerShellSession-Objekt zum Verwalten der Lebensdauer und Wiederverwendung von Runspace für die sequenzielle skriptausführung aktivieren.

Jede Komponente benötigt, um einen Verweis auf ein Objekt zu erstellen, die von der AppContextService-Klasse, die über drei verschiedene Optionen erstellt wird:
<!-- I don't 100% get this part - it looks like you're adding 3 arguments - nodeName, <session key>, and <PowerShellSessionRequestOptions>. I got that from looking at the examples, not the text. We need to rework those paras explaining. -->
``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName);
```

Durch die Bereitstellung des Knotennamens ein, die CreateSession-Methode, eine neue PowerShell-Sitzung erstellt, verwendet, und klicken Sie dann sofort nach Abschluss des PowerShell-Aufrufs zerstört. Diese Funktion eignet sich für die einmalige aufrufen, aber die wiederholte Verwendung kann die Leistung beeinträchtigen. Eine Sitzung dauert ungefähr 1 Sekunde erstellen, daher kontinuierlich Wiederverwendung Sitzungen kann Verzögerungen verursachen.

``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName, '<session key>');
```

Der erste optionale Parameter ist der \<Sitzungsschlüssel\> Parameter. Dadurch wird eine verschlüsselte Sitzung, die kann nachgeschlagen und wiederverwendet werden, auch über Komponenten (d. h. Component1 eine Sitzung mit Schlüssel "KMU-ROCKS" erstellen kann und Component2 dieselbe Sitzung können) erstellt.  

``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName, '<session key>', <PowerShellSessionRequestOptions>);
```
<!-- The second optional parameter is \<PowerShellSessionRequestOptions\> that does ... ? -->
### <a name="common-patterns"></a>Allgemeine Muster ###

In den meisten Fällen erstellen Sie eine verschlüsselte Sitzung in der **NgOnInit** -Methode, und klicken Sie dann verwerfen Sie sie in einem **NgOnDestroy**. Folgen Sie diesem Muster, wenn mehrere PowerShell-Skripts in eine Komponente, aber der zugrundeliegenden Sitzung, die Komponenten ist nicht gemeinsam vorhanden sind.

Für optimale Ergebnisse Sie sitzungserstellung innerhalb von Komponenten anstelle von Services verwaltet wird – damit wird sichergestellt, Lebensdauer und die Bereinigung ordnungsgemäß verwaltet werden kann.