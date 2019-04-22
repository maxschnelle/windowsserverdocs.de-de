---
title: Format
ms.prod: windows-server-threshold
manager: dongill
ms.author: JGerend
ms.technology: storage
ms.topic: article
ms.assetid: 51ec7423-9a01-4219-868a-25d69cdcc832
author: JasonGerend
ms.date: 10/16/2017
ms.openlocfilehash: 10c0dd97ddd7384673573c1354105314af5d5e04
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818981"
---
# <a name="format"></a>Format
> Gilt für: Windows 10, WindowsServer 2016

Formatiert einen Datenträger aus, um die Windows-Dateien akzeptiert.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
format <Volume> [/fs:{FAT|FAT32|NTFS}] [/v:<Label>] [/q] [/a:<UnitSize>] [/c] [/x] [/p:<Passes>]
format <Volume> [/v:<Label>] [/q] [/f:<Size>] [/p:<Passes>]
format <Volume> [/v:<Label>] [/q] [/t:<Tracks> /n:<Sectors>] [/p:<Passes>]
format <Volume> [/v:<Label>] [/q] [/p:<Passes>]
format <Volume> [/q]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Volume >|Gibt an, den Bereitstellungspunkt, Volumenamen oder Laufwerkbuchstaben (gefolgt von einem Doppelpunkt), der das Laufwerk, das Sie formatieren möchten. Wenn Sie nicht von den folgenden Befehlszeilenoptionen angeben **Format** verwendet Sie den Volumetyp, um das Standardformat für den Datenträger zu bestimmen.|
|/fs:{FAT|FAT32|NTFS|UDF}|Gibt den Typ des Dateisystems an: FAT, FAT32, NTFS- oder UDFs. Auf Disketten wird nur das Dateisystem FAT unterstützt.|
|/ v:\<Bezeichnung >|Gibt die Volumebezeichnung an. Wenn Sie weglassen der **/v** Befehlszeilen oder verwenden Sie es ohne Angabe einer Volumebezeichnung **Format** aufgefordert, die Volumebezeichnung nach Abschluss der Formatierung. Verwenden Sie die Syntax **/v:**, um die Aufforderung zur Eingabe einer Volumebezeichnung zu verhindern. Wenn Sie mit einem einzelnen **format**-Befehl mehrere Datenträger formatieren, erhalten alle Datenträger dieselbe Volumebezeichnung.|
|/a:\<UnitSize>|Gibt die Größe der Zuordnungseinheit auf FAT-, FAT32 oder NTFS-Volumes zu verwenden. Wenn Sie *UnitSize* nicht angeben, wird die Größe basierend auf der Volumegröße ausgewählt. Für die allgemeine Verwendung werden Standardeinstellungen unbedingt empfohlen. Die folgende Liste enthält gültige *UnitSize*-Werte für NTFS, FAT und FAT32:</br>512</br>1024</br>2.048</br>4.096</br>8.192</br>16 KB</br>32 KB</br>64 KB</br>FAT und FAT32 unterstützen auch 128 KB und 256 KB für eine Sektorgröße, die 512 Byte überschreitet.|
|/q|Führt eine Schnellformatierung durch. Löscht die Dateitabelle und das Stammverzeichnis eines bereits formatierten Volumes, jedoch führt keine Überprüfung Sektor für Sektor auf fehlerhafte Bereiche. Verwenden Sie die **/q /** Befehlszeilenoption nur formatiert bereits formatierte Volumes, die Sie kennen in gutem Zustand sind. Beachten Sie, dass **/p** von **/q** überschrieben wird.|
|/f:\<Size>|Gibt die Größe der zu formatierenden Diskette an. Verwenden Sie nach Möglichkeit diese Befehlszeilenoption anstelle der **/t /** und **/n** Befehlszeilenoptionen. Windows akzeptiert die folgenden Werte für die Größe:</br>–   1440 oder 1440k oder 1440kb</br>–   1,44 oder 1,44m oder 1,44mb</br>– 1,44 MB, beidseitiges, Quadrupel Dichte, 3,5-Zoll-Diskette|
|/ t:\<verfolgt >|Gibt die Anzahl der Spuren auf dem Datenträger an. Verwenden Sie nach Möglichkeit die **/f** Befehlszeilen option. Bei Verwendung der Option **/t** müssen Sie auch die Option **/n** verwenden. Diese Optionen bieten zusammen eine alternative Methode zum Angeben der Größe des Datenträgers, der formatiert wird. Diese Option ist mit der Option **/f** nicht gültig.|
|/ n:\<Sektoren >|Gibt die Anzahl der Sektoren pro Spur an. Verwenden Sie nach Möglichkeit die **/f** Befehlszeilenoption anstelle von **/n**. Bei Verwendung von **/n** müssen Sie auch **/t** verwenden. Diese beiden Optionen bieten zusammen eine alternative Methode zum Angeben der Größe des Datenträgers, der formatiert wird. Diese Option ist mit der Option **/f** nicht gültig.|
|/ p:\<übergibt >|Setzt jeden Sektor auf dem Volume für die Anzahl der angegeben Durchgänge auf 0. Diese Option ist mit der Option **/q** nicht gültig.|
|/c|Nur NTFS. Auf dem neuen Volume erstellte Dateien werden standardmäßig komprimiert.|
|/x|Bewirkt, dass die Bereitstellung des Volumes vor seiner Formatierung bei Bedarf aufgehoben wird. Alle geöffneten Handles zum Volume sind nicht mehr gültig.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Administratoranmeldeinformationen

    Sie müssen ein Mitglied der Gruppe "Administratoren" auf eine Festplatte formatiert werden.
-   Mithilfe von **Format**

    Die **Format** Befehl erstellt eine neue Stammverzeichnis und Dateisystem für den Datenträger. Es kann auch fehlerhafte Bereiche auf dem Datenträger überprüfen, und es kann alle Daten auf dem Datenträger löschen. Um einen neuen Datenträger verwenden können, müssen Sie zuerst mit diesem Befehl verwenden, auf um den Datenträger zu formatieren.
-   Hinzufügen einer Volumebezeichnung

    Nach der Formatierung von einer Diskette, **Format** wird die folgende Meldung angezeigt:

    `Volume label (11 characters, ENTER for none)?`

    Geben Sie zum Hinzufügen einer Volumebezeichnung bis zu 11 Zeichen (einschließlich Leerzeichen) ein. Wenn Sie nicht, um eine Volumebezeichnung ein auf den Datenträger hinzuzufügen möchten, drücken Sie die EINGABETASTE.
-   Formatieren einer Festplatte

> [!NOTE]
> Sie müssen ein Mitglied der Gruppe "Administratoren" auf eine Festplatte formatiert werden.

Bei Verwendung der **Format** Befehl zum Formatieren einer Festplatte, die eine Warnmeldung angezeigt, die ähnlich wie die folgende angezeigt:
```
WARNING, ALL DATA ON NON-REMOVABLE DISK 
DRIVE x: WILL BE LOST! 
Proceed with Format (Y/N)? _ 
```
Um die Festplatte zu formatieren, drücken Sie Y aus; Wenn Sie nicht den Datenträger formatieren möchten. drücken Sie N.
-   Größe der

    FAT-Dateisystemen beschränken die Anzahl von Clustern zu 65526. FAT32-Dateisysteme beschränken die Anzahl der Cluster zwischen 65527 und 4177917.

    Die NTFS-Komprimierung wird für Zuordnungseinheiten größer als 4.096 nicht unterstützt.

> [!NOTE]
> **Format** sofort beendet die Verarbeitung, wenn er feststellt, dass die obigen Anforderungen mithilfe der angegebenen Clustergröße nicht erfüllt werden können.
-   **Format** Nachrichten

    Nach Abschluss der Formatierung wird **Format** zeigt an, die den gesamten Speicherplatz, die Leerzeichen als fehlerhaft gekennzeichnet und den verfügbaren Speicherplatz für die Dateien angezeigt werden.
-   Schnellformatierung

    Sie können die Formatierung zu beschleunigen, mit der **/q /** Befehlszeilenoption. Verwenden Sie diese Option nur, wenn es keine fehlerhaften Sektoren auf der Festplatte gibt.
-   Verwenden von **format** mit einem neu zugewiesenen Laufwerk oder Netzlaufwerk

    Sie dürfen den Befehl **format** nicht auf einem Laufwerk verwenden, das mit dem Befehl **subst** vorbereitet wurde. Datenträger können nicht über ein Netzwerk formatiert werden.
-   Exitcodes für **format**

    In der folgenden Tabelle sind alle Exitcodes und eine Kurzbeschreibung ihrer Bedeutung aufgeführt.  
    |Exitcode|Beschreibung|
    |---------|-----------|
    |0|Der Formatierungsvorgang war erfolgreich.|
    |1|Es wurden falsche Parameter angegeben.|
    |4|Ein schwerwiegender Fehler aufgetreten ist (die alle Fehler außer 0, 1 oder 5).|
    |5|Vom Benutzer gedrückten N als Antwort auf die Frage "Formatierung durchführen (J/N)?" um den Vorgang zu beenden.|

    Sie können diese Exitcodes mithilfe der Umgebungsvariablen ERRORLEVEL und des Batchbefehls **if** überprüfen.
-   Verwenden von **format** in der Wiederherstellungskonsole

    Der Befehl **format** steht in der Wiederherstellungskonsole mit verschiedenen Parametern zur Verfügung.

## <a name="BKMK_examples"></a>Beispiele für

Um eine neue Diskette in Laufwerk A mit der Standardgröße zu formatieren, geben Sie Folgendes ein:
```
format a:
```
Um eine Schnellformatierung auf eine zuvor formatierte Diskette in Laufwerk A anzuwenden, geben Sie Folgendes ein:
```
format a: /q
```
Um eine Diskette in Laufwerk A zu formatieren und ihr die Volumebezeichnung „DATA“ zuzuweisen, geben Sie Folgendes ein:
```
format a: /v:DATA
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](https://technet.microsoft.com/library/cc771080.aspx)