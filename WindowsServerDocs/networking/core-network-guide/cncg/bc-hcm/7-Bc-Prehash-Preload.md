---
title: Prehashing und Vorabladen von Inhalt auf dem gehosteten Cacheserver (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b60a1f24b8988d6e394df0faf678467021e0c882
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839391"
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>Unterziehen und Vorabladen von Inhalt auf dem gehosteten Cacheserver \(Optional\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können die Verfahren in diesem Abschnitt Hashes von Inhalten auf der Inhaltsserver Datenpakete den Inhalt hinzu, und klicken Sie dann den Inhalt auf die gehosteten Cacheserver vorab. 

Diese Verfahren sind optional, da Sie auf die gehosteten Cacheserver nicht zu prehash und preload Inhalten erforderlich sind. 

Wenn Sie Inhalt nicht vorab laden, werden dem gehosteten Cache automatisch Daten hinzugefügt, wie Clients über die WAN-Verbindung heruntergeladen.

>[!IMPORTANT]
>Diese Verfahren sind zusammen optional, wenn Sie die prehash und preload-Inhalten auf die gehosteten Cacheserver, entscheiden zwar beide Verfahren erforderlich.

- [Erstellen von Inhaltsserver Datenpakete für das Web und Inhalt der Datei &#40;Optional&#41;](8-Bc-Data-Packages.md)
  
- [Importieren Sie Datenpakete auf dem gehosteten Cacheserver &#40;Optional&#41;](9-Bc-Import-Data.md)

Mit diesem Handbuch finden Sie [erstellen-Server Daten Inhaltspaketen für Web- und Dateiinhalt &#40;Optional&#41;](8-Bc-Data-Packages.md).