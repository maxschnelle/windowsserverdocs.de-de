---
title: nfsstat
description: Referenz Thema für den nfsstat-Befehl, in dem statistische Informationen zu den Aufrufen von Network File System (NFS) und Remote Prozedur Aufruf (RPC) angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85eb1184d3eb8ee731cf698a6d805e3f11d878ce
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721513"
---
# <a name="nfsstat"></a>nfsstat

Ein Befehlszeilen-Hilfsprogramm, das statistische Informationen zu den Aufrufen von Network File System (NFS) und Remote Procedure Calls (RPC) anzeigt. Wird ohne Parameter verwendet, werden mit diesem Befehl alle statistischen Daten angezeigt, ohne dass etwas zurückgesetzt wird.

## <a name="syntax"></a>Syntax

```
nfsstat [-c][-s][-n][-r][-z][-m]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -c | Zeigt nur die vom Client gesendeten und abgelehnten Client seitigen NFS-und RPC-und NFS-Aufrufe an. Um nur NFS-oder RPC-Informationen anzuzeigen, kombinieren Sie dieses Flag mit dem Parameter **-n** oder **-r** . |
| -S | Zeigt nur die serverseitigen NFS-und RPC-und NFS-Aufrufe an, die vom Server gesendet und abgelehnt wurden. Um nur NFS-oder RPC-Informationen anzuzeigen, kombinieren Sie dieses Flag mit dem Parameter **-n** oder **-r** . |
| -M | Zeigt Informationen zu einstellungsflags an, die durch Einstellungsoptionen festgelegt sind, interne einstellungsflags und andere Bereitstellungs Informationen. |
| -n | Zeigt NFS-Informationen für den Client und den Server an. Um nur die NFS-Client-oder Server Informationen anzuzeigen, kombinieren Sie dieses Flag mit dem Parameter **-c** oder **-s** . |
| -r | Zeigt RPC-Informationen sowohl für den Client als auch für den Server an. Um nur die RPC-Client-oder-Server Informationen anzuzeigen, kombinieren Sie dieses Flag mit dem Parameter **-c** oder **-s** . |
| -Z | Setzt die Rückruf Statistik zurück. Dieses Flag ist nur für den root-Benutzer verfügbar und kann mit einem der anderen Parameter kombiniert werden, um bestimmte Statistik Sätze nach dem anzeigen zurückzusetzen. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zur Anzahl der vom Client gesendeten und abgelehnten RPC-und NFS-Aufrufe anzuzeigen:

```
nfsstat -c
```

Geben Sie Folgendes ein, um die Informationen zum Client-NFS-aufrufen anzuzeigen und zu drucken:

```
nfsstat -cn
```

Geben Sie Folgendes ein, um Informationen zum RPC-Aufruf sowohl für den Client als auch für den Server anzuzeigen:

```
nfsstat -r
```

Geben Sie Folgendes ein, um Informationen zur Anzahl der vom Server empfangenen und abgelehnten RPC-und NFS-Aufrufe anzuzeigen:

```
nfsstat -s
```

Geben Sie Folgendes ein, um alle aufrufbezogenen Informationen auf dem Client und auf dem Server auf NULL zurückzusetzen:

```
nfsstat -z
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md)

- [Referenz zu NFS-Cmdlets](https://docs.microsoft.com/powershell/module/nfs)
