---
title: Problembehandlung bei Problemen mit Domain Name System (DNS)
description: In diesem Artikel wird erläutert, wie Sie Daten sammeln, wenn DNS-Probleme auftreten.
manager: dcscontentpm
ms.prod: ''
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 11c52b3beca3afcc0a6bfc8cecee2143dce0f023
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265832"
---
# <a name="troubleshooting-domain-name-system-dns-issues"></a>Problembehandlung bei Problemen mit Domain Name System (DNS)
 
Probleme mit der Domänen Namensauflösung können in Client seitige und serverseitige Probleme aufgeteilt werden. Im Allgemeinen sollten Sie mit der Client seitigen Problembehandlung beginnen, es sei denn, Sie legen während der Bereichs Phase fest, dass das Problem definitiv auf der Serverseite auftritt.

- [Problembehandlung bei DNS-Clients](troubleshoot-dns-client.md)

- [DNS-Server](troubleshoot-dns-server.md)
 
## <a name="data-collection"></a>Datensammlung
 
Es wird empfohlen, dass Sie Daten gleichzeitig auf den Client-und Server Seiten sammeln, wenn das Problem auftritt. Je nach tatsächlichem Problem können Sie die Sammlung jedoch mit einem einzelnen Dataset auf dem DNS-Client oder DNS-Server starten.
 
Führen Sie die folgenden Schritte aus, um eine Windows-Netzwerk Diagnose von einem betroffenen Client und seinem konfigurierten DNS-Server zu erfassen:

1. Starten Sie Netzwerk Erfassungen auf dem Client und dem Server:

   ```cmd
   netsh trace start capture=yes tracefile=c:\%computername%_nettrace.etl
   ```

2. Löschen Sie den DNS-Cache auf dem DNS-Client, indem Sie den folgenden Befehl ausführen:

   ```cmd
   ipconfig /flushdns
   ```

3. Reproduzieren Sie das Problem.

4. Abbrechen und Speichern von Ablauf Verfolgungen:

   ```cmd
   netsh trace stop
   ```

5. Speichern Sie die NetTrace. CAB-Dateien auf den einzelnen Computern. Diese Informationen sind hilfreich, wenn Sie sich mit Microsoft-Support in Verbindung setzen.