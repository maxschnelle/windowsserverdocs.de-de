---
title: tcmsetup
description: Informationen Sie zum Einrichten und deaktivieren die TAPI-Client.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15e0c10f-996f-4301-92e5-943f7ee8212d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac92c7b793274227bd20e6fa90a4106a32ea0446
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862001"
---
# <a name="tcmsetup"></a>tcmsetup



Legt fest, oder der TAPI-Client deaktiviert.

## <a name="syntax"></a>Syntax

```
tcmsetup [/q] [/x] /c <Server1> [<Server2> …] 
tcmsetup  [/q] /c /d
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/q|Verhindert die Anzeige der Meldungsfelder an.|
|/x|Gibt an, dass es sich bei einem verbindungsorientierten Rückrufe für stark ausgelastete Netzwerke verwendet werden, in dem Paketverlust zu hoch ist. Wenn dieser Parameter ausgelassen wird, werden die verbindungslose Rückrufe verwendet werden.|
|/c|Erforderlich. Gibt die Clientsetup an.|
|\<Server1>|Erforderlich. Gibt den Namen des Remoteservers, der die TAPI-Anbieter verfügt, die vom Client verwendet wird. Der Client wird die Dienstanbieter Anschlüsse und Telefone verwenden. Der Client muss in der gleichen Domäne wie der Server oder in einer Domäne, die über eine bidirektionale Vertrauensstellung mit der Domäne verfügt, die der Server enthält.|
|\<Server2>…|Gibt an, alle weiteren Server oder Server, die den Client zur Verfügung stehen. Wenn Sie, dass eine Liste der Server ist angeben, verwenden Sie ein Leerzeichen trennen Sie die Servernamen.|
|/d|Löscht die Liste von Remoteservern. Deaktiviert. den TAPI-Client wird verhindert, dass Sie die TAPI-Dienstanbieter, die auf dem Remoteserver vorhanden sind.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um diese Schritte ausführen zu können, müssen Sie auf dem lokalen Computer ein Mitglied der Gruppe %%amp;quot;Administratoren%%amp;quot; sein oder Ihnen muss die entsprechende Berechtigung übertragen worden sein. Wenn der Computer zu einer Domäne gehört, können möglicherweise Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren ausführen. Als Best Practice für die Sicherheit sollten Sie dieses Verfahren über **Ausführen als** ausführen.
-   In der Reihenfolge für TAPI ordnungsgemäß funktioniert, müssen Sie ausführen **Tcmsetup** Remoteserver angeben, die von TAPI-Clients verwendet werden.
-   Bevor ein Client-Benutzer einem Smartphone oder der Zeile auf ein TAPI-Server verwenden kann, muss die Telefonie-Server-Administrator den Benutzer auf das Telefon oder Zeile zuweisen.
-   Die Liste der Telefonieserver, die mit diesem Befehl erstellt wird, ersetzt jede vorhandene Liste der Telefonieserver für den Client verfügbar. Mit diesem Befehl können Sie der vorhandenen Liste hinzugefügt.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Übersicht über die Befehlsshell](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)

[Geben Sie die Telefonieserver auf einem Clientcomputer](https://technet.microsoft.com/library/cc759226(v=ws.10).aspx)

[Zuweisen eines Telefoniebenutzers zu einer Zeile oder einem Telefon](https://technet.microsoft.com/library/cc736875(v=ws.10).aspx)

