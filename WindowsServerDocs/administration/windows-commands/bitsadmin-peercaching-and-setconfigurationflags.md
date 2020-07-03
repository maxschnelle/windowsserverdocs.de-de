---
title: bitsadmin peercaching and setconfigurationflags
description: Referenz Artikel zum Befehl BITSAdmin-Peer Caching und setconfigurationflags, mit dem die Konfigurationsflags festgelegt werden, mit denen festgelegt wird, ob der Computer Inhalte an Peers bereitstellen und Inhalt von Peers herunterladen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 868ef39104f1d16c760d91eee401c0d48b27ea1f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928126"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin peercaching and setconfigurationflags

Legt die Konfigurationsflags fest, die bestimmen, ob der Computer Inhalte für Peers bereitstellen kann und ob Inhalt von Peers heruntergeladen werden kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| value | Eine ganze Zahl ohne Vorzeichen mit der folgenden Interpretation für die Bits in der binären Darstellung:<ul><li>Legen Sie das unwichtigste Bit fest, damit die Daten des Auftrags von einem Peer heruntergeladen werden können.</li><li>Um zuzulassen, dass die Auftragsdaten für Peers bereitgestellt werden, legen Sie das zweite Bit von der rechten Seite fest.</li></ul>|

## <a name="examples"></a>Beispiele

So geben Sie die Daten des Auftrags an, die für den Auftrag *mydownloadjob*von Peers heruntergeladen werden sollen:

```
bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)

- [bipadmin-Befehl "Peer Caching"](bitsadmin-peercaching.md)
