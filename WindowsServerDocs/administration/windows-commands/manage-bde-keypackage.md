---
title: manage-bde KeyPackage
description: Referenz Artikel zum Befehl "manage-bde KeyPackage", mit dem ein Schlüssel Paket für ein Laufwerk generiert wird.
ms.topic: reference
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b183c06dfa73d20f7dc3236b88d5346a8694ec61
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639310"
---
# <a name="manage-bde-keypackage"></a>manage-bde KeyPackage

Generiert ein Schlüssel Paket für ein Laufwerk. Das Schlüssel Paket kann zusammen mit dem Repair-Tool verwendet werden, um beschädigte Laufwerke zu reparieren.

## <a name="syntax"></a>Syntax

```
manage-bde -keypackage [<drive>] [-ID <keyprotectoryID>] [-path <pathtoexternalkeydirectory>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -ID | Erstellt ein Schlüssel Paket mithilfe der Schlüssel Schutzvorrichtung mit dem Bezeichner, der durch diesen ID-Wert angegeben wird. **Tipp:** Verwenden Sie den Befehl **manage-bde – Protector – Get** zusammen mit dem Laufwerk Buchstaben, für den Sie ein Schlüssel Paket erstellen möchten, um eine Liste der verfügbaren GUIDs abzurufen, die als ID-Wert verwendet werden sollen. |
| -path | Gibt den Speicherort an, an dem das erstellte Schlüssel Paket gespeichert wird. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Erstellen eines Schlüssel Pakets für Laufwerk C, basierend auf der durch die GUID identifizierten Schlüssel Schutzvorrichtung und zum Speichern des Schlüssel Pakets in "f:\folder", geben Sie Folgendes ein:

```
manage-bde -keypackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
