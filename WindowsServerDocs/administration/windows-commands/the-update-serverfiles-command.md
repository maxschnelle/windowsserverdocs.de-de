---
title: Update-Server Files
description: Referenz Artikel zu Update-serverfiles, mit dem Dateien im freigegebenen Ordner "REMINST" mithilfe der neuesten Dateien aktualisiert werden, die im Ordner "%windir%\system32\reminst" des Servers gespeichert sind.
ms.topic: reference
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4ba2ed4129f1575d5057d2fc88500c0c47e291fc
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036108"
---
# <a name="update-serverfiles"></a>Update-Server Files

Aktualisiert Dateien im Ordner "REMINST Shared" mithilfe der neuesten Dateien, die im Ordner "%windir%\system32\reminst" des Servers gespeichert sind. Um die Gültigkeit der Installation der Windows-Bereitstellungs Dienste sicherzustellen, sollten Sie diesen Befehl einmal nach jedem Server Upgrade, Service Pack Installation oder Update von Windows-Bereitstellungs Dienst Dateien ausführen.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Update-ServerFiles [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Um die Dateien zu aktualisieren, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)