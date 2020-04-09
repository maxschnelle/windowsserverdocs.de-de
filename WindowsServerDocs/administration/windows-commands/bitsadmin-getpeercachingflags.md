---
title: bitadmin getPeer Cache-Flags
description: Windows-Befehls Thema für **BITSAdmin getpeercachingflags**, das Flags abruft, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cdf9683d1a65400286b4604bd9420a5ab863d4af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850553"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitadmin getPeer Cache-Flags

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Flags ab, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /getpeercachingflags <job> 
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Flags für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getpeercachingflags myJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)