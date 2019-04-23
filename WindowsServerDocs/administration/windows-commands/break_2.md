---
title: break
description: 'Windows-Befehle Thema **break_2** : Hebt die Zuordnung einer Schattenkopievolume von VSS und erleichtert die wie ein reguläres Volume zugegriffen werden kann.'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 49516539ae603e2c93b3fc395c77786be790d663
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886331"
---
# <a name="break"></a>break



Hebt die Zuordnung einer Schattenkopievolume von VSS und erleichtert die wie ein reguläres Volume zugegriffen werden kann. Das Volume kann dann mit einem Laufwerkbuchstaben (sofern zugewiesen) oder die Volumename zugegriffen werden. Wenn Sie ohne Angabe von Parametern **Break** zeigt die Hilfe an der Eingabeaufforderung.

> [!NOTE]
> Dieser Befehl gilt nur für Hardwareschattenkopien nach dem Import zur Verfügung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
break [writable] <SetID>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[beschreibbaren]|Ermöglicht Lese-/Schreibzugriff auf dem Volume.|
|\<SetID>|Gibt die ID des dem Schattenkopiesatz.|

## <a name="remarks"></a>Hinweise

-   Verfügbar gemachten Volumes, wie die Schattenkopien, die sie aus, stammen, sind standardmäßig schreibgeschützt.
-   Den Alias der Schattenkopie-ID, die als Umgebungsvariable gespeichert wird die **Laden von Metadaten** Befehl, der verwendet werden können, der *SetID* Parameter.

## <a name="BKMK_examples"></a>Beispiele für

Um einen Schatten, kopieren Sie mit der Aliasname Alias1 als schreibbare Volume im Betriebssystem zugänglich zu machen, geben Sie Folgendes ein:
```
break writable %Alias1%
```

> [!NOTE]
> Zugriff auf das Volume wird direkt an den Hardwareanbieter, ohne den Datensatz, der das Volume wurde eine Schattenkopie vorgenommen.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)