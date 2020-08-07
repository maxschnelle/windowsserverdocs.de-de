---
title: Break (Schattenkopievolume)
description: Referenz Artikel für den Break-Befehl, bei dem ein Schattenkopievolume von VSS getrennt und als reguläres Volume zugänglich gemacht wird.
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 125f986152d10844bbab5a7b57a1a2ea4080aa3e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880459"
---
# <a name="break-shadow-copy-volume"></a>Break (Schattenkopievolume)

Trennt ein Schattenkopievolume von VSS und ermöglicht es als reguläres Volume. Auf das Volume kann dann mithilfe eines Laufwerk Buchstabens (sofern zugewiesen) oder eines Volumenamens zugegriffen werden. Bei Verwendung ohne Parameter zeigt **break** die Hilfe an der Eingabeaufforderung an.

> [!NOTE]
> Dieser Befehl ist nur für Hardware Schatten Kopien nach dem Import relevant.
>
> Verfügbar gemachte Volumes, wie die Schatten Kopien, von denen Sie stammen, sind standardmäßig schreibgeschützt. Der Zugriff auf das Volume erfolgt direkt an den Hardware Anbieter, ohne dass das Volume eine Schatten Kopie aufweist.

## <a name="syntax"></a>Syntax

```
break [writable] <setid>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| beschreibbaren | Aktiviert den Lese-/Schreibzugriff auf dem Volume. |
| \<setid> | Gibt die ID des schattenkopiessets an. Der Alias der Schattenkopiekennung, der durch den Befehl " **Metadaten laden** " als Umgebungsvariable gespeichert wird, kann *im Parameter "* Parameter" verwendet werden. |

## <a name="examples"></a>Beispiele

So erstellen Sie eine Schatten Kopie mithilfe des Alias namens Alias1 zugänglich als beschreibbares Volume im Betriebssystem:

```
break writable %Alias1%
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)