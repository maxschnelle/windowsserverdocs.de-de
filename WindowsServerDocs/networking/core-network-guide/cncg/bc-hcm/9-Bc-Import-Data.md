---
title: Importieren von Datenpaketen auf dem gehosteten Cacheserver (Optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e0bd8f12ab76c8e2bf03ba79ce46a4cbea2f4dc5
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>Importieren von Datenpaketen auf dem gehosteten Cache-Server \(Optional\)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können dieses Verfahren zum Importieren von Datenpaketen und Vorabladen von Inhalt auf Ihrer gehosteten Cacheserver verwenden.

Dieses Verfahren ist optional, da Sie auf die gehosteten Cacheserver nicht prehash und vorab geladene erforderlich sind.

Andernfalls nicht auf Inhalte registrierungseintragswert laden, werden dem gehosteten Cache automatisch Daten hinzugefügt, wie Clients über die WAN-Verbindung heruntergeladen.

Sie müssen ein Mitglied der Gruppe "Administratoren" zum Ausführen dieses Verfahrens werden.

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>Importieren von Datenpaketen auf dem gehosteten Cacheserver  

1. Öffnen Sie auf dem Servercomputer des Windows PowerShell mit Administratorrechten.

2. Geben Sie folgenden Befehl ein, ersetzen den Wert für den – Path-Parameter mit dem Speicherort, in dem Sie Ihre Datenpakete gespeichert haben, und drücken Sie dann die EINGABETASTE.

    ```  
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```  

3. Wenn Sie mehr als einen gehosteten Cacheserver haben, in dem Sie Inhalt vorab laden möchten, führen Sie dieses Verfahren auf jedem Cacheserver gehosteten.

Wenn Sie mit dieser Anleitung fortfahren, finden Sie unter [konfigurieren Sie automatische gehosteten Cache Clientermittlung nach Dienstverbindungspunkt](10-Bc-Client-By-Scp.md).
