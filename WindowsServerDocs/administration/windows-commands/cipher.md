---
title: cipher
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78ef795e-0f87-4acd-8d15-192c972c0f41
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: baf527d3590a4ec52a51260d3083419ab27d548d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887181"
---
# <a name="cipher"></a>cipher



Ändert die Verschlüsselung von Verzeichnissen und Dateien auf NTFS-Volumes oder zeigt sie an. Wenn Sie ohne Angabe von Parametern **Cipher** zeigt den Verschlüsselungsstatus des aktuellen Verzeichnisses und aller darin enthaltenen Dateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
cipher [/e | /d | /c] [/s:<Directory>] [/b] [/h] [PathName [...]]
cipher /k
cipher /r:<FileName> [/smartcard]
cipher /u [/n]
cipher /w:<Directory>
cipher /x[:efsfile] [FileName]
cipher /y
cipher /adduser [/certhash:<Hash> | /certfile:<FileName>] [/s:Directory] [/b] [/h] [PathName [...]]
cipher /removeuser /certhash:<Hash> [/s:<Directory>] [/b] [/h] [<PathName> [...]]
cipher /rekey [PathName [...]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|----------|-----------|
|/b|Bricht Sie ab, wenn ein Fehler aufgetreten ist. In der Standardeinstellung **Cipher** wird weiterhin ausgeführt, auch wenn Fehler auftreten.|
|/c|Zeigt Informationen zu der verschlüsselten Datei.|
|/d|Entschlüsselt die angegebenen Dateien oder Verzeichnisse.|
|/ e|Verschlüsselt die angegebenen Dateien oder Verzeichnisse. Verzeichnisse werden markiert, sodass Dateien, die später hinzugefügt werden verschlüsselt werden.|
|/h|Zeigt Dateien mit ausgeblendet oder Systemattribute. Standardmäßig werden diese Dateien nicht verschlüsselt oder entschlüsselt.|
|/k|Erstellt ein neues Zertifikat und Schlüssel für die Verwendung mit verteilten Dateisystems (Encrypting File System, EFS)-Dateien an. Wenn die **/k** -Parameter angegeben wird, alle anderen Parameter werden ignoriert.|
|/ r:\<Dateiname > [/ Smartcard]|Generiert eine EFS-Wiederherstellungs-Agent-Schlüssel und das Zertifikat, und schreibt sie in eine PFX-Datei (mit Zertifikaten und privaten Schlüsseln) und eine CER-Datei (nur das Zertifikat enthält). Wenn **/Smartcard** angegeben wird, schreibt er den Wiederherstellungsschlüssel und das Zertifikat in eine Smartcard, und keine PFX-Datei generiert.|
|/ s:\<Verzeichnis >|Führt den angegebenen Vorgang für alle Unterverzeichnisse im angegebenen *Directory*.|
|/u [/n]|Sucht alle verschlüsselte Dateien auf lokalen Laufwerken. Bei Verwendung mit der **/n** -Parameter, die keine Updates ausgeführt werden. Ohne Angabe von **/n**, **/u** vergleicht Verschlüsselungsschlüssel für Sicherheitsdatei des Benutzers oder der Recovery-Agent-Schlüssel auf den aktuellen Schlüssel und aktualisiert sie, wenn diese geändert wurden. Dieser Parameter funktioniert nur mit **/n**.|
|/ w:\<Verzeichnis >|Entfernt Daten aus nicht verwendeten Speicherplatz auf dem Datenträger. Bei Verwendung der **/w** Parameter alle anderen Parameter werden ignoriert. Das angegebene Verzeichnis kann an einer beliebigen Stelle in einem lokalen Volume befinden. Wenn sie ein Bereitstellungspunkt zeigen oder Wiederherstellungspunkte in einem anderen Volume, die Daten in ein Verzeichnis, dass das Volume entfernt wird.|
|/ x [: Efsfile] [\<Dateiname >]|Sichert die EFS-Zertifikate und Schlüssel des angegebenen Dateinamens. Bei Verwendung mit **: Efsfile**, **/x** gesichert, die Zertifikate des Benutzers, die zum Verschlüsseln der Datei verwendet wurden. Andernfalls werden aktuelle EFS-Zertifikat und Schlüssel des Benutzers gesichert.|
|/y|Zeigt Ihre aktuelle Miniaturansicht der EFS-Zertifikat auf dem lokalen Computer.|
|/adduser [/ Certhash:\<Hash > | /certfile:<FileName>]|Fügt einen Benutzer für die angegebenen verschlüsselten Dateien. Bei Verwendung mit **/certhash**, **Cipher** sucht nach einem Zertifikat mit dem SHA1-Hash angegeben. Bei Verwendung mit **/certfile**, **Cipher** extrahiert das Zertifikat aus dem angegebenen Dateinamen.|
|/rekey|Aktualisiert die angegebenen verschlüsselten Dateien den aktuell konfigurierten EFS-Schlüssel verwenden.|
|/RemoveUser /certhash:\<Hash >|Entfernt einen Benutzer aus den angegebenen Dateien. Die *Hash* vorgesehenen **/certhash** muss der SHA1-Hash des Zertifikats, das entfernt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn das übergeordnete Verzeichnis nicht verschlüsselt ist, konnte eine verschlüsselte Datei entschlüsselt werden, wenn er geändert wird. Aus diesem Grund, wenn Sie eine Datei verschlüsseln, sollten Sie auch das übergeordnete Verzeichnis verschlüsseln.
-   Ein Administrator kann die EFS-Wiederherstellungsrichtlinie So erstellen Sie die Recovery-Agent für Benutzer den Inhalt der CER-Datei hinzugefügt, und importieren Sie die PFX-Datei zum Wiederherstellen einzelner Dateien.
-   Sie können mehrere Verzeichnisnamen und Platzhalter verwenden.
-   Sie müssen die Leerzeichen zwischen den verschiedenen Parametern eingefügt werden.

## <a name="BKMK_examples"></a>Beispiele für

Um den Verschlüsselungsstatus der einzelnen Dateien und Unterverzeichnisse im aktuellen Verzeichnis anzuzeigen, geben Sie Folgendes ein:
```
cipher
```
Verschlüsselte Dateien und Verzeichnisse mit markiert sind ein **E**. Unverschlüsselte Dateien und Verzeichnisse mit markiert sind eine **U**. Die folgende Ausgabe gibt beispielsweise an, dass das aktuelle Verzeichnis und seinen gesamten Inhalt derzeit unverschlüsselte sind:
```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
U Private
U hello.doc
U hello.txt
```
Geben Sie zum Aktivieren der Verschlüsselung für das Private Verzeichnis, das im vorherigen Beispiel verwendet:
```
cipher /e private
```
Die folgende Ausgabe angezeigt:
```
Encrypting files in C:\Users\MainUser\Documents\
Private             [OK]
1 file(s) [or directorie(s)] within 1 directorie(s) were encrypted.
```
Die **Cipher** Befehl wird die folgende Ausgabe angezeigt:
```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
E Private
U hello.doc
U hello.txt
```
Beachten Sie, dass das Private Verzeichnis markiert ist verschlüsselt.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)