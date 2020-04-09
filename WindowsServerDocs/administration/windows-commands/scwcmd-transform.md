---
title: Scwcmd-Transformation
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1fed9ff6369e6c966d9d1f5295db7db6648a1ab1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835123"
---
# <a name="scwcmd-transform"></a>scwcmd: transform

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Transformiert eine mit dem Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) generierte Sicherheitsrichtlinien Datei in ein neues Gruppenrichtlinie Objekt (GPO) in Active Directory Domain Services. Der Transformations Vorgang ändert keine Einstellungen auf dem Server, auf dem er ausgeführt wird. Nachdem der Transformations Vorgang abgeschlossen ist, muss ein Administrator das Gruppenrichtlinien Objekt mit den gewünschten Organisationseinheiten verknüpfen, um die Richtlinie auf den Servern bereitzustellen.

Die Anmelde Informationen des Domänen Administrators sind erforderlich, um den Transformations Vorgang abzuschließen.

> [!IMPORTANT]
> Internetinformationsdienste (IIS)-Sicherheitsrichtlinien Einstellungen können nicht mithilfe von Gruppenrichtlinie bereitgestellt werden.</br>> Firewallrichtlinien, die genehmigte Anwendungen auflisten, sollten nur dann auf Servern bereitgestellt werden, wenn der Windows-Firewalldienst beim letzten Start des Servers automatisch gestartet wurde.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
scwcmd transform /p:<Policyfile.xml> /g:<GPODisplayName>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/p:\<policyFile. XML >|Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die angewendet werden soll. Dieser Parameter muss angegeben werden.|
|/g:\<gpodisplayname >|Gibt den anzeigen amen des Gruppenrichtlinien Objekts an. Dieser Parameter muss angegeben werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Geben Sie Folgendes ein, um ein Gruppenrichtlinien Objekt namens fileserversecurity aus einer Datei namens fileserverpolicy. XML zu erstellen:
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)