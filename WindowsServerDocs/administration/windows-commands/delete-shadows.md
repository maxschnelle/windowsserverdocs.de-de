---
title: Schatten löschen
description: Windows-Befehls Artikel zum Löschen von Schatten Kopien.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd109f7ddc0365d03737eddba31a1a4b7f34915b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846563"
---
# <a name="delete-shadows"></a>Schatten löschen

Löscht Schatten Kopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---- | ---- |
| all | Löscht alle Schatten Kopien. |
| Volume \<Volume > | Löscht alle Schatten Kopien des angegebenen Volumes. |
| ältestes \<Volume > | Löscht die älteste Schatten Kopie des angegebenen Volumes. |
| Legen Sie \<setID fest > | Löscht die Schatten Kopien im Schattenkopiesatz der angegebenen ID. Sie können einen Alias angeben, indem Sie das **%** Symbol verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| ID \<shadowid > | Löscht eine Schatten Kopie der angegebenen ID. Sie können einen Alias angeben, indem Sie das **%** Symbol verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| {\<Laufwerk > verfügbar gemacht | <MountPoint>} |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)