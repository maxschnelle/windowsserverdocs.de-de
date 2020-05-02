---
title: Update-Server Files
description: Referenz Thema für Update-serverfiles, das Dateien im freigegebenen Ordner "REMINST" mithilfe der neuesten Dateien aktualisiert, die im Ordner "%windir%\system32\reminst" des Servers gespeichert sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0005d8e198300c4aad9fdfc772957b460d6fee74
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721383"
---
# <a name="update-serverfiles"></a>Update-Server Files

Aktualisiert Dateien im Ordner "REMINST Shared" mithilfe der neuesten Dateien, die im Ordner "%windir%\system32\reminst" des Servers gespeichert sind. Um die Gültigkeit der Installation der Windows-Bereitstellungs Dienste sicherzustellen, sollten Sie diesen Befehl einmal nach jedem Server Upgrade, Service Pack Installation oder Update von Windows-Bereitstellungs Dienst Dateien ausführen.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Update-ServerFiles [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[/Server:\<Server Name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Um die Dateien zu aktualisieren, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)