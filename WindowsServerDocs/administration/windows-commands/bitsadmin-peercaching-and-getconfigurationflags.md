---
title: bitadmin-Peer Caching und getconfigurationflags
description: Windows-Befehls Thema für **BITSAdmin-Peer Caching** und **getconfigurationflags**, die die Konfigurationsflags abrufen, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: be8d6a719d63c8e9c6250320560b6ce21274c680
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850173"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitadmin-Peer Caching und getconfigurationflags

Ruft die Konfigurationsflags ab, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Konfigurationsflags für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\> bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)