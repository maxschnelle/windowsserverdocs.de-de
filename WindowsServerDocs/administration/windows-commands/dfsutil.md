---
title: Dfsutil
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 1a06806b109bbd324213f935892bbbab415362df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377979"
---
# <a name="dfsutil"></a>Dfsutil

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Dfsutil-Befehl verwaltet DFS-Namespaces,-Server und-Clients. Dfsutil-Befehle verwenden die ursprüngliche verteiltes Dateisystem Terminologie, wobei die aktualisierte Terminologie für DFS-Namespaces als Erklärung für die meisten Befehle bereitgestellt wird.

Beispiele dazu, wie dieser Befehl verwendet werden kann, finden Sie unter. 

## <a name="syntax"></a>Syntax

```
command </parameter> </param2>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|[Dfsutil-Stamm](dfsutil-root.md)|Zeigt, erstellt, entfernt, importiert und exportiert Namespace Stämme.|
|[Dfsutil-Link](dfsutil-link.md)|Hiermit werden Ordner \(Verknüpfungen\)angezeigt, erstellt, entfernt oder verschoben.|
|[Dfsutil-Ziel](dfsutil-target.md)|Zeigt, erstellt oder entfernt den Ordner Ziel-oder Namespace Server.|
|[Dfsutil (Eigenschaft)](dfsutil-property.md)|Zeigt ein Ordner Ziel oder einen Namespace Server an oder ändert ihn.|
|[Dfsutil-Client](dfsutil-client.md)|Zeigt Client Informationen oder Registrierungsschlüssel an oder ändert Sie.|
|[Dfsutil-Server](dfsutil-server.md)|Dient zum Anzeigen oder Ändern der Namespace Konfiguration.|
|[Dfsutil Diag](dfsutil-diag.md)|Ausführen von Diagnosen oder Anzeigen von dfsdirs\/dfspath.|
|[Dfsutil-Domäne](dfsutil-domain.md)|Zeigt alle Domänen\-basierten Namespaces in einer Domäne an.|
|[Dfsutil-Cache](dfsutil-cache.md)|Zeigt den Client Cache an oder leert ihn.|
|[Dfsutil oldcli](dfsutil-oldcli.md)|Verwenden Sie den Befehl Dfsutil \/oldcli, um die ursprüngliche Dfsutil-Syntax zu verwenden.|

## <a name="remarks-optional-section"></a>Hinweise <optional section>
Wenn Sie ein Objekt \(z. b. einen Namespace Server\) am Ende eines Befehls festlegen, werden die meisten Befehle Informationen über das Objekt anzeigen, ohne weitere Parameter oder Befehle zu erfordern. Wenn Sie z. b. den Befehl Dfsutil root verwenden, können Sie einen Namespace Stamm an den Befehl anfügen, um Informationen zum Stamm anzuzeigen.

## <a name="BKMK_Examples"></a>Beispiele
&lt;hier finden Sie eine ausführliche Beschreibung ihres Beispiels.&gt;

```
This /is /the /example /of /calling /command /with /parameters
```

&lt;hier finden Sie eine ausführliche Beschreibung eines anderen Beispiels.&gt;

```
This /is /a:different /example
```

## <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


