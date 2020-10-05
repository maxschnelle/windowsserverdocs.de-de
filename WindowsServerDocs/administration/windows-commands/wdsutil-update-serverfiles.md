---
title: Update-Server Files
description: Referenz Artikel zu Update-serverfiles, mit dem Dateien im freigegebenen Ordner "REMINST" mithilfe der neuesten Dateien aktualisiert werden, die im Ordner "%windir%\system32\reminst" des Servers gespeichert sind.
ms.topic: reference
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1a984c789a309395dcee0d93a6ba0877c44aab22
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730592"
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
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Um die Dateien zu aktualisieren, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)