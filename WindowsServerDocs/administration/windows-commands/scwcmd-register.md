---
title: scwcmd register
description: Referenz Artikel für den Befehl scwcmd Register, der die Sicherheits Konfigurations Datenbank des Sicherheitskonfigurations-Assistenten (Security Configuration Wizard, SCW) erweitert oder anpasst, indem eine Sicherheits Konfigurations-Datenbankdatei registriert wird, die Rollen-, Task-, Dienst-oder Port Definitionen enthält.
ms.topic: reference
ms.assetid: fe4d126a-9f27-4076-b7b1-fbefa45f378a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b1e981ef2a428174406fd793d5c959de57a8067c
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388576"
---
# <a name="scwcmd-register"></a>scwcmd register

> Gilt für: Windows Server 2012 R2 und Windows Server 2012

Erweitert oder passt die Sicherheitskonfigurations-Assistent (Security Configuration Wizard, SCW) Sicherheits Konfigurations Datenbank an, indem eine Sicherheits Konfigurations-Datenbankdatei registriert wird, die Rollen-, Task-, Dienst-oder Port Definitionen enthält

## <a name="syntax"></a>Syntax

```
scwcmd register /kbname:<MyApp> [/kbfile:<kb.xml>] [/kb:<path>] [/d]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /kbname:`<MyApp>` | Gibt den Namen an, unter dem die Sicherheitskonfigurations-Daten Bank Erweiterung registriert wird. Dieser Parameter muss angegeben werden. |
| /kbfile:`<kb.xml>` | Gibt den Pfad und den Dateinamen der Sicherheitskonfigurations-Datenbankdatei an, die zum Erweitern oder Anpassen der Datenbank der Basis Sicherheitskonfiguration verwendet wird. Um zu überprüfen, ob die Sicherheits Konfigurations-Datenbankdatei mit dem SCW-Schema kompatibel ist, verwenden Sie die `%windir%\security\KBRegistrationInfo.xsd` Schema Definitionsdatei. Diese Option muss angegeben werden, es sei denn, der **/d** -Parameter wird angegeben. |
| verarbeiten`<path>` | Gibt den Pfad zu dem Verzeichnis an, das die zu aktualisierenden SCW-Sicherheits Konfigurations-Datenbankdateien enthält. Wenn diese Option nicht angegeben ist, `%windir%\security\msscw\kbs` wird verwendet. |
| /d | Hebt die Registrierung einer Sicherheitskonfigurations-Daten Bank Erweiterung aus der Sicherheitskonfigurations-Datenbank auf. Die Erweiterung, deren Registrierung aufgehoben werden soll, wird durch den **/kbname** -Parameter angegeben. (Der **/kbfile** -Parameter sollte nicht angegeben werden.) Die Sicherheits Konfigurations Datenbank, von der die Registrierung der Erweiterung aufgehoben werden soll, wird durch den **/KB** -Parameter angegeben. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Sicherheits Konfigurations-Datenbankdatei namens *SCWKBForMyApp.xml* unter dem Namen " *myapp* " am Speicherort zu registrieren `\\kbserver\kb` :

```
scwcmd register /kbfile:d:\SCWKBForMyApp.xml /kbname:MyApp /kb:\\kbserver\kb
```

Geben Sie Folgendes ein, um die Registrierung der Sicherheitskonfigurations-Datenbank " *myapp*" unter zu deaktivieren `\\kbserver\kb` :

```
scwcmd register /d /kbname:MyApp /kb:\\kbserver\kb
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [scwcmd-Analyse Befehl](scwcmd-analyze.md)

- [scwcmd-Befehl "configure"](scwcmd-configure.md)

- [scwcmd-rollback-Befehl](scwcmd-rollback.md)

- [Befehl "Scwcmd Transform"](scwcmd-transform.md)

- [scwcmd-Ansichts Befehl](scwcmd-view.md)