---
title: cipher
description: Referenz Artikel zum Chiffre Befehl, der die Verschlüsselung von Verzeichnissen und Dateien auf NTFS-Volumes anzeigt oder ändert.
ms.topic: reference
ms.assetid: 78ef795e-0f87-4acd-8d15-192c972c0f41
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ff3c98a3533b77f257c2f1bd4d7102ccd0eed1f7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629677"
---
# <a name="cipher"></a>cipher

Ändert die Verschlüsselung von Verzeichnissen und Dateien auf NTFS-Volumes oder zeigt sie an. Bei Verwendung ohne Parameter zeigt **Chiffre** den Verschlüsselungs Status des aktuellen Verzeichnisses und aller darin enthaltenen Dateien an.

## <a name="syntax"></a>Syntax

```
cipher [/e | /d | /c] [/s:<directory>] [/b] [/h] [pathname [...]]
cipher /k
cipher /r:<filename> [/smartcard]
cipher /u [/n]
cipher /w:<directory>
cipher /x[:efsfile] [filename]
cipher /y
cipher /adduser [/certhash:<hash> | /certfile:<filename>] [/s:directory] [/b] [/h] [pathname [...]]
cipher /removeuser /certhash:<hash> [/s:<directory>] [/b] [/h] [<pathname> [...]]
cipher /rekey [pathname [...]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---------- | ----------- |
| /b | Bricht ab, wenn ein Fehler aufgetreten ist. Standardmäßig wird die **Chiffre** auch dann ausgeführt, wenn Fehler auftreten. |
| /C | Zeigt Informationen über die verschlüsselte Datei an. |
| /d | Entschlüsselt die angegebenen Dateien oder Verzeichnisse. |
| /e | Verschlüsselt die angegebenen Dateien oder Verzeichnisse. Verzeichnisse werden so gekennzeichnet, dass Dateien, die später hinzugefügt werden, verschlüsselt werden. |
| /h | Zeigt Dateien mit ausgeblendeten oder System Attributen an. Diese Dateien werden standardmäßig nicht verschlüsselt oder entschlüsselt. |
| /k | Erstellt ein neues Zertifikat und einen Schlüssel für die Verwendung mit Verschlüsselndes Dateisystem (EFS)-Dateien. Wenn der **/k** -Parameter angegeben wird, werden alle anderen Parameter ignoriert. |
| /r: `<filename>` [/Smartcard] | Generiert einen EFS-Wiederherstellungs-Agent-Schlüssel und ein Zertifikat und schreibt Sie dann in eine PFX-Datei (die das Zertifikat und den privaten Schlüssel enthält) und eine CER-Datei (die nur das Zertifikat enthält). Wenn **/Smartcard** angegeben wird, werden der Wiederherstellungs Schlüssel und das Zertifikat auf eine Smartcard geschrieben, und es wird keine PFX-Datei generiert. |
| /s`<directory>` | Führt den angegebenen Vorgang für alle Unterverzeichnisse im angegebenen *Verzeichnis*aus. |
| /u [/n] |  Sucht alle verschlüsselten Dateien auf dem lokalen Laufwerk. Wenn Sie mit dem **/n** -Parameter verwendet wird, werden keine Updates vorgenommen. Bei Verwendung ohne **/n**vergleicht **/u** den Datei Verschlüsselungsschlüssel des Benutzers oder den Schlüssel des Wiederherstellungs-Agents mit den aktuellen, und aktualisiert diese, wenn Sie geändert wurden. Dieser Parameter kann nur mit **/n**verwendet werden. |
| /w`<directory>` | Entfernt Daten aus dem verfügbaren nicht verwendeten Speicherplatz auf dem gesamten Volume. Wenn Sie den **/w** -Parameter verwenden, werden alle anderen Parameter ignoriert. Das angegebene Verzeichnis kann sich an einer beliebigen Stelle in einem lokalen Volume befinden. Wenn es sich um einen Einstellungs Punkt handelt oder auf ein Verzeichnis in einem anderen Volume verweist, werden die Daten auf diesem Volume entfernt. |
| /x [: efsfile] [ `<FileName>` ] | Sichert das EFS-Zertifikat und die Schlüssel für den angegebenen Dateinamen. Bei Verwendung mit **: efsfile**sichert **/x** die Zertifikate des Benutzers, die zum Verschlüsseln der Datei verwendet wurden. Andernfalls werden das aktuelle EFS-Zertifikat und die Schlüssel des Benutzers gesichert. |
| /y | Zeigt die aktuelle EFS-Zertifikat Miniaturansicht auf dem lokalen Computer an. |
| /adduser [/certhash:`<hash>` | /CertFile: `<filename>` ] |
| /rekey | Aktualisiert die angegebene verschlüsselte Datei (en), sodass Sie den derzeit konfigurierten EFS-Schlüssel verwendet. |
| /removeuser /certhash:`<hash>` | Entfernt einen Benutzer aus den angegebenen Dateien. Der für **/CertHash** angegebene *Hash* muss der SHA1-Hash des Zertifikats sein, das entfernt werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="remarks"></a>Hinweise

- Wenn das übergeordnete Verzeichnis nicht verschlüsselt ist, kann eine verschlüsselte Datei bei der Änderung entschlüsselt werden. Wenn Sie eine Datei verschlüsseln, sollten Sie daher auch das übergeordnete Verzeichnis verschlüsseln.

- Ein Administrator kann den Inhalt einer CER-Datei der EFS-Wiederherstellungs Richtlinie hinzufügen, um den Wiederherstellungs-Agent für Benutzer zu erstellen, und dann die PFX-Datei importieren, um einzelne Dateien wiederherzustellen.

- Sie können mehrere Verzeichnisnamen und Platzhalter verwenden.

- Sie müssen Leerzeichen zwischen mehreren Parametern platzieren.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Verschlüsselungs Status der einzelnen Dateien und Unterverzeichnisse im aktuellen Verzeichnis anzuzeigen:

```
cipher
```

Verschlüsselte Dateien und Verzeichnisse werden mit **E**gekennzeichnet. Unverschlüsselte Dateien und Verzeichnisse werden mit einem **U**gekennzeichnet. Die folgende Ausgabe gibt beispielsweise an, dass das aktuelle Verzeichnis und alle zugehörigen Inhalte zurzeit unverschlüsselt sind:

```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
U Private
U hello.doc
U hello.txt
```

Geben Sie Folgendes ein, um die Verschlüsselung für das im vorherigen Beispiel verwendete private Verzeichnis zu aktivieren:

```
cipher /e private
```

Die folgende Ausgabe wird angezeigt:

```
Encrypting files in C:\Users\MainUser\Documents\
Private             [OK]
1 file(s) [or directorie(s)] within 1 directorie(s) were encrypted.
```

Der Befehl " **Chiffre** " zeigt die folgende Ausgabe an:

```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
E Private
U hello.doc
U hello.txt
```

Wenn das **private** Verzeichnis nun als verschlüsselt gekennzeichnet ist.

### <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
