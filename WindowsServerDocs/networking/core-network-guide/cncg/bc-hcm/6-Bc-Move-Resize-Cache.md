---
title: Verschieben und Ändern der Größe der gehosteten Caches (Optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2a3ed1d6de1281575b33cdf75a5970d2ed033085
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>Verschieben und Ändern der Größe der gehostete Cache \(Optional\)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können dieses Verfahren verwenden, auf den gehosteten Cache in den Ordner, in der Sie arbeiten und das Laufwerk verschieben, und die Menge des Speicherplatzes angeben, die der gehosteten Cacheserver für den gehosteten Cache verwenden kann.

Dieses Verfahren ist optional. Wenn die Standard-Cache Speicherort \(%windir%\\ServiceProfiles\\NetworkService\\AppData\\Local\\PeerDistPub\) und Größe – die 5 % der gesamte Festplattenspeicherplatz ist – für Ihre Bereitstellung geeignet sind, müssen Sie nicht ändern.

Sie müssen ein Mitglied der Gruppe "Administratoren" zum Ausführen dieses Verfahrens werden.

### <a name="to-move-and-resize-the-hosted-cache"></a>Verschieben und Ändern der Größe des gehosteten Caches

1. Öffnen Sie Windows PowerShell mit Administratorrechten.

2. Geben Sie den folgenden Befehl auf den gehosteten Cache auf dem lokalen Computer an einen anderen Speicherort zu verschieben, und drücken Sie dann die EINGABETASTE.

    > [!IMPORTANT]
    > Ersetzen Sie vor dem Ausführen des folgenden Befehls, Parameterwerte, z. B. – Pfad und – MoveTo, mit den Werten, die für Ihre Bereitstellung geeignet sind.

    ``` 
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ``` 

3.  Geben Sie den folgenden Befehl zum Ändern der Größe des gehosteten cache – insbesondere die Datacache \ – auf dem lokalen Computer. Drücken Sie die EINGABETASTE.

    > [!IMPORTANT]
    > Ersetzen Sie vor dem Ausführen des folgenden Befehls, Parameterwerte, z. B. \-Percentage, mit den Werten, die für Ihre Bereitstellung geeignet sind.  

    ``` 
    Set-BCCache -Percentage 20
    ``` 

4.  Um die gehosteten Server-Konfiguration zu überprüfen, geben Sie folgenden Befehl aus, und drücken die EINGABETASTE.

    ``` 
    Get-BCStatus
    ``` 

    Die Ergebnisse des Befehls der Status für alle Aspekte der BranchCache-Installation. Im folgenden sind einige der BranchCache-Einstellungen und der richtige Wert für die einzelnen Elemente:

    -   DataCache | CacheFileDirectoryPath: Zeigt die Festplatte-Speicherort, die dem Wert übereinstimmt, den Sie mit der MoveTo-Parameter des Befehls SetBCCache bereitgestellt. Wenn Sie den Wert D:\\datacache angegeben, wird dieser Wert in der Befehlsausgabe angezeigt.

    -   DataCache | MaxCacheSizeAsPercentageOfDiskVolume: Zeigt an, die mit dem Wert übereinstimmt, die, den Sie mit dem – Prozentsatz-Parameter des Befehls SetBCCache bereitgestellt. Wenn Sie den Wert 20 angegeben, wird dieser Wert in der Befehlsausgabe angezeigt.

Wenn Sie mit dieser Anleitung fortfahren, finden Sie unter [Prehash und Vorabladen von Inhalt an den gehosteten Cacheserver & #40; Optional & #41; ](7-Bc-Prehash-Preload.md).