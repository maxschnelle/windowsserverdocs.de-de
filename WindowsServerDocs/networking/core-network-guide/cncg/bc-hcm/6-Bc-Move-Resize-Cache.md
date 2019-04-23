---
title: Verschieben und Ändern der Größe des gehosteten Caches (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cb75e06b5da8ff95fcf763b22c5160ea200035f3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853531"
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>Verschiebe und verkleinere Sie den gehosteten Cache \(Optional\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können dieses Verfahren verwenden, um dem gehosteten Cache zu verschieben, auf dem Laufwerk bzw. Ordner, die Sie bevorzugen, und die Menge des Speicherplatzes angeben, die für den gehosteten Cache des gehosteten cacheservers verwenden können.

Dieses Verfahren ist optional. Wenn der standardmäßige Speicherort zwischenspeichern \(% windir%\\ServiceProfiles\\NetworkService\\AppData\\lokalen\\PeerDistPub\) und Größe – die 5 % der gesamten Festplatte ist. Speicherplatz – eignen sich für Ihre Bereitstellung, Sie müssen nicht ändern.

Sie müssen Mitglied der Gruppe Administratoren sein, um dieses Verfahren auszuführen.

### <a name="to-move-and-resize-the-hosted-cache"></a>Zum Verschieben und ändern Sie die Größe des gehosteten Caches

1. Öffnen Sie Windows PowerShell mit Administratorrechten aus.

2. Geben Sie den folgenden Befehl aus, um dem gehosteten Cache auf dem lokalen Computer an einen anderen Speicherort zu verschieben, und drücken Sie dann die EINGABETASTE.

    > [!IMPORTANT]
    > Ersetzen Sie vor dem Ausführen des folgenden Befehls, Parameterwerte, z. B. "–" Path "und" – "MoveTo", mit Werten, die für Ihre Bereitstellung geeignet sind.

    ``` 
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ``` 

3.  Geben Sie den folgenden Befehl zum Ändern der Größe des gehosteten cache – insbesondere die Datacache \- auf dem lokalen Computer. Drücken Sie die EINGABETASTE.

    > [!IMPORTANT]
    > Bevor Sie den folgenden Befehl ausführen, ersetzen Sie die Werte, wie z. B. \--Prozentsatz, mit Werten, die für Ihre Bereitstellung geeignet sind.  

    ``` 
    Set-BCCache -Percentage 20
    ``` 

4.  Um die Serverkonfiguration für gehostete Caches zu überprüfen, geben Sie den folgenden Befehl aus, und drücken Sie EINGABETASTE.

    ``` 
    Get-BCStatus
    ``` 

    Die Ergebnisse des Befehls der Status für alle Aspekte der BranchCache-Installation. Es folgen einige der BranchCache-Einstellungen und den richtigen Wert für jedes Element:

    -   DataCache | CacheFileDirectoryPath: Zeigt den Speicherort der Festplatte, der mit dem Wert übereinstimmt, die, den Sie mit dem "MoveTo"-Parameter des Befehls SetBCCache angegeben. Angenommen, Sie angegeben, dass den Wert "d:"\\Datacache, dass der Wert in der Befehlsausgabe angezeigt wird.

    -   DataCache | MaxCacheSizeAsPercentageOfDiskVolume: Zeigt die Anzahl, die mit dem Wert übereinstimmt, die, den Sie mit dem – Prozentsatz-Parameter des Befehls SetBCCache angegeben. Wenn Sie den Wert 20 angegeben, wird dieser Wert z. B. in der Befehlsausgabe angezeigt.

Mit diesem Handbuch finden Sie [Prehash und Vorabladen von Inhalt auf dem gehosteten Cacheserver &#40;Optional&#41;](7-Bc-Prehash-Preload.md).