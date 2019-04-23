---
title: Scwcmd-Transformation
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a6a6e37c2c2a362f3aa0aeadef615ff5065713f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843811"
---
# <a name="scwcmd-transform"></a>scwcmd: transform

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Transformiert eine Sicherheitsrichtliniendatei mit (Security Configuration Wizard, SCW) in eine neue Gruppe Gruppenrichtlinienobjekt (GPO) in Active Directory Domain Services generiert. Die Transformation wird keine Einstellungen auf dem Server geändert, in dem sie ausgeführt wird. Nach der Transformationsvorgang abgeschlossen ist, muss ein Administrator das GPO mit den gewünschten Organisationseinheiten zum Bereitstellen der Richtlinie auf Server verknüpfen.

Domänenadministrator-Anmeldeinformationen sind erforderlich, um den Transformationsvorgang abzuschließen.

> [!IMPORTANT]
> Sicherheitsrichtlinieneinstellungen für Internetinformationsdienste (Internet Information Services, IIS) können nicht mithilfe einer Gruppenrichtlinie bereitgestellt werden.</br>> Genehmigte Anwendungen nicht auf Servern bereitgestellt werden sollten, es sei denn, der Windows-Firewall-Dienst automatisch gestartet, wenn der Server entsprechend seiner letzten Firewall Richtlinien gestartet.

Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
scwcmd transform /p:<Policyfile.xml> /g:<GPODisplayName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ p:\<Policyfile.xml >|Gibt an, der Pfad und Dateiname der XML-Richtliniendatei, die angewendet werden soll. Dieser Parameter muss angegeben werden.|
|/g:\<GPODisplayName>|Gibt den Anzeigenamen des Gruppenrichtlinienobjekts an. Dieser Parameter muss angegeben werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern unter Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 verfügbar.

## <a name="BKMK_Examples"></a>Beispiele für

Um ein Gruppenrichtlinienobjekt namens FileServerSecurity aus einer Datei namens FileServerPolicy.xml zu erstellen, geben Sie Folgendes ein:
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)