---
title: Scwcmd-Transformation
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5af1f9d1f2ee5386da8b02f4142c156c3711852f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883097"
---
# <a name="scwcmd-transform"></a>Scwcmd: Transformation

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Transformiert eine mit dem Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) generierte Sicherheitsrichtlinien Datei in ein neues Gruppenrichtlinie Objekt (GPO) in Active Directory Domain Services. Der Transformations Vorgang ändert keine Einstellungen auf dem Server, auf dem er ausgeführt wird. Nachdem der Transformations Vorgang abgeschlossen ist, muss ein Administrator das Gruppenrichtlinien Objekt mit den gewünschten Organisationseinheiten verknüpfen, um die Richtlinie auf den Servern bereitzustellen.

Die Anmelde Informationen des Domänen Administrators sind erforderlich, um den Transformations Vorgang abzuschließen.

> [!IMPORTANT]
> Internetinformationsdienste (IIS)-Sicherheitsrichtlinien Einstellungen können nicht mithilfe von Gruppenrichtlinie bereitgestellt werden.</br>> Firewallrichtlinien, die genehmigte Anwendungen auflisten, sollten nur dann auf Servern bereitgestellt werden, wenn der Windows-Firewalldienst beim letzten Start des Servers automatisch gestartet wurde.



## <a name="syntax"></a>Syntax

```
scwcmd transform /p:<Policyfile.xml> /g:<GPODisplayName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/p\<Policyfile.xml>|Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die angewendet werden soll. Dieser Parameter muss angegeben werden.|
|/g\<GPODisplayName>|Gibt den anzeigen amen des Gruppenrichtlinien Objekts an. Dieser Parameter muss angegeben werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Scwcmd.exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Gruppenrichtlinien Objekt namens fileserversecurity aus einer Datei namens FileServerPolicy.xml zu erstellen:
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)