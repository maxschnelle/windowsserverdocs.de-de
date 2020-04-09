---
title: Format
ms.prod: windows-server
manager: dongill
ms.author: jgerend
ms.technology: storage
ms.topic: article
ms.assetid: 51ec7423-9a01-4219-868a-25d69cdcc832
author: jasongerend
ms.date: 10/16/2017
ms.openlocfilehash: 95f88ef316bb7d188db212911835b867c6d4556f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844473"
---
# <a name="format"></a>Format
> Gilt für: Windows 10, Windows Server 2016

Formatiert einen Datenträger zum Akzeptieren von Windows-Dateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
format <Volume> [/fs:{FAT|FAT32|NTFS}] [/v:<Label>] [/q] [/a:<UnitSize>] [/c] [/x] [/p:<Passes>]
format <Volume> [/v:<Label>] [/q] [/f:<Size>] [/p:<Passes>]
format <Volume> [/v:<Label>] [/q] [/t:<Tracks> /n:<Sectors>] [/p:<Passes>]
format <Volume> [/v:<Label>] [/q] [/p:<Passes>]
format <Volume> [/q]
```

### <a name="parameters"></a>Parameter

|   Parameter    |                                                                                                                                                                                                                    Beschreibung                                                                                                                                                                                                                     |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   \<Volume >    |                                                                                         Gibt den Einfügepunkt, den Volumenamen oder den Laufwerk Buchstaben (gefolgt von einem Doppelpunkt) des Laufwerks an, das Sie formatieren möchten. Wenn Sie keine der folgenden Befehlszeilenoptionen angeben, verwendet **Format** den Volumentyp, um das Standardformat für den Datenträger festzulegen.                                                                                         |
|    /FS: {FAT    |                                                                                                                                                                                                                       FAT32                                                                                                                                                                                                                        |
|  /v:\<Bezeichnung >   |                           Gibt die Volumebezeichnung an. Wenn Sie die Befehlszeilenoption **/v** weglassen oder verwenden, ohne eine Volumebezeichnung anzugeben, werden Sie durch **Format** zur Eingabe der Volumebezeichnung aufgefordert, nachdem die Formatierung fertiggestellt wurde. Verwenden Sie die Syntax **/v:** , um die Aufforderung zur Eingabe einer Volumebezeichnung zu verhindern. Wenn Sie mit einem einzelnen **format**-Befehl mehrere Datenträger formatieren, erhalten alle Datenträger dieselbe Volumebezeichnung.                            |
| /a:\<UnitSize-> | Gibt die Größe der Zuordnungs Einheit an, die auf FAT-, FAT32-oder NTFS-Volumes verwendet wird. Wenn Sie *UnitSize* nicht angeben, wird die Größe basierend auf der Volumegröße ausgewählt. Für die allgemeine Verwendung werden Standardeinstellungen unbedingt empfohlen. Die folgende Liste enthält gültige *UnitSize*-Werte für NTFS, FAT und FAT32:</br>512</br>1024</br>2\.048</br>4\.096</br>8\.192</br>16.000</br>32 Tsd.</br>64 KB</br>FAT und FAT32 unterstützen auch 128 KB und 256 KB für eine Sektorgröße, die 512 Byte überschreitet. |
|       /q       |                                                       Führt eine Schnellformatierung durch. Löscht die Dateitabelle und das Stammverzeichnis eines zuvor formatierten Volumes, führt jedoch keinen sektorbasierten Scan für fehlerhafte Bereiche durch. Verwenden Sie die Befehlszeilenoption **/q** , um nur zuvor formatierte Volumes zu formatieren, von denen Sie wissen, dass Sie sich in einem guten Zustand befinden. Beachten Sie, dass **/p** von **/q** überschrieben wird.                                                       |
|   /f:\<Größe >   |                                                         Gibt die Größe der zu formatierenden Diskette an. Verwenden Sie nach Möglichkeit diese Befehlszeilenoption anstelle der Befehlszeilenoptionen **/t** und **/n** . Windows akzeptiert die folgenden Werte für die Größe:</br>–   1440 oder 1440k oder 1440kb</br>–   1,44 oder 1,44m oder 1,44mb</br>-1,44-MB, Double-seitig, vierfach Dichte, 3,5-Zoll-Datenträger                                                         |
|  /t:\<verfolgt >  |                                                    Gibt die Anzahl der Spuren auf dem Datenträger an. Verwenden Sie, wenn möglich, stattdessen die Befehlszeilenoption **/f** . Bei Verwendung der Option **/t** müssen Sie auch die Option **/n** verwenden. Diese Optionen bieten zusammen eine alternative Methode zum Angeben der Größe des Datenträgers, der formatiert wird. Diese Option ist mit der Option **/f** nicht gültig.                                                     |
| /n:\<Sektoren >  |                                                         Gibt die Anzahl der Sektoren pro Spur an. Verwenden Sie nach Möglichkeit die Befehlszeilenoption **/f** anstelle von **/n**. Bei Verwendung von **/n** müssen Sie auch **/t** verwenden. Diese beiden Optionen bieten zusammen eine alternative Methode zum Angeben der Größe des Datenträgers, der formatiert wird. Diese Option ist mit der Option **/f** nicht gültig.                                                         |
|  /p:\<übergibt >  |                                                                                                                                                               Setzt jeden Sektor auf dem Volume für die Anzahl der angegeben Durchgänge auf 0. Diese Option ist mit der Option **/q** nicht gültig.                                                                                                                                                                |
|       /c       |                                                                                                                                                                                     Nur NTFS. Auf dem neuen Volume erstellte Dateien werden standardmäßig komprimiert.                                                                                                                                                                                      |
|       /x       |                                                                                                                                                            Bewirkt, dass die Bereitstellung des Volumes vor seiner Formatierung bei Bedarf aufgehoben wird. Alle geöffneten Handles zum Volume sind nicht mehr gültig.                                                                                                                                                            |
|       /?       |                                                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                        |

## <a name="remarks"></a>Hinweise

-   Administratoranmeldeinformationen

    Sie müssen ein Mitglied der Gruppe "Administratoren" sein, um eine Festplatte zu formatieren.
-   Verwenden des **Formats**

    Der Befehl **Format** erstellt ein neues Stammverzeichnis und Dateisystem für den Datenträger. Er kann auch auf dem Datenträger nach fehlerhaften Bereichen suchen und alle Daten auf dem Datenträger löschen. Um einen neuen Datenträger verwenden zu können, müssen Sie diesen Befehl zuerst zum Formatieren des Datenträgers verwenden.
-   Hinzufügen einer Volumebezeichnung

    Nach dem **formatieren** einer Diskette wird die folgende Meldung angezeigt:

    `Volume label (11 characters, ENTER for none)?`

    Um eine Volumebezeichnung hinzuzufügen, geben Sie bis zu 11 Zeichen (einschließlich Leerzeichen) ein. Wenn Sie dem Datenträger keine Volumebezeichnung hinzufügen möchten, drücken Sie die EINGABETASTE.
-   Formatieren einer Festplatte

> [!NOTE]
> Sie müssen ein Mitglied der Gruppe "Administratoren" sein, um eine Festplatte zu formatieren.

Wenn Sie den Befehl **Format** verwenden, um eine Festplatte zu formatieren, wird eine Warnmeldung ähnlich der folgenden angezeigt:
```
WARNING, ALL DATA ON NON-REMOVABLE DISK 
DRIVE x: WILL BE LOST! 
Proceed with Format (Y/N)? _ 
```
Um die Festplatte zu formatieren, drücken Sie Y; Wenn Sie den Datenträger nicht formatieren möchten, drücken Sie N.
-   Einheiten Größe

    Bei FAT-Dateisystemen wird die Anzahl der Cluster auf nicht mehr als 65526 beschränkt. FAT32-Dateisysteme beschränken die Anzahl der Cluster auf zwischen 65527 und 4177917.

    Die NTFS-Komprimierung wird für Zuordnungseinheiten größer als 4.096 nicht unterstützt.

> [!NOTE]
> Beim **Format** wird die Verarbeitung sofort beendet, wenn festgelegt wird, dass die vorherigen Anforderungen nicht mit der angegebenen Clustergröße erfüllt werden können.
> -   **Formatieren** von Meldungen

    When formatting is complete, **format** displays messages that show the total disk space, the spaces marked as defective, and the space available for your files.
- Schnellformatierung

  Der Formatierungsprozess kann mithilfe der Befehlszeilenoption **/q** beschleunigt werden. Verwenden Sie diese Option nur, wenn es keine fehlerhaften Sektoren auf der Festplatte gibt.
- Verwenden von **format** mit einem neu zugewiesenen Laufwerk oder Netzlaufwerk

  Sie dürfen den Befehl **format** nicht auf einem Laufwerk verwenden, das mit dem Befehl **subst** vorbereitet wurde. Datenträger können nicht über ein Netzwerk formatiert werden.
- Exitcodes für **format**

  In der folgenden Tabelle sind alle Exitcodes und eine Kurzbeschreibung ihrer Bedeutung aufgeführt.  

  |Exitcode|Beschreibung|
  |---------|-----------|
  |0|Der Formatierungsvorgang war erfolgreich.|
  |1|Es wurden falsche Parameter angegeben.|
  |4|Ein schwerwiegender Fehler ist aufgetreten (bei dem es sich um einen Fehler handelt, der nicht 0, 1 oder 5 ist).|
  |5|Der Benutzer hat die N als Antwort auf die Eingabeaufforderung "mit Format fortsetzen (Y/N)" gedrückt. um den Vorgang zu beenden.|

  Sie können diese Exitcodes mithilfe der Umgebungsvariablen ERRORLEVEL und des Batchbefehls **if** überprüfen.
- Verwenden von **format** in der Wiederherstellungskonsole

  Der Befehl **format** steht in der Wiederherstellungskonsole mit verschiedenen Parametern zur Verfügung.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](https://technet.microsoft.com/library/cc771080.aspx)