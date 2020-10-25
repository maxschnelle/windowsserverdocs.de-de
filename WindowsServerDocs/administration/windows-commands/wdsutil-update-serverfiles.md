---
title: Update-ServerFiles
description: Referenz Artikel zu Update-serverfiles, mit dem Dateien im freigegebenen Ordner "REMINST" mithilfe der neuesten Dateien aktualisiert werden, die im Ordner "%windir%\system32\reminst" des Servers gespeichert sind.
ms.topic: reference
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7684dfb694ac6814d00c91363d6573be5cf7be7f
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524895"
---
# <a name="update-serverfiles"></a>Update-ServerFiles

Aktualisiert Dateien im Ordner "REMINST Shared" mithilfe der neuesten Dateien, die im Ordner "%windir%\system32\reminst" des Servers gespeichert sind. Um die Gültigkeit der Installation der Windows-Bereitstellungs Dienste sicherzustellen, sollten Sie diesen Befehl einmal nach jedem Server Upgrade, Service Pack Installation oder Update von Windows-Bereitstellungs Dienst Dateien ausführen.

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /Update-ServerFiles [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Um die Dateien zu aktualisieren, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Update-ServerFiles
wdsutil /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)