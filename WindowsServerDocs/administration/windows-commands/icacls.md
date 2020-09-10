---
title: icacls
description: Referenz Artikel für den Befehl icacls, der freigegebene Zugriffs Steuerungs Listen (DACL) für angegebene Dateien anzeigt oder ändert und gespeicherte DACLs auf Dateien in angegebenen Verzeichnissen anwendet.
ms.topic: reference
ms.assetid: 403edfcc-328a-479d-b641-80c290ccf73e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 08/21/2018
ms.openlocfilehash: 82c24b529aaaf364b4a1e67e853c464e21bfd349
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634581"
---
# <a name="icacls"></a>icacls

Zeigt oder ändert DACLs (Discretionary Access Control Lists) für bestimmte Dateien an, und wendet gespeicherte DACLs auf Dateien in angegebenen Verzeichnissen an.

> [!NOTE]
> Dieser Befehl ersetzt den veralteten [cacls-Befehl](cacls.md).

## <a name="syntax"></a>Syntax

```
icacls <filename> [/grant[:r] <sid>:<perm>[...]] [/deny <sid>:<perm>[...]] [/remove[:g|:d]] <sid>[...]] [/t] [/c] [/l] [/q] [/setintegritylevel <Level>:<policy>[...]]
icacls <directory> [/substitute <sidold> <sidnew> [...]] [/restore <aclfile> [/c] [/l] [/q]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<filename>` | Gibt die Datei an, für die DACLs angezeigt werden sollen. |
| `<directory>` | Gibt das Verzeichnis an, für das DACLs angezeigt werden sollen. |
| /t | Führt den Vorgang für alle angegebenen Dateien im aktuellen Verzeichnis und seinen Unterverzeichnissen aus. |
| /C | Der Vorgang wird trotz aller Datei Fehler fortgesetzt. Fehlermeldungen werden weiterhin angezeigt. |
| /l | Führt den Vorgang für einen symbolischen Link anstelle seines Ziels aus. |
| /q | Unterdrückt Erfolgsmeldungen. |
| [/Save `<ACLfile>` /t /c /l [/q]] | Speichert DACLs für alle übereinstimmenden Dateien in *aclfile* für die spätere Verwendung mit **/Restore**. |
| [/SetOwner `<username>` /t /c /l [/q]] | Ändert den Besitzer aller übereinstimmenden Dateien für den angegebenen Benutzer. |
| [/findsid `<sid>` /t /c /l [/q]] | Sucht alle übereinstimmenden Dateien, die eine DACL enthalten, die explizit die angegebene Sicherheits-ID (SID) erwähnt. |
| [/verify [/t] [/c] [/l] [/q]] | Findet alle Dateien mit ACLs, die nicht kanonisch sind oder Längen inkonsistent mit ACE (Access Control Entry)-Anzahlen aufweisen. |
| [/Reset [/t] [/c] [/l] [/q]] | Ersetzt ACLs durch geerbte Standard-ACLs für alle übereinstimmenden Dateien. |
| [/Grant [: r] \<sid> : <perm> [...]] | Erteilt angegebene Benutzer Zugriffsrechte. Berechtigungen ersetzen zuvor erteilte explizite Berechtigungen.<p>Wird nicht hinzu **gefügt, bedeutet dies, dass**Berechtigungen allen zuvor erteilten expliziten Berechtigungen hinzugefügt werden. |
| [/deny \<sid> : <perm> [...]] | Verweigert explizit angegebene Benutzer Zugriffsrechte. Für die angegebenen Berechtigungen wird ein expliziter Verweigerungs-ACE hinzugefügt, und die gleichen Berechtigungen in expliziten Berechtigungen werden entfernt. |
| [/Remove `[:g | :d]]` `<sid>` [...] /t /c /l /q | Entfernt alle Vorkommen der angegebenen SID aus der DACL. Dieser Befehl kann auch Folgendes verwenden:<ul><li>**: g** -entfernt alle Vorkommen der gewährten Rechte für die angegebene SID.</li><li>**:d** : entfernt alle Vorkommen abgelehnter Rechte für die angegebene SID. |
| [/setintegritylevel [(CI) (OI)] `<Level>:<Policy>` [...]] | Fügt allen übereinstimmenden Dateien explizit einen Integritäts-ACE hinzu. Die Ebene kann wie folgt angegeben werden:<ul><li>**l** -niedrig</li><li>**m**-Mittel</li><li>**h** -hoch</li></ul>Vererbungs Optionen für den Integritäts-ACE können der Ebene vorangestellt werden und werden nur auf Verzeichnisse angewendet. |
| [/Substitute `<sidold> <sidnew>` [...]] | Ersetzt eine vorhandene sid (*sidold*) durch eine neue sid (*sidnew*). Erfordert die Verwendung von mit dem- `<directory>` Parameter. |
| /Restore `<ACLfile>` [/c] [/l] [/q] | Wendet gespeicherte DACLs von `<ACLfile>` auf Dateien im angegebenen Verzeichnis an. Erfordert die Verwendung von mit dem- `<directory>` Parameter. |
| /inheritancelevel:`[e | d | r]` | Legt die Vererbungs Ebene fest. Dies kann wie folgt lauten:<ul><li>**e** -aktiviert Vererbung</li><li>**d** : Deaktivieren der Vererbung und Kopieren der ACEs</li><li>**r** -entfernt alle geerbten ACEs</li></ul> |

## <a name="remarks"></a>Hinweise

- SIDs können entweder in Form eines numerischen oder eines anzeigen Amens vorliegen. Wenn Sie ein numerisches Format verwenden, können Sie das Platzhalter Zeichen **&#42;** an den Anfang der SID anbinden.

- Dieser Befehl behält die kanonische Reihenfolge der ACE-Einträge wie folgt bei:

    - Explizite Verweigerungen

    -  Explizite Zuweisungen

    - Geerbte Verweigerungen

    - Geerbte Zuweisungen

- `<perm>`Bei der Option handelt es sich um eine Berechtigungs Maske, die in einer der folgenden Formen angegeben werden kann:

    - Eine Sequenz von einfachen rechten:

      - **F** -Vollzugriff

      - **M**-Zugriff ändern

      - **RX** -Lese-und Ausführungs Zugriff

      - **R** -Schreib geschützter Zugriff

      - **W** -Schreib geschützter Zugriff

    - Eine durch Trennzeichen getrennte Liste in Klammern spezifischer Rechte:

      - **D** -löschen

      - **RC** -Steuerelement lesen

      - **WDac** -Schreiben von DAC

      - **-** /Schreibbesitzer

      - **S** -synchronisieren

      - Systemsicherheit **als** Zugriff

      - **MA** -maximal zulässig

      - **Gr** -generischer Lesevorgang

      - **GW** -generischer Schreibvorgang

      - **Ge** -generische Ausführung

      - **GA** Allgemeine allgemeine Verfügbarkeit

      - **RD** -Lesedaten/Listen Verzeichnis

      - **WD** -Daten schreiben/Datei hinzufügen

      - **AD** -Daten anfügen/Unterverzeichnis hinzufügen

      - **REA** -Erweiterte Attribute lesen

      - **WEA** : Erweiterte Attribute schreiben

      - **X** -Execute/Traversieren

      - **DC** -untergeordnetes Element löschen

      - **RA** -Attribute lesen

      - **WA** -Attribute schreiben

  - Vererbungs Rechte können einer der beiden `<perm>` Formulare vorangestellt werden, und Sie werden nur auf Verzeichnisse angewendet:

      - **(OI)** -Objekt erben

      - **(CI)** -Container erben

      - **(IO)** -nur Erben

      - **(NP)** -nicht erben propagieren

## <a name="examples"></a>Beispiele

Wenn Sie die DACLs für alle Dateien im Verzeichnis "c:\Windows" und deren Unterverzeichnisse in der aclfile-Datei speichern möchten, geben Sie Folgendes ein:

```
icacls c:\windows\* /save aclfile /t
```

Geben Sie Folgendes ein, um die DACLs für jede Datei in aclfile wiederherzustellen, die im Verzeichnis "c:\Windows" und in den zugehörigen Unterverzeichnissen vorhanden ist:

```
icacls c:\windows\ /restore aclfile
```

Geben Sie Folgendes ein, um dem Benutzer user1 Berechtigungen zum Löschen und Schreiben von DAC für eine Datei namens Test1 zu erteilen:

```
icacls test1 /grant User1:(d,wdac)
```

Geben Sie Folgendes ein, um dem Benutzer, der durch sid S-1-1-0 definiert ist, DAC-Berechtigungen für eine Datei mit dem Namen test2 zu erteilen:

```
icacls test2 /grant *S-1-1-0:(d,wdac)
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
