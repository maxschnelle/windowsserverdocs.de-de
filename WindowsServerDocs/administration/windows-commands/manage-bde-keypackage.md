---
title: manage-bde KeyPackage
description: Referenz Thema für den Befehl "manage-bde KeyPackage", mit dem ein Schlüssel Paket für ein Laufwerk generiert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4d0956154d6b20d5ceedb44d0781614f8da5fb1
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222887"
---
# <a name="manage-bde-keypackage"></a>manage-bde KeyPackage

Generiert ein Schlüssel Paket für ein Laufwerk. Das Schlüssel Paket kann zusammen mit dem Repair-Tool verwendet werden, um beschädigte Laufwerke zu reparieren.

## <a name="syntax"></a>Syntax

```
manage-bde -keypackage [<drive>] [-ID <keyprotectoryID>] [-path <pathtoexternalkeydirectory>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -ID | Erstellt ein Schlüssel Paket mithilfe der Schlüssel Schutzvorrichtung mit dem Bezeichner, der durch diesen ID-Wert angegeben wird. **Tipp:** Verwenden Sie den Befehl **manage-bde – Protector – Get** zusammen mit dem Laufwerk Buchstaben, für den Sie ein Schlüssel Paket erstellen möchten, um eine Liste der verfügbaren GUIDs abzurufen, die als ID-Wert verwendet werden sollen. |
| -path | Gibt den Speicherort an, an dem das erstellte Schlüssel Paket gespeichert wird. |
| -Computername | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Erstellen eines Schlüssel Pakets für Laufwerk C, basierend auf der durch die GUID identifizierten Schlüssel Schutzvorrichtung und zum Speichern des Schlüssel Pakets in "f:\folder", geben Sie Folgendes ein:

```
manage-bde -keypackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
