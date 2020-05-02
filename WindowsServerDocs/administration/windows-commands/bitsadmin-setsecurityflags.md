---
title: bitsadmin setsecurityflags
description: Referenz Thema für den BITSAdmin setsecurityflags-Befehl, mit dem sicherheitsflags für http festgelegt werden, um zu bestimmen, ob Bits die Zertifikat Sperr Liste überprüfen, bestimmte Zertifikat Fehler ignorieren und die Richtlinie definieren, die verwendet werden soll, wenn ein Server die HTTP-Anforderung umleitet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63430f9814037aeb948cc8b91e8590f13a4df00e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720469"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags

Legt sicherheitsflags für http fest, um zu bestimmen, ob Bits die Zertifikat Sperr Liste überprüfen, bestimmte Zertifikat Fehler ignorieren und die Richtlinie definieren soll, die verwendet werden soll, wenn ein Server die HTTP-Anforderung umleitet. Der Wert ist eine ganze Zahl ohne Vorzeichen.

## <a name="syntax"></a>Syntax

```
bitsadmin /setsecurityflags <job> <value>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| value | Kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten, einschließlich:<ul><li>Legen Sie das unwichtigste Bit zum Aktivieren der CRL-Überprüfung fest.</li><li>Legen Sie das zweite Bit von rechts fest, um falsche allgemeine Namen im Serverzertifikat zu ignorieren.</li><li>Legen Sie das dritte Bit von rechts fest, um falsche Datumsangaben im Serverzertifikat zu ignorieren.</li><li>Legen Sie das 4. Bit von rechts fest, um falsche Zertifizierungsstellen im Serverzertifikat zu ignorieren.</li><li>Legen Sie das 5. Bit von rechts fest, um die falsche Verwendung des Serverzertifikats zu ignorieren.</li><li>Legen Sie die 9. bis 11. Bits von rechts fest, um die angegebene Umleitungs Richtlinie zu implementieren, einschließlich:<ul><li>**0, 0, 0.** Umleitungen sind automatisch zulässig.</li><li>**0, 0, 1.** Der Remote Name in der **ibackgroundcopyfile** -Schnittstelle wird aktualisiert, wenn eine Umleitung erfolgt.</li><li>**0, 1, 0.** Bits schlägt den Auftrag fehl, wenn eine Umleitung erfolgt.</li></ul></li><li>Legen Sie das 12. Bit von rechts fest, um die Umleitung von HTTPS zu http zuzulassen.</li></ul> |

## <a name="examples"></a>Beispiele

So legen Sie die sicherheitsflags zum Aktivieren einer CRL-Prüfung für den Auftrag *mydownloadjob*fest:

```
bitsadmin /setsecurityflags myDownloadJob 0x0001
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
