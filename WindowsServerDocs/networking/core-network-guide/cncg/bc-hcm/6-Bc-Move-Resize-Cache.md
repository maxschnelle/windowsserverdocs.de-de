---
title: Verschieben und Ändern der Größe des gehosteten Caches (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8eed5b91d0634a8409b6b6e26f823ffe86ea8a14
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964266"
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>Verschieben und Ändern der Größe des gehosteten Caches \( optional\)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit diesem Verfahren können Sie den gehosteten Cache auf das gewünschte Laufwerk und den gewünschten Ordner verschieben und den Speicherplatz angeben, der vom gehosteten Cache Server für den gehosteten Cache verwendet werden kann.

Dieses Verfahren ist optional. Wenn für die Bereitstellung der Standard Cache Speicherort \( % windir% \\ Service Profiles \\ Network Service \\ AppData \\ local \\ peerdistpub \) und Size – 5% des gesamten Festplatten Speicherplatzes – geeignet ist, müssen Sie diese nicht ändern.

Sie müssen Mitglied der Gruppe Administratoren sein, um dieses Verfahren auszuführen.

### <a name="to-move-and-resize-the-hosted-cache"></a>So verschieben Sie den gehosteten Cache und ändern die Größe

1. Öffnen Sie Windows PowerShell mit Administrator Rechten.

2. Geben Sie den folgenden Befehl ein, um den gehosteten Cache an einen anderen Speicherort auf dem lokalen Computer zu verschieben, und drücken Sie die EINGABETASTE

    > [!IMPORTANT]
    > Ersetzen Sie vor dem Ausführen des folgenden Befehlsparameter Werte (z. b. – Path und – muveto) durch Werte, die für Ihre Bereitstellung geeignet sind.

    ```
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ```

3.  Geben Sie den folgenden Befehl ein, um die Größe des gehosteten Caches zu ändern – insbesondere die datacache \- auf dem lokalen Computer. Drücken Sie die EINGABETASTE.

    > [!IMPORTANT]
    > Ersetzen Sie vor dem Ausführen des folgenden Befehlsparameter Werte (z \- . b. Prozentsatz) durch Werte, die für Ihre Bereitstellung geeignet sind.

    ```
    Set-BCCache -Percentage 20
    ```

4.  Um die Serverkonfiguration für den gehosteten Cache zu überprüfen, geben Sie den folgenden Befehl ein, und drücken Sie

    ```
    Get-BCStatus
    ```

    Mit den Ergebnissen des Befehls wird der Status für alle Aspekte der BranchCache-Installation angezeigt. Im folgenden sind einige der BranchCache-Einstellungen und der richtige Wert für jedes Element aufgeführt:

    -   Datacache | Cachefiledirectorypath: zeigt den Speicherort der Festplatte an, der dem Wert entspricht, den Sie mit dem Parameter "–" des Befehls "setbccache" angegeben haben. Wenn Sie z. b. den Wert D: \\ datacache angegeben haben, wird dieser Wert in der Befehlsausgabe angezeigt.

    -   Datacache | Maxcachesizeasprozageofdiskvolume: zeigt die Zahl an, die mit dem Wert übereinstimmt, den Sie mit dem Parameter – Prozent des Befehls setbccache angegeben haben. Wenn Sie z. b. den Wert 20 angegeben haben, wird dieser Wert in der Befehlsausgabe angezeigt.

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [vorab Hash und vorab Laden von Inhalten auf dem gehosteten Cache Server &#40;optionale&#41;](7-Bc-Prehash-Preload.md).