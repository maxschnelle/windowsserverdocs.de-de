---
title: icacls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b1aaa329c8925d7fa4245555ed51b08f7366299d
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811108"
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
|\<FileName>|Gibt die Datei für die DACLs angezeigt werden sollen.|
|\<Directory>|Gibt das Verzeichnis für die DACLs angezeigt werden sollen.|
|/t|Führt den Vorgang für alle angegebenen Dateien im aktuellen Verzeichnis und seinen Unterverzeichnissen.|
|/c|Setzt den Vorgang trotz der Dateifehler fort. Fehlermeldungen werden weiterhin angezeigt werden.|
|/l|Führt den Vorgang auf eine symbolische Verknüpfung im Vergleich zu das Ziel.|
|/q|Werden Erfolgsmeldungen unterdrückt.|
|[/ speichern \<ACLfile > [t] [c] [/ l] [/ q]]|Speichert DACLs für alle übereinstimmenden Dateien *ACLfile* für die spätere Verwendung mit **/Wiederherstellung**.|
|[/ Setowner \<Benutzername > [t] [c] [/ l] [/ q]]|Ändert den Besitzer aller entsprechenden Dateien für den angegebenen Benutzer.|
|[/ FindSID \<Sid > [t] [c] [/ l] [/ q]]|Sucht alle übereinstimmende Dateien, die eine DACL, die explizit erwähnt werden die angegebene Sicherheits-ID (SID) enthalten.|
|[/ Überprüfen von [t] [c] [/ l] [/ q]]|Sucht nach allen Dateien mit ACLs, die nicht kanonische oder inkonsistente ACE (Access Control-Eintrag) anzahlbasiertes Länge haben.|
|[/ zurücksetzen [t] [c] [/ l] [/ q]]|Standard-ACLs, ersetzt werden ACLs für alle übereinstimmenden Dateien geerbt.|
|[/ erteilen [: R] \<Sid >:<Perm>[...]]|Gewährt angegeben Benutzerzugriffsrechte an. Berechtigungen ersetzen zuvor gewährt explizite Berechtigungen.</br>Ohne **: R**, Berechtigungen werden auf eine zuvor explizite Berechtigungen hinzugefügt.|
|[/ deny \<Sid >:<Perm>[...]]|Explizit verweigert den angegebenen Benutzerzugriffsrechte. Ein explizites verbotssystem ACE wird hinzugefügt, für die angegebenen Berechtigungen und die gleichen Berechtigungen in jede ausdrückliche Erteilung von Berechtigungen entfernt werden.|
|[/ remove [: g\|: d]] \<Sid > [...]] [t] [c] [/ l] [/ q]|Entfernt alle Vorkommen der angegebenen SID aus der DACL.</br>**: g** entfernt alle Vorkommen der gewährten Rechte für die angegebene SID.</br>**: d** entfernt alle Vorkommen der verweigerten Rechte für die angegebene SID.|
|[/ Setintegritylevel [(CI)(OI)]\<Ebene >:<Policy>[...]]|Alle übereinstimmenden Dateien hinzugefügt explizit ein Integrität ACE. *Ebene* als angegeben wird:</br>-   **L**[ow]</br>-   **M**[Edium]</br>-   **H**[beres]</br>Vererbungsoptionen für die Integrität ACE können der Ebene vor, und es gelten nur für Verzeichnisse.|
|[/ Ersetzen \<SidOld > <SidNew> [...]]|Ersetzt eine vorhandene SID (*SidOld*) mit einer neuen SID (*SidNew*). Erfordert die *Directory* Parameter.|
|/ Wiederherstellung \<ACLfile > [c] [/ l] [/ q]|Wendet gespeicherte DACLs aus *ACLfile* auf Dateien im angegebenen Verzeichnis. Erfordert die *Directory* Parameter.|
|/inheritancelevel:[e\|d\|r]|Legt fest, das die Vererbungsebene: <br>  **e** -Enheritance aktiviert <br>**d** : deaktiviert die Vererbung und kopiert die ACEs <br>**R** – entfernt alle geerbten Zugriffssteuerungseinträge

## <a name="remarks"></a>Hinweise

-   SIDs kann entweder numerische oder angezeigter Name-Format haben. Wenn Sie ein numerisches Format verwenden, bringt Sie das Platzhalterzeichen an **&#42;** auf den Anfang der SID.
-   **Icacls** behält die kanonische Reihenfolge des ACE-Einträge, wie:  
    -   Explizite ablehnungen
    -   Explizite gewährt
    -   Geerbte ablehnungen
    -   Geerbte gewährt
-   *Perm* ist eine Berechtigungsmaske, die in einem der folgenden Formate angegeben werden kann:  
    -   Eine Sequenz von einfachen rechten:

        **F** (Vollzugriff)

        **M** (ändern Sie den Zugriff)

        **RX** (Lese- und Ausführungsberechtigungen)

        **R** (nur-Lese Zugriff)

        **W** (nur-schreiben-Datenzugriff)
    -   Eine durch Trennzeichen getrennte Liste in Klammern, der bestimmte Rechte:

        **D** (löschen)

        **RC** (Lesezugriff)

        **WDAC** (DAC schreiben)

        **WEI** (Besitzer schreiben)

        **S** (synchronisieren)

        **AS** (Systemsicherheit Zugriff)

        **MA** (maximal zulässig)

        **GR** (generische lesen)

        **GW** (generic Write)

        **GE** (generische execute)

        **Bei allgemeiner Verfügbarkeit** (generische alle)

        **Remotedesktop** (Lesen von Daten/Verzeichnis)

        **WD** (Datei/hinzufügen von Daten schreiben)

        **AD** (Anfügen Unterverzeichnis/Hinzufügen von Daten)

        **REA** (Erweiterte Attribute lesen)

        **WEA** (Schreiben von erweiterten Attributen)

        **X** (Ausführen/durchsuchenden)

        **DC** (untergeordnetes Element löschen)

        **RA** (Attribute lesen)

        **WA** (Schreiben von Attributen)
-   Vererbung von Berechtigungen können entweder vorausgehen *Perm* Formular, und sie gelten nur für Verzeichnisse:

    **(OI)** : für Datenobjekte erbt

    **(CI)** : Container erben.

    **(E/A)** : nur erben

    **(NP)** : do not propagate inherit

## <a name="examples"></a>Beispiele

Um die DACLs für alle Dateien in das Verzeichnis von C:\Windows und seinen Unterverzeichnissen der ACLFile-Datei zu speichern, geben Sie Folgendes ein:

```
icacls c:\windows\* /save aclfile /t
```

Um die DACLs für jede Datei innerhalb der ACLFile wiederherzustellen, die in das Verzeichnis von C:\Windows und seinen Unterverzeichnissen vorhanden ist, geben Sie Folgendes ein:

```
icacls c:\windows\ /restore aclfile
```

Geben Sie den Benutzer "user1" zu löschen und Schreiben von DAC in eine Datei namens "Test1" zu gewähren:

```
icacls test1 /grant User1:(d,wdac)
```

Geben Sie Folgendes ein, um die benutzerdefinierte SID S-1-1-0 löschen und Schreiben von DAC-Berechtigungen in eine Datei, die mit dem Namen "Test2", zu gewähren:

```
icacls test2 /grant *S-1-1-0:(d,wdac)
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
