---
title: tcmsetup
description: Erfahren Sie, wie Sie den TAPI-Client einrichten und deaktivieren.
ms.topic: reference
ms.assetid: 15e0c10f-996f-4301-92e5-943f7ee8212d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2d148a273aaf6de917cec546f487fab5e8ebea0
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027088"
---
# <a name="tcmsetup"></a>tcmsetup



Richtet den TAPI-Client ein oder deaktiviert ihn.

## <a name="syntax"></a>Syntax

```
tcmsetup [/q] [/x] /c <Server1> [<Server2> …]
tcmsetup  [/q] /c /d
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/q|Verhindert die Anzeige von Meldungs Feldern.|
|/x|Gibt an, dass Verbindungs orientierte Rückrufe für große Verkehrs Netzwerke verwendet werden, bei denen der Paketverlust hoch ist. Wenn dieser Parameter ausgelassen wird, werden verbindungslose Rückrufe verwendet.|
|/C|Erforderlich. Gibt die Client Einrichtung an.|
|\<Server1>|Erforderlich. Gibt den Namen des Remote Servers an, der über die TAPI-Dienstanbieter verfügt, die vom Client verwendet werden. Der Client verwendet die Zeilen und Telefone des Dienstanbietern. Der Client muss sich in derselben Domäne wie der-Server oder in einer Domäne befinden, die über eine bidirektionale Vertrauensstellung mit der Domäne verfügt, in der der Server enthalten ist.|
|\<Server2>…|Gibt alle zusätzlichen Server an, die für diesen Client verfügbar sein werden. Wenn Sie eine Liste der Server angeben, verwenden Sie ein Leerzeichen, um die Servernamen zu trennen.|
|/d|Löscht die Liste der Remote Server. Deaktiviert den TAPI-Client, indem verhindert wird, dass er die TAPI-Dienstanbieter verwendet, die sich auf den Remote Servern befinden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Um diese Schritte auszuführen, müssen Sie Mitglied der Gruppe "Administratoren" auf dem lokalen Computer sein, oder die entsprechende Berechtigung muss an Sie delegiert worden sein. Wenn der Computer zu einer Domäne gehört, können möglicherweise Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren ausführen. Als Best Practice für die Sicherheit sollten Sie dieses Verfahren über **Ausführen als** ausführen.
-   Damit TAPI ordnungsgemäß funktioniert, müssen Sie **tcmsetup** ausführen, um die Remote Server anzugeben, die von TAPI-Clients verwendet werden.
-   Bevor ein Client Benutzer ein Telefon oder eine Zeile auf einem TAPI-Server verwenden kann, muss der Benutzer des Telefonieservers den Benutzer dem Telefon oder der Zeile zuweisen.
-   Die Liste der von diesem Befehl erstellten Telefonieserver ersetzt jede vorhandene Liste von Telefonieservern, die für den Client verfügbar sind. Sie können diesen Befehl nicht verwenden, um der vorhandenen Liste hinzuzufügen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Übersicht über Befehlsshell](/previous-versions/windows/it-pro/windows-server-2003/cc737438(v=ws.10))

[Angeben von Telefonieservern auf einem Client Computer](/previous-versions/windows/it-pro/windows-server-2003/cc759226(v=ws.10))

[Zuweisen eines Telefoniebenutzers zu einer Zeile oder einem Telefon](/previous-versions/windows/it-pro/windows-server-2003/cc736875(v=ws.10))
