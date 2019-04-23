---
title: Importieren von Datenpaketen auf dem gehosteten Cacheserver (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 440ef1e04143cba09213ffea634aa9d4fea51dab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888001"
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>Importieren Sie Datenpakete auf dem gehosteten Cacheserver \(Optional\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können dieses Verfahren verwenden, Datenpakete importieren und Vorabladen von Inhalt auf die gehosteten Cacheserver.

Dieses Verfahren ist optional, da Sie auf die gehosteten Cacheserver nicht zu prehash und preload Inhalten erforderlich sind.

Wenn Sie nicht vor tun\-laden Inhalt, auf Daten werden auf dem gehosteten Cache automatisch hinzugefügt, wie sie über die WAN-Verbindung von Clients heruntergeladen.

Sie müssen Mitglied der Gruppe Administratoren sein, um dieses Verfahren auszuführen.

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>Zum Importieren von Daten auf dem gehosteten Cacheserver-Pakete  

1. Öffnen Sie auf dem Server-Computer Windows PowerShell mit Administratorrechten aus.

2. Geben Sie den folgenden Befehl ein, und Ersetzen Sie den Wert für den-Path-Parameter mit dem Speicherort, in dem Sie Ihre Datenpakete gespeichert haben, und drücken Sie dann die EINGABETASTE.

    ```  
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```  

3. Wenn Sie mehr als einen gehosteten Cacheserver verfügen, in dem Sie Inhalt vorab laden möchten, führen Sie dieses Verfahren auf jedem Server gehosteten Cache.

Mit diesem Handbuch finden Sie [konfigurieren Sie automatische gehosteten Cache Clientermittlung nach Dienstverbindungspunkt](10-Bc-Client-By-Scp.md).
