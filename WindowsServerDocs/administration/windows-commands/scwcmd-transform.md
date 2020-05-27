---
title: Scwcmd-Transformation
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86c88f0207a53da813f5d4eaed399375bfc5bc02
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820950"
---
# <a name="scwcmd-transform"></a>Scwcmd: transform

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
|/p: \< policyFile. XML>|Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die angewendet werden soll. Dieser Parameter muss angegeben werden.|
|/g: \< gpodisplayname>|Gibt den anzeigen amen des Gruppenrichtlinien Objekts an. Dieser Parameter muss angegeben werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Gruppenrichtlinien Objekt namens fileserversecurity aus einer Datei namens fileserverpolicy. XML zu erstellen:
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)