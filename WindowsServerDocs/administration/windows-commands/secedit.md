---
title: secedit-Befehle
description: Referenz Artikel zu den secedit-Befehlen, die ihre aktuellen Sicherheits Konfigurationen mit angegebenen Sicherheits Vorlagen vergleichen.
ms.topic: reference
ms.assetid: 58ed57ed-08e3-403d-a363-0620b358637a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ceb1a28376c17ab9d08689c7b0367dd90fdecc4f
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388287"
---
# <a name="secedit-commands"></a>secedit-Befehle

Konfiguriert und analysiert die Systemsicherheit durch Vergleichen Ihrer aktuellen Sicherheitskonfiguration mit angegebenen Sicherheits Vorlagen.

> [!NOTE]
> Die Microsoft Management Console (MMC) und das Snap-in "Sicherheitskonfiguration und-Analyse" sind auf Server Core nicht verfügbar.

## <a name="syntax"></a>Syntax

```
secedit /analyze
secedit /configure
secedit /export
secedit /generaterollback
secedit /import
secedit /validate
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [secedit/analyze](secedit-analyze.md) | Ermöglicht es Ihnen, die aktuellen Systemeinstellungen anhand von baselineeinstellungen zu analysieren, die in einer Datenbank gespeichert sind.  Die Analyseergebnisse werden in einem separaten Bereich der Datenbank gespeichert und können im Snap-in "Sicherheitskonfiguration und-Analyse" angezeigt werden. |
| [secedit/configure](secedit-configure.md) | Ermöglicht das Konfigurieren eines Systems mit Sicherheitseinstellungen, die in einer-Datenbank gespeichert sind. |
| [secedit/Export](secedit-export.md) | Ermöglicht das Exportieren von Sicherheitseinstellungen, die in einer-Datenbank gespeichert sind. |
| [secedit/generaterollback](secedit-generaterollback.md) | Ermöglicht das Generieren einer Rollback-Vorlage in Bezug auf eine Konfigurations Vorlage. |
| [secedit/Import](secedit-import.md) | Ermöglicht es Ihnen, eine Sicherheits Vorlage in eine-Datenbank zu importieren, damit die in der Vorlage angegebenen Einstellungen auf ein System angewendet oder anhand eines Systems analysiert werden können. |
| [secedit/Validate](secedit-validate.md) | Ermöglicht es Ihnen, die Syntax einer Sicherheits Vorlage zu validieren. |

#### <a name="remarks"></a>Hinweise

- Wenn kein filePath angegeben ist, werden alle Dateinamen standardmäßig auf das aktuelle Verzeichnis festgelegt.

- Die Analyseergebnisse werden in einem separaten Bereich der Datenbank gespeichert und können im Snap-in "Sicherheitskonfiguration und-Analyse" der MMC angezeigt werden.

- Wenn Ihre Sicherheits Vorlagen mit dem Snap-in "Sicherheits Vorlage" erstellt werden und Sie das Snap-in "Sicherheitskonfiguration und-Analyse" für diese Vorlagen ausführen, werden die folgenden Dateien erstellt:

    | Datei | BESCHREIBUNG |
    |--|--|
    | Scesrv. log | <ul><li>**Speicherort:**`%windir%\security\logs`</li><li>**Erstellt von:** Betriebssystem</li><li>**Dateityp:** Text</li><li>**Aktualisierungsrate:** Überschrieben `secedit analyze` , wenn, `secedit configure` `secedit export` oder `secedit import` ausgeführt wird.</li><li>**Inhalt:** Enthält die Ergebnisse der Analyse nach Richtlinientyp gruppiert.</li></ul> |
    | vom *Benutzer ausgewählter Name*. SDB | <ul><li>**Speicherort:**`%windir%\<user account>\Documents\Security\Database`</li><li>**Erstellt von:** Ausführen des Sicherheitskonfigurations-und Analyse-Snap-Ins</li><li>**Dateityp:** Tä</li><li>**Aktualisierungsrate:** Wird immer dann aktualisiert, wenn eine neue Sicherheits Vorlage erstellt wird.</li><li>**Inhalt:** Lokale Sicherheitsrichtlinien und vom Benutzer erstellte Sicherheits Vorlagen.</li></ul> |
    | vom *Benutzer ausgewählter Name*. log | <ul><li>**Speicherort:** Benutzer definiert, aber standardmäßig `%windir%\<user account>\Documents\Security\Logs`</li><li>**Erstellt von:** Ausführen der `secedit analyze` `secedit configure` Befehle oder oder mithilfe des Snap-Ins Sicherheitskonfiguration und-Analyse.</li><li>**Dateityp:** Text</li><li>**Aktualisierungsrate:** Überschrieben `secedit analyze` , wenn oder `secedit configure` ausgeführt wird, oder mithilfe des Sicherheitskonfigurations-und Analyse-Snap-Ins.</li><li>**Inhalt:** Protokoll Dateiname, Datum und Uhrzeit sowie die Ergebnisse der Analyse oder Untersuchung.</li></ul> |
    | vom *Benutzer ausgewählter Name*. inf | <ul><li>**Speicherort:**`%windir%\*<user account>\Documents\Security\Templates`</li><li>**Erstellt von:** Ausführen des Snap-Ins "Sicherheits Vorlage"</li><li>**Dateityp:** Text</li><li>**Aktualisierungsrate:** Wird jedes Mal überschrieben, wenn die Sicherheits Vorlage aktualisiert wird.</li><li>**Inhalt:** Enthält die Informationen zur Einrichtung für die Vorlage für jede Richtlinie, die mithilfe des-Snap-Ins ausgewählt wird.</li></ul> |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
