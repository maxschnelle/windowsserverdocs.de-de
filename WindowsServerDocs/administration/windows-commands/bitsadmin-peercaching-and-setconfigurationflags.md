---
title: bitadmin-Peer Caching und setconfigurationflags
description: Windows-Befehls Thema für **BITSAdmin-Peer Caching** und **setconfigurationflags**, mit dem die Konfigurationsflags festgelegt werden, die bestimmen, ob der Computer Inhalte für Peers bereitstellen kann und ob Inhalt von Peers heruntergeladen werden kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebaa09da2d4594d2762e67dc5884dd15cf4d1da8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850133"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitadmin-Peer Caching und setconfigurationflags

Legt die Konfigurationsflags fest, die bestimmen, ob der Computer Inhalte für Peers bereitstellen kann und ob Inhalt von Peers heruntergeladen werden kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| Wert | Eine ganze Zahl ohne Vorzeichen mit der folgenden Interpretation für die Bits in der binären Darstellung:<ul><li> Legen Sie das unwichtigste Bit fest, damit die Daten des Auftrags von einem Peer heruntergeladen werden können.</li><li>Um zuzulassen, dass die Auftragsdaten für Peers bereitgestellt werden, legen Sie das zweite Bit von der rechten Seite fest.</li></ul>|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Daten des Auftrags angegeben, die von Peers für den Auftrag mit dem Namen *mydownloadjob*heruntergeladen werden sollen.

```
C:\> bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)