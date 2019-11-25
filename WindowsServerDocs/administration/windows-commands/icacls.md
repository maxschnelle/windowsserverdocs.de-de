---
title: icacls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 403edfcc-328a-479d-b641-80c290ccf73e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: 494c87073cfd78c7f5e17c72d4c65bec33a49b98
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375490"
---
# <a name="icacls"></a>icacls

Zeigt oder ändert DACLs (Discretionary Access Control Lists) für bestimmte Dateien an, und wendet gespeicherte DACLs auf Dateien in angegebenen Verzeichnissen an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
icacls <FileName> [/grant[:r] <Sid>:<Perm>[...]] [/deny <Sid>:<Perm>[...]] [/remove[:g|:d]] <Sid>[...]] [/t] [/c] [/l] [/q] [/setintegritylevel <Level>:<Policy>[...]]
icacls <Directory> [/substitute <SidOld> <SidNew> [...]] [/restore <ACLfile> [/c] [/l] [/q]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Dateiname >|Gibt die Datei an, für die DACLs angezeigt werden sollen.|
|\<Verzeichnis >|Gibt das Verzeichnis an, für das DACLs angezeigt werden sollen.|
|/t|Führt den Vorgang für alle angegebenen Dateien im aktuellen Verzeichnis und seinen Unterverzeichnissen aus.|
|/c|Der Vorgang wird trotz aller Datei Fehler fortgesetzt. Fehlermeldungen werden weiterhin angezeigt.|
|/l|Führt den Vorgang für eine symbolische Verknüpfung im Vergleich zum Ziel aus.|
|/q|Unterdrückt Erfolgsmeldungen.|
|[/Save \<aclfile > [/t] [/c] [/l] [/q]]|Speichert DACLs für alle übereinstimmenden Dateien in *aclfile* für die spätere Verwendung mit **/Restore**.|
|[/SetOwner \<username > [/t] [/c] [/l] [/q]]|Ändert den Besitzer aller übereinstimmenden Dateien für den angegebenen Benutzer.|
|[/findSID \<sid > [/t] [/c] [/l] [/q]]|Sucht alle übereinstimmenden Dateien, die eine DACL enthalten, die explizit die angegebene Sicherheits-ID (SID) erwähnt.|
|[/verify [/t] [/c] [/l] [/q]]|Findet alle Dateien mit ACLs, die nicht kanonisch sind oder Längen inkonsistent mit ACE (Access Control Entry)-Anzahlen aufweisen.|
|[/Reset [/t] [/c] [/l] [/q]]|Ersetzt ACLs durch geerbte Standard-ACLs für alle übereinstimmenden Dateien.|
|[/Grant [: r] \<sid >:<Perm>[...]]|Erteilt angegebene Benutzer Zugriffsrechte. Berechtigungen ersetzen zuvor erteilte explizite Berechtigungen.</br>Ohne **: r**werden Berechtigungen zu allen zuvor erteilten expliziten Berechtigungen hinzugefügt.|
|[/Deny \<sid >:<Perm>[...]]|Verweigert explizit angegebene Benutzer Zugriffsrechte. Für die angegebenen Berechtigungen wird ein expliziter Verweigerungs-ACE hinzugefügt, und die gleichen Berechtigungen in expliziten Berechtigungen werden entfernt.|
|[/remove [: g\|:d]] \<sid > [...]] /t /c /l /q|Entfernt alle Vorkommen der angegebenen SID aus der DACL.</br>**: g** entfernt alle Vorkommen der gewährten Rechte für die angegebene SID.</br>**:d** entfernt alle Vorkommen abgelehnter Rechte für die angegebene SID.|
|[/setintegritylevel [(CI) (OI)]\<Ebene >:<Policy>[...]]|Fügt allen übereinstimmenden Dateien explizit einen Integritäts-ACE hinzu. Die *Ebene* wird wie folgt angegeben:</br>-   **L**[OW]</br>-   **M**[edium]</br>-   **H**[IGH]</br>Vererbungs Optionen für den Integritäts-ACE können der Ebene vorangestellt werden und werden nur auf Verzeichnisse angewendet.|
|[/Substitute \<sidold > <SidNew> [...]]|Ersetzt eine vorhandene sid (*sidold*) durch eine neue sid (*sidnew*). Erfordert den *Directory* -Parameter.|
|/Restore \<aclfile > [/c] [/l] [/q]|Wendet gespeicherte DACLs aus *aclfile* auf Dateien im angegebenen Verzeichnis an. Erfordert den *Directory* -Parameter.|
|/InheritanceLevel: [e\|d\|r]|Legt die Vererbungs Ebene fest: <br>  **e** -Aktivierung der Einschreibung <br>**d** : Deaktivieren der Vererbung und Kopieren der ACEs <br>**r** -entfernt alle geerbten ACEs

## <a name="remarks"></a>Hinweise

-   SIDs können entweder in Form eines numerischen oder eines anzeigen Amens vorliegen. Wenn Sie ein numerisches Format verwenden, können Sie das Platz **&#42;** Halter Zeichen an den Anfang der SID anbinden.
-   **icacls** behält die kanonische Reihenfolge der ACE-Einträge wie folgt bei:  
    -   Explizite Verweigerungen
    -   Explizite Zuweisungen
    -   Geerbte Verweigerungen
    -   Geerbte Zuweisungen
-   *Perm* ist eine Berechtigungs Maske, die in einer der folgenden Formen angegeben werden kann:  
    -   Eine Sequenz von einfachen rechten:

        **F** (Vollzugriff)

        **M** (Zugriff ändern)

        **RX** (Lese-und Ausführungs Zugriff)

        **R** (Schreib geschützter Zugriff)

        **W** (Schreib geschützter Zugriff)
    -   Eine durch Trennzeichen getrennte Liste in Klammern spezifischer Rechte:

        **D** (Löschen)

        **RC** (Read-Steuerelement)

        **WDac** (Schreiben von DAC)

        **Wo** (Besitzer schreiben)

        **S** (Synchronisieren)

        **As** (Zugriffs Systemsicherheit)

        **MA** (maximal zulässig)

        **Gr** (generischer Lesevorgang)

        **GW** (generischer Schreibvorgang)

        **Ge** (generisches ausführen)

        **GA** (generisch)

        **RD** (Daten lesen/auflisten)

        **WD** (Daten schreiben/Datei hinzufügen)

        **AD** (Daten anfügen/Unterverzeichnis hinzufügen)

        **REA** (Erweiterte Attribute lesen)

        **WEA** (Erweiterte Attribute schreiben)

        **X** (ausführen/durchlaufen)

        **DC** (untergeordnetes Element löschen)

        **RA** (Attribute lesen)

        **WA** (Attribute schreiben)
-   Vererbungs Rechte können entweder der *Perm* -Form vorangestellt werden, und Sie werden nur auf Verzeichnisse angewendet:

    **(OI)** : Objekt erben

    **(CI)** : Container erben

    **(IO)** : nur Erben

    **(NP)** : nicht erben

## <a name="examples"></a>Beispiele

Wenn Sie die DACLs für alle Dateien im Verzeichnis "c:\Windows" und deren Unterverzeichnisse in der aclfile-Datei speichern möchten, geben Sie Folgendes ein:

```
icacls c:\windows\* /save aclfile /t
```

Geben Sie Folgendes ein, um die DACLs für jede Datei in aclfile wiederherzustellen, die im Verzeichnis "c:\Windows" und in den zugehörigen Unterverzeichnissen vorhanden ist:

```
icacls c:\windows\ /restore aclfile
```

Geben Sie Folgendes ein, um dem Benutzer user1 Berechtigungen zum Löschen und Schreiben von DAC für eine Datei mit dem Namen "test1" zu erteilen:

```
icacls test1 /grant User1:(d,wdac)
```

Geben Sie Folgendes ein, um dem Benutzer, der durch sid S-1-1-0 definiert ist, DAC-Berechtigungen für eine Datei mit dem Namen "test2" zu erteilen:

```
icacls test2 /grant *S-1-1-0:(d,wdac)
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
