---
title: bitsadmin peercaching and setconfigurationflags
description: Referenz Thema für den Befehl BITSAdmin-Peer Caching und setconfigurationflags, mit dem die Konfigurationsflags festgelegt werden, die bestimmen, ob der Computer Inhalte an Peers bereitstellen kann und ob Inhalt von Peers heruntergeladen werden kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c3ce69ce7a372311ce0c30e9b3a391ea33f45ce
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717235"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin peercaching and setconfigurationflags

Legt die Konfigurationsflags fest, die bestimmen, ob der Computer Inhalte für Peers bereitstellen kann und ob Inhalt von Peers heruntergeladen werden kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| value | Eine ganze Zahl ohne Vorzeichen mit der folgenden Interpretation für die Bits in der binären Darstellung:<ul><li>Legen Sie das unwichtigste Bit fest, damit die Daten des Auftrags von einem Peer heruntergeladen werden können.</li><li>Um zuzulassen, dass die Auftragsdaten für Peers bereitgestellt werden, legen Sie das zweite Bit von der rechten Seite fest.</li></ul>|

## <a name="examples"></a>Beispiele

So geben Sie die Daten des Auftrags an, die für den Auftrag *mydownloadjob*von Peers heruntergeladen werden sollen:

```
bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)

- [bipadmin-Befehl "Peer Caching"](bitsadmin-peercaching.md)
