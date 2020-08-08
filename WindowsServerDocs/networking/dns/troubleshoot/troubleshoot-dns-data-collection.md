---
title: Problembehandlung bei Problemen mit Domain Name System (DNS)
description: In diesem Artikel wird erläutert, wie Sie Daten sammeln, wenn DNS-Probleme auftreten.
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: f56c3b7004392f06e0e0728e6e82851ae015640d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954066"
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

5. Speichern Sie die Nettrace.cab Dateien auf den einzelnen Computern. Diese Informationen sind hilfreich, wenn Sie sich mit Microsoft-Support in Verbindung setzen.