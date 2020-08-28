---
title: msiexec
description: Referenz Artikel für den Befehl "msiexec", der die Möglichkeit bietet, Windows Installer über die Befehlszeile zu installieren, zu ändern und auszuführen.
ms.topic: reference
ms.assetid: 122eb0ce-ecbc-4909-a52a-15c3413619af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1255cf26ac4dd3f9c28189ce7df76d63c875ee64
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025284"
---
# <a name="msiexec"></a>msiexec

Bietet die Möglichkeit zum Installieren, ändern und Ausführen von Vorgängen auf Windows Installer von der Befehlszeile aus.

## <a name="install-options"></a>Installationsoptionen

Legen Sie den Installationstyp für das Starten eines Installationspakets fest.

### <a name="syntax"></a>Syntax

```
msiexec.exe [/i][/a][/j{u|m|/g|/t}][/x] <path_to_package>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| /i | Gibt die normale Installation an. |
| /a | Gibt die administrative Installation an. |
| /ju | Kündigen Sie das Produkt dem aktuellen Benutzer an. |
| /jm | Ankündigen Sie das Produkt für alle Benutzer. |
| /j/g | Gibt den sprach Bezeichner an, der vom angekündigten Paket verwendet wird. |
| /j/t | Wendet die Transformation auf das angekündigte Paket an. |
| /x | Deinstalliert das Paket. |
| `<path_to_package>` | Gibt den Speicherort und den Namen der Installationspaket Datei an. |

#### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Paket mit dem Namen *example.msi* vom Laufwerk C: zu installieren. verwenden Sie dazu einen normalen Installationsvorgang:

```
msiexec.exe /i "C:\example.msi"
```

## <a name="display-options"></a>Anzeigeoptionen

Basierend auf der Zielumgebung können Sie konfigurieren, was ein Benutzer während des Installationsvorgangs sieht. Wenn Sie z. b. ein Paket für die manuelle Installation an alle Clients verteilen, sollte eine vollständige Benutzeroberfläche vorhanden sein. Wenn Sie jedoch ein Paket mit Gruppenrichtlinie bereitstellen, für das keine Benutzerinteraktion erforderlich ist, sollte keine Benutzeroberfläche beteiligt sein.

### <a name="syntax"></a>Syntax

```
msiexec.exe /i <path_to_package> [/quiet][/passive][/q{n|b|r|f}]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| `<path_to_package>` | Gibt den Speicherort und den Namen der Installationspaket Datei an. |
| /quiet | Gibt den stillen Modus an. Dies bedeutet, dass keine Benutzerinteraktion erforderlich ist. |
| /passive | Gibt den unbeaufsichtigten Modus an. Dies bedeutet, dass die Installation nur eine Statusanzeige anzeigt. |
| /qn | Gibt an, dass während des Installationsvorgangs keine Benutzeroberfläche vorhanden ist. |
| /Qn + | Gibt an, dass während des Installationsvorgangs keine Benutzeroberfläche vorhanden ist, mit Ausnahme eines abschließenden Dialog Felds am Ende. |
| /qb | Gibt an, dass während des Installationsvorgangs eine grundlegende Benutzeroberfläche vorhanden ist. |
| /QB + | Gibt an, dass während des Installationsvorgangs eine grundlegende Benutzeroberfläche vorhanden ist, einschließlich eines abschließenden Dialog Felds am Ende. |
| /qr | Gibt eine reduzierte Benutzeroberfläche während des Installationsvorgangs an. |
| /qf | Gibt eine vollständige Benutzeroberfläche während des Installationsvorgangs an. |

##### <a name="remarks"></a>Bemerkungen

- Das modale Feld wird nicht angezeigt, wenn die Installation vom Benutzer abgebrochen wird. Sie können **qb +! verwenden.** oder **qb! +** , um die Schaltfläche " **Abbrechen** " auszublenden.

#### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Paket *C:\example.msi*zu installieren, indem Sie einen normalen Installationsvorgang und keine Benutzeroberfläche verwenden:

```
msiexec.exe /i "C:\example.msi" /qn
```

## <a name="restart-options"></a>Neustart Optionen

Wenn das Installationspaket Dateien überschreibt oder versucht, Dateien zu ändern, die verwendet werden, ist möglicherweise ein Neustart erforderlich, bevor die Installation abgeschlossen ist.

### <a name="syntax"></a>Syntax

```
msiexec.exe /i <path_to_package> [/norestart][/promptrestart][/forcerestart]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| `<path_to_package>` | Gibt den Speicherort und den Namen der Installationspaket Datei an. |
| /norestart | Beendet das Starten des Geräts nach Abschluss der Installation. |
| /promptrestart | Fordert den Benutzer auf, wenn ein Neustart erforderlich ist. |
| /forcerestart | Startet das Gerät nach Abschluss der Installation neu. |

#### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Paket *C:\example.msi*zu installieren. verwenden Sie dazu einen normalen Installationsprozess ohne Neustart am Ende:

```
msiexec.exe /i "C:\example.msi" /norestart
```

## <a name="logging-options"></a>Protokollierungsoptionen

Wenn Sie das Installationspaket Debuggen müssen, können Sie die Parameter so festlegen, dass eine Protokolldatei mit bestimmten Informationen erstellt wird.

### <a name="syntax"></a>Syntax

```
msiexec.exe [/i][/x] <path_to_package> [/L{i|w|e|a|r|u|c|m|o|p|v|x+|!|*}] <path_to_log>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| /i | Gibt die normale Installation an. |
| /x | Deinstalliert das Paket. |
| `<path_to_package>` | Gibt den Speicherort und den Namen der Installationspaket Datei an. |
| /li | Schaltet die Protokollierung ein und schließt Statusmeldungen in die Ausgabeprotokoll Datei ein. |
| /lw | Schaltet die Protokollierung ein und schließt nicht schwerwiegende Warnungen in die Ausgabeprotokoll Datei ein. |
| /le | Schaltet die Protokollierung ein und schließt alle Fehlermeldungen in der Ausgabeprotokoll Datei ein. |
| /la | Schaltet die Protokollierung ein und enthält Informationen darüber, wann eine Aktion in der Ausgabeprotokoll Datei gestartet wurde. |
| /lr | Schaltet die Protokollierung ein und schließt Aktions spezifische Datensätze in die Ausgabeprotokoll Datei ein. |
| /lu | Schaltet die Protokollierung ein und schließt Benutzer Anforderungs Informationen in die Ausgabeprotokoll Datei ein. |
| /lc | Schaltet die Protokollierung ein und schließt die anfänglichen Benutzeroberflächen Parameter in die Ausgabeprotokoll Datei ein. |
| /LM | Schaltet die Protokollierung ein und enthält nicht genügend Arbeitsspeicher oder schwerwiegende Beendigungs Informationen in der Ausgabeprotokoll Datei. |
| /lo | Schaltet die Protokollierung ein und schließt Nachrichten außerhalb des Speicherplatzes in die Ausgabeprotokoll Datei ein. |
| /lp | Schaltet die Protokollierung ein und schließt Terminal Eigenschaften in die Ausgabeprotokoll Datei ein. |
| /lp | Schaltet die Protokollierung ein und schließt Terminal Eigenschaften in die Ausgabeprotokoll Datei ein. |
| /lv | Schaltet die Protokollierung ein und schließt eine ausführliche Ausgabe in die Ausgabeprotokoll Datei ein. |
| /lp | Schaltet die Protokollierung ein und schließt Terminal Eigenschaften in die Ausgabeprotokoll Datei ein. |
| /lx | Schaltet die Protokollierung ein und enthält zusätzliche Debuginformationen in der Ausgabeprotokoll Datei. |
| /l + | Schaltet die Protokollierung ein und fügt die Informationen an eine vorhandene Protokolldatei an. |
| /l! | Schaltet die Protokollierung ein und leert jede Zeile in die Protokolldatei. |
| /l | Schaltet die Protokollierung ein und protokolliert alle Informationen, mit Ausnahme ausführlicher Informationen (**/LV**) oder zusätzlicher Debuginformationen (**/LX**). |
| `<path_to_logfile>` | Gibt den Speicherort und den Namen für die Ausgabeprotokoll Datei an. |

#### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Paket *C:\example.msi*zu installieren. verwenden Sie dazu einen normalen Installationsvorgang mit allen bereitgestellten Protokollinformationen, einschließlich ausführlicher Ausgabe und Speichern der Ausgabeprotokoll Datei unter " *c:\Package.log*":

```
msiexec.exe /i "C:\example.msi" /L*V "C:\package.log"
```

## <a name="update-options"></a>Updateoptionen

Sie können Updates mithilfe eines Installationspakets anwenden oder entfernen.

### <a name="syntax"></a>Syntax

```
msiexec.exe [/p][/update][/uninstall[/package<product_code_of_package>]] <path_to_package>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| /p | Installiert einen Patch. Wenn Sie eine unbeaufsichtigte Installation durcharbeiten, müssen Sie auch die Eigenschaft REINSTALLMODE auf *ecmus* festlegen und auf *alle*neu installieren. Andernfalls aktualisiert der Patch nur die MSI-Datei, die auf dem Zielgerät zwischengespeichert ist. |
| /update | Option zum Installieren von Patches. Wenn Sie mehrere Updates anwenden, müssen Sie Sie mit einem Semikolon (;)) trennen. |
| /Package | Installiert oder konfiguriert ein Produkt. |

#### <a name="examples"></a>Beispiele

```
msiexec.exe /p "C:\MyPatch.msp"
msiexec.exe /p "C:\MyPatch.msp" /qb REINSTALLMODE="ecmus" REINSTALL="ALL"
msiexec.exe /update "C:\MyPatch.msp"
```

```
msiexec.exe /uninstall {1BCBF52C-CD1B-454D-AEF7-852F73967318} /package {AAD3D77A-7476-469F-ADF4-04424124E91D}
```

Bei der ersten GUID handelt es sich um die Patch-GUID, bei der zweiten handelt es sich um den MSI-Produktcode, auf den der Patch angewendet wurde.

## <a name="repair-options"></a>Reparatur Optionen

Mit diesem Befehl können Sie ein installiertes Paket reparieren.

### <a name="syntax"></a>Syntax

```
msiexec.exe [/f{p|o|e|d|c|a|u|m|s|v}] <product_code>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| /fp | Repariert das Paket, wenn eine Datei fehlt. |
| /fo | Repariert das Paket, wenn eine Datei nicht vorhanden ist, oder wenn eine ältere Version installiert ist. |
| /FE | Repariert das Paket, wenn die Datei nicht vorhanden ist oder wenn eine oder eine frühere Version installiert ist. |
| /FD | Repariert das Paket, wenn die Datei nicht vorhanden ist oder eine andere Version installiert ist. |
| /fc | Repariert das Paket, wenn die Datei nicht vorhanden ist, oder, wenn die Prüfsumme nicht mit dem berechneten Wert identisch ist. |
| /FA | Erzwingt das erneute Installieren aller Dateien. |
| /Fu | Repariert alle erforderlichen benutzerspezifischen Registrierungseinträge. |
| /FM | Repariert alle erforderlichen computerspezifischen Registrierungseinträge. |
| /FS | Repariert alle vorhandenen Verknüpfungen. |
| /fc | Wird von der Quelle ausgeführt und speichert das lokale Paket erneut. |

#### <a name="examples"></a>Beispiele

Wenn Sie erzwingen möchten, dass alle Dateien basierend auf dem zu reparierenden MSI-Produktcode ( *{AAD3D77A-7476-469F-ADF4-04424124E91D}*) neu installiert werden, geben Sie Folgendes ein:

```
msiexec.exe /fa {AAD3D77A-7476-469F-ADF4-04424124E91D}
```

## <a name="set-public-properties"></a>Öffentliche Eigenschaften festlegen

Sie können öffentliche Eigenschaften mithilfe dieses Befehls festlegen. Informationen zu den verfügbaren Eigenschaften und deren Festlegung finden Sie unter [öffentliche Eigenschaften](/windows/win32/msi/public-properties).

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Msiexec.exe Befehlszeilenoptionen](/windows/win32/msi/command-line-options)

- [Standard Installationsprogramm-Befehlszeilenoptionen](/windows/win32/msi/standard-installer-command-line-options)
