---
title: Break (Schattenkopievolume)
description: Referenz Artikel für den Break-Befehl, bei dem ein Schattenkopievolume von VSS getrennt und als reguläres Volume zugänglich gemacht wird.
ms.topic: reference
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fa698a91ec7ddcabba7bcaaa6a80dac0831312af
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630033"
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