---
title: reg-Befehle
description: Referenz Artikel zu den reg-Befehlen, mit denen Vorgänge für Registrierungs Unterschlüssel Informationen und Werte in Registrierungs Einträgen durchgeführt werden.
ms.topic: reference
ms.assetid: c97496b2-d1ff-4887-b5d2-6e1524be465a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 619f6ae1d03197754145d0daad029deb817efffe
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388836"
---
# <a name="reg-commands"></a>reg-Befehle

Führt Vorgänge für Registrierungs Unterschlüssel Informationen und Werte in Registrierungs Einträgen aus.

Einige Vorgänge ermöglichen es Ihnen, Registrierungseinträge auf lokalen Computern oder Remote Computern anzuzeigen oder zu konfigurieren. andere ermöglichen es Ihnen, nur lokale Computer zu konfigurieren. Die Verwendung von **reg** zum Konfigurieren der Registrierung von Remote Computern schränkt die Parameter ein, die Sie in einigen Vorgängen verwenden können. Überprüfen Sie die Syntax und die Parameter für jeden Vorgang, um sicherzustellen, dass Sie auf Remote Computern verwendet werden können.

> [!CAUTION]
> Bearbeiten Sie die Registrierung nur dann direkt, wenn Sie keine Alternative haben. Der Registrierungs-Editor umgeht Standard-Sicherheitsvorkehrungen und ermöglicht Einstellungen, die die Leistung beeinträchtigen, das System beschädigen oder sogar die Neuinstallation von Windows erfordern. Sie können die meisten Registrierungs Einstellungen sicher ändern, indem Sie die Programme in der Systemsteuerung oder Microsoft Management Console (MMC) verwenden. Wenn Sie die Registrierung direkt bearbeiten müssen, sichern Sie Sie zuerst.

## <a name="syntax"></a>Syntax

```
reg add
reg compare
reg copy
reg delete
reg export
reg import
reg load
reg query
reg restore
reg save
reg unload
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [reg add](reg-add.md) | Fügt der Registrierung einen neuen Unterschlüssel oder Eintrag hinzu. |
| [reg compare](reg-compare.md) | Vergleicht die angegebenen Registrierungs Unterschlüssel oder-Einträge. |
| [reg copy](reg-copy.md) | Kopiert einen Registrierungs Eintrag an einen angegebenen Speicherort auf dem lokalen Computer oder auf dem Remote Computer. |
| [reg delete](reg-delete.md) | Löscht einen Unterschlüssel oder Einträge aus der Registrierung. |
| [reg export](reg-export.md) | Kopiert die angegebenen Unterschlüssel, Einträge und Werte des lokalen Computers in eine Datei für die Übertragung an andere Server. |
| [reg import](reg-import.md) | Kopiert den Inhalt einer Datei, die exportierte Registrierungs Unterschlüssel, Einträge und Werte enthält, in die Registrierung des lokalen Computers. |
| [reg load](reg-load.md) | Schreibt gespeicherte Unterschlüssel und Einträge in einen anderen Unterschlüssel in der Registrierung. |
| [reg query](reg-query.md) | Gibt eine Liste der nächsten Ebene von unter Schlüsseln und Einträgen zurück, die sich unter einem angegebenen Unterschlüssel in der Registrierung befinden. |
| [reg restore](reg-restore.md) | Schreibt gespeicherte Unterschlüssel und Einträge zurück in die Registrierung. |
| [reg save](reg-save.md) | Speichert eine Kopie der angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei. |
| [reg unload](reg-unload.md) | Entfernt einen Abschnitt der Registrierung, der mit dem reg- **Lade** Vorgang geladen wurde. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
