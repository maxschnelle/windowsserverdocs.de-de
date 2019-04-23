---
title: regini
description: Erfahren Sie, wie Sie die Registrierung über die Eingabeaufforderung oder mithilfe eines Skripts ändern.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ff18dc3-5bd8-400a-b311-fd73a3267e8c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 292dfe5755a10a91f2b8bcffaa6412ccda6c6f8a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867631"
---
# <a name="regini"></a>regini

Ändert die Registrierung über die Befehlszeile oder ein Skript, und Änderungen, die in eine oder mehrere Textdateien Voreinstellung wurden angewendet. Sie können erstellen, ändern oder Löschen von Registrierungsschlüsseln, zusätzlich zum Ändern der Berechtigungen für die Registrierungsschlüssel.

Ausführliche Informationen zum Format und Inhalt der Text-Skriptdatei, die Regini.exe verwendet wird, um Änderungen an der Registrierung vornehmen, finden Sie unter [wie Registrierungswerte oder Berechtigungen über eine Befehlszeile oder ein Skript geändert](https://support.microsoft.com/help/264584/how-to-change-registry-values-or-permissions-from-a-command-line-or-a).

## <a name="syntax"></a>Syntax

```
regini [-m \\machinename | -h hivefile hiveroot][-i n] [-o outputWidth][-b] textFiles...
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|-m \< \\ \\ComputerName >|Gibt Namen des Remotecomputers mit einer Registrierung, die geändert werden soll. Verwenden Sie das Format  **\\ \\ComputerName**.|
|---------------------|-|
|-h \<Hivefile Hiveroot >|Gibt die lokale Registrierung-Struktur ändern. Sie müssen den Namen der Hive-Datei und den Stamm der Struktur angeben, im Format **Hivefile Hiveroot**.|
|-i \<n>|Gibt die Ebene des Einzugs zu verwenden, um die Struktur der Registrierungsschlüssel in der Befehlsausgabe anzugeben. Die **Regdmp.exe** -Tool (das eine Registrierung aktuellen Berechtigungen des Schlüssels im Binärformat ruft) mithilfe von Einzügen ein Vielfaches von vier, damit der Standardwert ist **4**.|
|-o \<outputwidth>|Gibt die Breite der Ausgabe des Befehls, in Zeichen an. Wenn die Ausgabe im Befehlsfenster angezeigt wird, ist der Standardwert der Breite des Fensters. Wenn die Ausgabe in eine Datei weitergeleitet wird, wird der Standardwert ist **240** Zeichen.|
|-b|Gibt an, dass **Regini.exe** Ausgabe ist abwärtskompatibel mit früheren Versionen von **Regini.exe**. Finden Sie im Abschnitt "Hinweise".|
|%% amp;quot;c:\textfiles%%amp;quot|Gibt den Namen von ein oder mehrere Textdateien, die Registrierungsdaten enthalten. Es kann eine beliebige Anzahl von ANSI- oder Unicode-Text-Dateien aufgeführt werden.|

## <a name="remarks"></a>Hinweise

Die folgenden Richtlinien gelten in erster Linie auf den Inhalt der Textdateien, die Registrierungsdaten, die Sie anwenden enthalten, indem Sie mithilfe von **Regini.exe**.
-   Verwenden Sie das Semikolon als von End-of-Line-Kommentarzeichen. Es muss das erste nicht leere Zeichen in einer Zeile sein.
-   Verwenden Sie den umgekehrten Schrägstrich, um die Fortsetzung einer Zeile anzugeben. Der Befehl ignoriert alle Zeichen aus dem umgekehrten Schrägstrich, bis zu (aber nicht einschließlich) dem ersten Zeichen der nächsten Zeile. Wenn Sie mehr als ein Leerzeichen vor dem umgekehrten Schrägstrich einbeziehen, wird es durch ein einzelnes Leerzeichen ersetzt.
-   Verwenden Sie feste Tabstoppzeichen, um Einzug zu steuern. Diese Einzüge gibt an, die Struktur der Registrierungsschlüssel; Allerdings werden diese Zeichen in ein einzelnes Leerzeichen unabhängig von ihrer Position konvertiert.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)