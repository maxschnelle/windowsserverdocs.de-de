---
title: dfsutil
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
robots: noindex,nofollow
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45545b4e12d31c293ead5b18b83efd50d7bc37bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439652"
---
# <a name="dfsutil"></a>dfsutil

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Der Befehl Dfsutil verwaltet die DFS-Namespaces, Servern und Clients. DFSutil-Befehle verwenden die ursprüngliche Distributed File System-Terminologie, mit der geänderten DFS-Namespaces-Terminologie als Erklärung für die meisten Befehle bereitgestellt.

Beispiele wie dieser Befehl verwendet werden kann finden Sie unter 

## <a name="syntax"></a>Syntax

```
command </parameter> </param2>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|[dfsutil Root](dfsutil-root.md)|Zeigt an, erstellt, entfernt, importiert, exportiert Namespacestämme.|
|[dfsutil Link](dfsutil-link.md)|Zeigt an, erstellt, entfernt oder Ordner verschoben \(Links\).|
|[dfsutil Target](dfsutil-target.md)|Angezeigt, und erstellen, entfernen Sie Ordner Ziel oder die Namespace-Server.|
|[dfsutil Property](dfsutil-property.md)|Zeigt oder ändert einen Ordner Ziel oder die Namespace-Server.|
|[dfsutil Client](dfsutil-client.md)|Zeigt an, oder ändert Client-Informationen oder der Registrierung Schlüssel.|
|[dfsutil Server](dfsutil-server.md)|Zeigt oder ändert die Konfiguration von Namespaces.|
|[dfsutil Diag](dfsutil-diag.md)|Führen Sie die Diagnose oder Anzeigen von Dfsdirs\/Dfspath.|
|[dfsutil Domain](dfsutil-domain.md)|Zeigt alle in der Domäne\-basierend Namespaces in einer Domäne.|
|[dfsutil Cache](dfsutil-cache.md)|Zeigt an, oder der Clientcache geleert.|
|[dfsutil oldcli](dfsutil-oldcli.md)|Verwenden Sie die Dfsutil \/Oldcli Befehl aus, um die ursprüngliche Dfsutil-Syntax verwenden.|

## <a name="remarks-optional-section"></a>"Hinweise" <optional section>
Wenn Sie angeben, dass ein Objekt \(wie z. B. einen Namespaceserver\) am Ende eines Befehls, werden die meisten Befehle Informationen über das Objekt ohne weitere Parameter oder Befehle angezeigt. Z. B. Wenn Sie die Dfsutil Root-Befehl verwenden zu können, können Sie einen Namespacestamm an den Befehl zum Anzeigen von Informationen über das Stammverzeichnis anfügen.

## <a name="BKMK_Examples"></a>Beispiele für
&lt;Hier ist, fügen Sie eine ausführliche Beschreibung der Ihres Beispiels hinzu.&gt;

```
This /is /the /example /of /calling /command /with /parameters
```

&lt;Hier ist, fügen Sie eine ausführliche Beschreibung der ein weiteres Beispiel hinzu.&gt;

```
This /is /a:different /example
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


